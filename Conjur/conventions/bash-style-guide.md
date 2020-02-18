# Bash Style Guide

## Table of Contents
- [Bash Style Guide and Best Practices](#bash-style-guide-and-best-practices)
  * [Style Baseline](#style-baseline)
  * [Testing](#testing)
  * [Further Reading](#further-reading)

## Bash Style Guide and Best Practices

Many of our projects rely on bash scripts to automate or simplify building, running, or testing. It
is important that we have standardized conventions for these bash scripts, to provide a consistent
experience developing across projects.

Much of the content for this style guide is drawn from publicly available bash style guides.

This guide is intended to be a "living document" in the sense that it's expected that it will evolve
as we refine and hone our bash knowledge base.

## Style Baseline
- **Styling** 
    - ***Pure Bash Bible*** - commonly-known and lesser-known methods of doing various tasks using
      only built-in bash features
    - ***Pure sh Bible*** - commonly-known and lesser-known methods of doing various tasks using
      only built-in POSIX sh features

- **Google Shell Style** ([Google Shell Style Guide](https://google.github.io/styleguide/shell.xml))

- **On Extensions** ([Google Style Guide: File
  Extensions](https://google.github.io/styleguide/shell.xml#File_Extensions)) - Quote from Jonah
  Goldstein (@jonahx)
> "**Executables** should have no extension (strongly preferred) or a .sh extension. **Libraries**
must have a .sh extension and _should not_ be executable. <br /> <br /> Thus, if you have a file a
with bash utility functions meant to be included by other bash scripts, name it, eg, `utils.sh` and
don’t make it executable. <br /> <br /> If you have some script meant to be executed directly, name
it by what it does, eg  `upload_files`, make it executable, and do not give it an extension.  In
this use case the language (whether bash or something else) is an implementation detail.

- **On Flags**  - Quote from Jonah Goldstein (@jonahx)
> Please don’t use the short versions of flags in scripts. The short versions of flags exist to save
keystrokes in an interactive terminal sessions. Scripts are meant to be read."

## Testing
- **BATS** ([Bash Automated Testing System](https://github.com/sstephenson/bats)) 

## Linting
- **Static Analysis** ([shellcheck](https://github.com/koalaman/shellcheck))
