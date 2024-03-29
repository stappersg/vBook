# Contributing to vBook and vSMTP documentation

Thanks for considering helping this project. There are many ways you can help.

There are opportunities to contribute to vSMTP at any level like translating, reviewing or making improvements to the documentation.

Even tiny pull requests (e.g., fixing a typo in API documentation) are greatly
appreciated.

## Help wanted

If you're looking for ways to help that don't involve large amounts of
reading or writing, check out the [open issues with the E-help-wanted
label][help-wanted]. These might be small fixes to the text, Rust code,
frontend code, or shell scripts that would help us be more efficient or
enhance the book in some way!

[help-wanted]: https://github.com/viridit/vbook/issues?q=is%3Aopen+is%3Aissue+label%3AE-help-wanted

## VSCode

To use the debugger, download the [codelldb](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) extension.

Run the task "Launch & configure vSMTP", then attach the debugger to the new process using the task "Debug vSMTP".
If the task is not permitted, that probably means that you cannot debug the process with ptrace. To solve this, use:

```sh
cat /proc/sys/kernel/yama/ptrace_scope
```

to check the scope of ptrace. If it is >= 1, this is why you cannot debug the process. Use:

```sh
echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope
```

To debug the process. Don't forget to set the ptrace_scope back to it's original value after you finish
you debug session. checkout [linux audit](https://linux-audit.com/protect-ptrace-processes-kernel-yama-ptrace_scope/) for more information.

## Licensing

vBook, vBook files and this repository are licensed under a Creative Commons Attribution-ShareAlike 4.0 International License by viridIT SAS. For further details please refer to the [License][License] file.

[License]: https://github.com/viridIT/vBook/blob/main/LICENSE

## Conduct

vBook project and viridIT teams adheres to the principles described in the
[Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/version/1/4/code-of-conduct/).
This is the minimum behavior expected from all contributors. Instances of
violations of the Code of Conduct can be reported by contacting the project team
at [moderation@viridit.com](mailto:moderation@viridit.com).
