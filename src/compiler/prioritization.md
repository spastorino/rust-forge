# Prioritization

Issues prioritization and [triaging](triage-meeting.html) is the process to assign a priority value to issues based on their impact on users and developers.

This section documents the prioritization process for issues of the rust-lang repository.

- [Procedure](prioritization/procedure.html)
- [Priority levels](#)

## A typical triaging workflow

#### 1. Issue gets filed on the [rust-lang repository](https://github.com/rust-lang/rust)

#### 2. Release team applies labels to issues

One or more "area" labels are applied to identify the area of responsability. Area labels are expressed as `A-*` (ex. "A-error-handling", "A-ffi", ... full list [here](https://github.com/rust-lang/rust/labels?q=A-))

One or more "team" labels are applied to assign responsability for that issue to the relevant team(s). Team labels are expressed as `T-*` (ex. "T-cargo", "T-compiler", ... full list [here](https://github.com/rust-lang/rust/labels?q=T-))

If bisection is needed, a [MCVE](https://stackoverflow.com/help/minimal-reproducible-example) is requested as well:

* label `needs-bisection`, `needs-mcve` are added to the issue
* label `ICEBreaker-Cleanup-Crew` is added to the issue (they can help improving the quality of the report, by producing a MCVE or the bisection)

In general, if the scope and impact of the issue is straightforward to understand, it is directly prioritized or sent to the relevant area, otherwise it is  "nominated" for compiler team meeting (that is, appointed for discussion during the meeting).

#### 3. Release team nominates for compiler team to further process (TODO: improve this section)

* also cc folks to bisect
* (usually ICE), usually includes needs-bisection and needs-mcve

#### 4. Compiler team triage group analysis

If the issue is found to be a critical bug, the label [P-critical](priority-levels.html#p-critical) will be applied and a discussion will happen whether the issue need to be delegated to another team.
