# go-gitsafe

[![License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg)](https://github.com/go-gitsafe/gitsafe/blob/main/LICENSE)
[![Pure Go](https://img.shields.io/badge/pure%20Go-CGO%3D0-00ADD8?logo=go&logoColor=white)](https://github.com/go-gitsafe/gitsafe)
[![Go Reference](https://pkg.go.dev/badge/github.com/go-gitsafe/gitsafe.svg)](https://pkg.go.dev/github.com/go-gitsafe/gitsafe)

**Guards that do not rely on remembering.**

Two things went wrong on one machine, and neither was fixed by resolving to be
careful.

A token was written into a remote URL, and git echoed it back. Twice. It had to
be revoked and reissued both times.

A tested, green change went straight onto `main` — no branch, no pull request,
no checks run against it, read by nobody.

Documentation asks. A hook refuses.

## What is here

**[gitsafe](https://github.com/go-gitsafe/gitsafe)** — four programs and two
libraries, pure Go, no cgo, nothing outside the standard library.

- `git-pre-push-guard` — the **global** hook. Refuses a URL that carries a
  credential, and refuses a write to the branch pull requests land on, whoever
  runs git and whatever they run it with.
- `gitpush` — names a credential helper rather than reading the token, refuses a
  remote URL that carries one, and redacts what it prints by shape.
- `git-credential-tokenfile` — a minimal helper: a token file to git over a
  pipe, `get` only, and never to a terminal.
- `ghscopes` — what a token may do, without ever printing it.

## The rule these are built on

A guard that gets in the way is a guard that gets switched off. So what the hook
lets through is as considered as what it stops: **tags** go up untouched,
**creating** a default branch is allowed, and there is exactly one escape —
deliberate, one command at a time, and visible in the transcript afterwards.

The refusals say what to do instead. A guard that only says no teaches nothing,
and a person who has been stopped twice starts looking for the way round.
