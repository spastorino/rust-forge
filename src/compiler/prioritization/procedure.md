# Procedure

This document details the procedure the WG-prioritization follows to fill the agenda for the [weekly meeting](https://hackmd.io/pHb6eTZ2Sjy6XZmwXZHIBA?view) of `T-compiler`.
The working group focuses mainly on triaging `T-compiler` and `libs-impl` bugs, deciding if bugs are critical (potential release blockers) or not.

## The procedure in detail

High level overview:

- Follow ups from previous meeting
  - Remove `I-nominated` tags of already discussed issues
  - Notify @pnkfelix about stable/beta-nominated issues without stable/beta-accepted labels
  - Create the next meeting agenda using [the weekly agenda template
- Prepare contents of the agenda and set up everything in place
  - Prioritize "Unprioritized I-prioritize" issues
  - Prioritize regressions without P label
  - Summarize beta nominations
  - Summarize stable nominations
  - Summarize PR's waiting on team
  - Summarize P-criticals
  - Summarize unassigned P-high regressions
  - Summarize nominations
- Prepare agenda items
  - Accept MCPs pending to be accepted
  - Sanity check beta nominations
  - Sanity check stable nominations
  - Sanity check PR's waiting on team
  - Sanity check regressions
  - Sanity check nominations
- Generate Agenda
  - Run cli to generate agenda
  - Fill agenda announcements
- Notify the team about the meeting
  - Figure out which WGs need to check-in
  - Notify the team about the meeting
    - Share the agenda
    - Notify WG leads about checkins
- Final reviews
  - Re-sync agenda some minutes before the meeting
  - Check toolstate
  - Check performance stats

### Follow ups from previous meeting

The agenda is created as soon as we finish our thursday's weekly meeting.

#### Remove `I-nominated` tags of already discussed issues

### prepare contents of the ...

#### Sanity check beta nominations

- Get a list of all the issues labelled with beta-nominated
- Check if all of them have a team label (T-* or libs-impl)
- If such labels are missing, label the issue with the appropriate
  T-compiler or libs-impl when it corresponds

###  ...

---

## Async procedure

1. The agenda is created as soon as we finish our thursday's weekly meeting.
2. Unprioritized issues: a Zulip topic is created requesting prioritization when an issue is labelled with `I-prioritize`. Regressions and `I-unsound` issues that do not `requires-nightly` are automatizally tagged with `I-prioritize`.
3. stable/beta nominations, `I-nominated` and PRs `S-waiting-on-team`: a Zulip topic is created requesting addition of these items to the agenda.
4. `P-critical` issues and `P-high` regressions: A Zulip topic is created requesting addition of these items to the agenda.
5. Once we do all this, some things from the triagebot script could be removed
6. We probably want the script to integrate with triagebot
   1. we could run `@triagebot prioritization pendings` on wednesdays mornings and have that figuring out what's pending an opening issues or bumping existing ones to notify us what we need to do
   2. we could run `@triagebot prioritization agenda` and have that dumping out the agenda. I'm not 100% sure about this we are going to be filling the agenda as we go. So maybe it's more appropriate to have stuff like `@triagebot prioritization agenda issues-of-note`, `@triagebot prioritization agenda nominations` and things like that so the script could dump parts of the agenda we need to update.

## Drafting the meeting agenda

The draft is currently prepared by running a CLI tool.

Note: In general for issues that not labeled with `T-compiler` or `libs-impl`, add the appropriate labels.

These steps are:

- [Unprioritized I-prioritize](#1-unprioritized-i-prioritize)
- [Regressions](#2-regressions)
- [Stable/Beta nominations](#3-stablebeta-nominations)
- [Pull requests waiting for team](#4-pull-requests-waiting-for-team)
- [High priority and critical unassigned regressions](#5-p-critical-and-unassigned-p-high-regressions)
- [Agenda](#6-agenda)
- [Final meeting review and announcements](#7-final-review)

Below each step of the Triagebot CLI is explained.

### 1. Unprioritized I-prioritize

We need all `I-prioritize` issues for `T-compiler` and `libs-impl` to be actually prioritized. To do so, we add one of the `P-critical`, `P-high`, `P-medium` or `P-low` labels and remove `I-prioritize` and also add a text like: "Assigning `P-XXX` as [discussed as part of the Prioritization Working Group procedure](link_to_zulip_conversation) and removing `I-prioritize`."

Note: These lists should typically be empty when we are close to the meeting.

We should:

- Prioritize these issues
- Tag regressions accordingly
- [Notify the appropriate groups](https://rustc-dev-guide.rust-lang.org/notification-groups/about.html)
- Nominate the issues that needs some dicussion

### 2. Regressions

We should not have unprioritized regressions and ideally regressions should be assigned to somebody.

#### Stable/Beta/Nightly regressions without P-label

For stable regressions, we are trying to get this list down to zero unprioritized issues right now. The idea is that on every iteration we add `I-prioritize` to 4 issues from this list, so soon we will have zero elements here.

We should:

- Prioritize these issues
- [Notify the appropriate groups](https://rustc-dev-guide.rust-lang.org/notification-groups/about.html)
- Nominate the ones worth discussing
- Assign if possible; if it remains unassigned, add it to agenda so we can assign during the meeting

### 3. Stable/Beta nominations

- Add them to the agenda explaining:
  - Why was it nominated
  - Who is assigned
  - Add important details

Issues labeled with `I-nominated` are important issues that we decide deserve discussion during the weekly meeting.

We should:

- Check if they were already discussed and in that case remove `I-nominated` label
- Check if each issue is worth the discussion time
- Add them to the agenda explaining:
  - Why was it nominated
  - Who is assigned
  - Is this an issue or a PR: if an issue, does it have a PR that fixes it?
  - Add important details

### 4. Pull requests waiting for team

These are PRs waiting for some decision by our team (T-compiler or libs-impl).

We should:

- Add them to the agenda explaining:
  - What are they waiting for
  - Add important details
- Explicitly nominate any that you think may be able to be resolved *quickly* in triage meeting.

### 5. P-critical and Unassigned P-high regressions

- [Notify the appropriate groups](https://rustc-dev-guide.rust-lang.org/notification-groups/about.html)
- Push them forward, if possible
- Assign if possible; if the issue remains unassigned, add it to agenda so we can assign it during the meeting

### 6. Agenda

At this point of the script the agenda is generated.

#### Nominate issues

Check how packed the agenda looks like and if there's room for more, consider important issues:

- [All P-critical](https://github.com/rust-lang/rust/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3AP-critical+)
- [T-compiler P-high](https://github.com/rust-lang/rust/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3AT-compiler+label%3AP-high+)
  - [unassigned](https://github.com/rust-lang/rust/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3AT-compiler+label%3AP-high+no%3Aassignee)
- [libs-impl P-high](https://github.com/rust-lang/rust/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3Alibs-impl+label%3AP-high+)

### Fill agenda announcements

Check the compiler calendar to see if there's an outstanding event to announce and add them to the agenda.

#### Toolstate

Check [toolstate](https://rust-lang-nursery.github.io/rust-toolstate/) for tool breakage and notify teams in the corresponding channels.

#### Performance regressions

- Add Triage Logs to the agenda
  - https://github.com/rust-lang/rustc-perf/tree/master/triage#triage-logs
- Check [perf regressions](http://perf.rust-lang.org/index.html).
  - Notify involved actors.

## Notify the team about the meeting

### Figure out which WGs need to check-in

[Check which working groups should do their check-ins.](https://rust-lang.github.io/compiler-team/about/triage-meeting/)
`YYYY-MM-DD` is the date of the meeting.

### Notify the team about the meeting

A topic on Zulip will be created with the following format

Title:

`[weekly meeting] YYYY-MM-DD #54818` in `#t-compiler/meetings`

Content:

```text
Hi @*T-compiler/meeting*; the triage meeting will be starting in ~ X hours Y minutes
The @*WG-prioritization* have done pre-triage in #**t-compiler/wg-prioritization**
@*WG-prioritization* have prepared the [meeting agenda](link_to_hackmd_agenda)
We will have checkins from @*WG-X* and @*WG-Y*
@**person1** do you have something you want to share about @*WG-X*?
@**person2** do you have something you want to share about @*WG-Y*?
```
