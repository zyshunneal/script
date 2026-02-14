# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a single-script Python tool (`pt_kill_generator.py`) that generates `pt-kill` (Percona Toolkit) commands for killing MySQL queries/connections. It supports both batch output of all recommended commands and an interactive menu-driven mode.

## Running

```bash
# Generate all recommended commands for an instance
python pt_kill_generator.py --instance 10.0.1.100:3306

# With explicit defaults-file
python pt_kill_generator.py --instance 10.0.1.100:3306 --defaults-file /etc/my-pt.cnf

# RDS instance
python pt_kill_generator.py --instance rds-endpoint:3306 --user admin --rds

# Interactive mode
python pt_kill_generator.py --instance 10.0.1.100:3306 -i
```

## Key Design Decisions

- Compatible with Python 2.6+ and Python 3 (uses `from __future__ import print_function`, `%` formatting instead of f-strings).
- When `--defaults-file` is not specified, defaults to `/etc/pt-kill.cnf`.
- Every generated command is shown in two variants: `[预览]` (preview with `--print`) and `[执行]` (execute with `--kill-query` or `--kill`).
- `ptkillhelp.txt` is a reference copy of `pt-kill --help` output, not consumed by the script.
