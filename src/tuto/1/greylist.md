# Greylist

[Greylisting] is one method to defend a SMTP server against spam.

[Greylisting]: https://en.wikipedia.org/wiki/Greylisting_(email)

The goal is to temporarily reject emails from a sender that is not yet in registered in a database, then accepting it back if the sender retries.

<!-- markdown-link-check-disable-next-line -->
To build a greylist, you need to create a database and a vSMTP service. For this tutorial, we will use the [mysql](https://www.mysql.com/) database.

## The database

### Install MySQL

Please follow this great [tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04) to install MySQL.
<!-- markdown-link-check-disable-next-line -->
This setup has been tested on Ubuntu 22.04, check out the [MySQL website](https://www.mysql.com/) for other systems.

```sh
# Install mysql.
$ sudo apt update
$ sudo apt install mysql-server
$ sudo systemctl start mysql.service

# Login as root.
$ sudo mysql

# Replace auth_socket authentication by a simple password.
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your-password';
mysql> exit

# Update root password & remove unnecessary stuff.
$ sudo mysql_secure_installation

# Connect as root with the password.
mysql -u root -p

# Reset auth to auth_socket, this way you can connect with `sudo mysql`
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
<p class="ann"> Setting up MySQL </p>

### Setup a user

To manage your database, you should create a new user with restricted privileges instead of relying on root.

```sh
# Here we use localhost as our host but you could also setup your database on another server.
mysql> CREATE USER 'greylist-manager'@'localhost' IDENTIFIED BY 'your-password';
```
<p class="ann"> Creating a user named 'greylist-manager' </p>

### Setup the database and a table

To create the database, simply put the content of this sql code into a `greylist.sql` file.

```sql
CREATE DATABASE greylist;

CREATE TABLE greylist.sender(
    address varchar(500) NOT null primary key,
    user varchar(500) NOT null,
    domain varchar(500) NOT null
);
```
<p class="ann"> Template for the greylist database </p>

And then run the `mysql` command as root to generate the database.

```sh
sudo mysql < greylist.sql
```

Grant necessary privileges to your user on the newly create table.

```sh
mysql> GRANT SELECT, INSERT ON greylist.sender TO 'greylist-manager'@'localhost';
```

The greylist database is now operational.

## Setup vSMTP

To setup vSMTP, you first need to create a mysql service, that will enable you to query your database. You can, for example, write it in a `services.vsl` file where your `main.vsl` is located.

```rust,ignore
export const greylist = mysql(#{
    // Change this url to the url of your database, or keep it like this if the 'greylist-manager' user is setup on localhost.
    url: "mysql://localhost/?user=greylist-manager&password=your-password",
});
```
<p class="ann"> `services/db.vsl` </p>

The `query` function from the `mysql` service is used to query a mysql database. Variables are passed to the query using string interpolation.

> ⚠️ String interpolation can lead to SQL injection if not used properly. Make sure to sanitize your inputs, set only required privileges to the mysql user, and check what kind of data you are injecting.

Create a greylist rule in your root `filter.vsl` file.

```
import "services/db" as db;

#{
    // The greylist is effective in the "mail" stage, because the sender
    // of the email is received at this stage.
    mail: [
        rule "greylist" || {
            let sender = mail_from();

            // if the sender is not recognized in our database,
            // we deny the transaction and write the sender into
            // the database.
            if db::greylist.query(`SELECT * FROM greylist.sender WHERE address = '${sender}';`) == [] {
                // Writing the sender into the database.
                db::greylist.query(`
                    INSERT INTO greylist.sender (user, domain, address)
                    values ("${sender.local_part}", "${sender.domain}", "${sender}");
                `);

                // vsl exposes a `code_greylist` code which is a "451 4.7.1" enhanced code.
                deny(code_greylist)
            } else {
                // the user is known by the server, the transaction
                // can proceed.
                accept()
            }
        }
    ]
}
```
<p class="ann"> Declaring a greylist rule </p>
