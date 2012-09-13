# Incremental Build

## Incremental Build

Gradle has *build avoidance* built in. A task gets executed iff:

* its inputs have changed OR
* its outputs aren't available anymore

Otherwise, the task is considered *up-do-date*. (Use `clean` or `--rerun-tasks` to override.)

Example: `JavaCompile` task

Inputs: Source code, compile class path, target Java version, etc.

Outputs: Class files

Build avoidance is a *generic* Gradle feature. Use it for your own tasks!

# Lab 03

Incremental Build

