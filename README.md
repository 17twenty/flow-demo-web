# flow-demo-web

A demonstration repository for [flow](https://github.com/17twenty/flow). There
is no application here. The point is the workflow around it.

## The board

Tickets live on [project 3](https://github.com/users/17twenty/projects/3),
which has the lean-kanban columns flow's default preset describes:

| Column | What it means |
|---|---|
| Backlog | somebody wrote it down |
| Ready | it meets the Definition of Ready, so it can be started |
| In progress | somebody is working on it |
| In review | the work is open as a pull request |
| Done | the work merged |

## What moves a ticket

`.flow.yaml` names who moves work for each event, and flow refuses to pretend
otherwise. Backlog to Ready is nobody's job: flow judges readiness and reports
it, but a person decides when work starts.

| Event | To | Who moves it |
|---|---|---|
| a draft pull request opens | In progress | flow, from the gate |
| it is marked ready for review | In review | flow, from the gate |
| changes are requested | In progress | GitHub's own project automation |
| it merges | Done | GitHub's own project automation |
| the issue closes | Done | GitHub's own project automation |

The gate is `.github/workflows/flow.yml`. It runs `flow check pr` on every
pull request event, posts `flow/policy`, and makes the moves above that are
flow's to make.

## The worked example

Pull request #6 is the one that made the gate work: it ran from its own
branch, judged the change that repaired it, and posted the first green
`flow/policy` this repository has had.
