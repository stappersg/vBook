# vSL - the vSMTP Scripting Language

vSL is a lightweight scripting language dedicated to email filtering. It is based on the [RHAI] scripting language. 

[RHAI]: (https://rhai.rs/)

vSL has no notion of a "main" program. vSL files are analyzed and executed by vSMTP through specific function calls. However, advanced users can use the RHAI scripting language on top of vSL to create and manage a wide variety of actions.

To interact with the SMTP traffic vSL combines declarative [rules] with [objects] and [actions].

[rules]: rules.md
[objects]: objects.md
[actions]: actions.md

These rules can be applied at any [stage] of the SMTP transaction.

[stage]: stages.md

The [delivery] system uses the same concepts by applying rules to targeted domains and users.

[delivery]: delivery.md

Communication with third-party software is provided by user-defined [services]. Like other objects, these services can be invoked through vSL rules.

[services]: services.md