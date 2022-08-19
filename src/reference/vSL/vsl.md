# vSL - the vSMTP Scripting Language

vSL is a lightweight scripting language dedicated to email filtering. It is based on the [Rhai] scripting language.

> Code highlighting is available for Microsoft [VSCode](https://code.visualstudio.com/) IDE, using the [Rhai extension](https://marketplace.visualstudio.com/items?itemName=rhaiscript.vscode-rhai).

[Rhai]: https://rhai.rs/

To interact with the SMTP traffic, vSL combines:

- filtering [rules].
- Configuration-like [objects]
- email utilities wrapped in [functions].
- [services] to interact with third-party software

[rules]: rules.md
[objects]: objects.md
[functions]: api.md
[services]: services.md

Rules can be applied at any [stage] of the SMTP transaction.

[stage]: stages.md

The [delivery] system uses the same concepts by applying rules to targeted domains and users.

[delivery]: delivery.md

These sections describe the gist of how the rule system works. Advanced user can use the [Rhai] scripting language on top of vSL to create and manage a wide variety of actions.
