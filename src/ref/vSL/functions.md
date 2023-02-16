# Standard functions & operators

The following modules lists:
- All standard functions available for email filtering. (referred by the `fn` keyword)
- Operators. (referred by the `op` keyword)
- Objects getters. (referred by the `get` keyword)
- Objects setters. (referred by the `set` keyword)

Documentation for each function is written using [markdown](https://www.markdownguide.org/), and is split between `sections`:

| Name                  | Description | 
| :-------------------- | :-------------------------- |
| Args                  | Arguments to pass to the function. |
| Return                | What result does the function return. |
| Effective smtp stage  | Stage of the rule engine where this function can be called from. |
| Note                  | Additional comments for the function. |
| Examples              | vSL examples using the function. |
| Errors                | Errors that can happen during the execution of the function. WARNING: this means that the function can throw an exception. Exceptions stops the evaluation of the rule engine and return a deny code. To handle exceptions, checkout the [`try catch` statement](https://rhai.rs/book/language/try-catch.html#catch-exceptions) in Rhai. |
<p class="ann"> Available documentation sections and their purpose </p>