# Gradle Workshop

JavaZone 2012

## About Me

* Peter Niederwieser ([@pniederw](http://twitter.com/pniederw))
* Principal Engineer at Gradleware
* peter.niederwieser@gradleware.com

Started using Gradle in 2010, joined Gradleware in 2011

Occasional Groovy committer, creator of [Spock](http://spockframework.org)

## Topics for Today

* Introduction to Gradle
* Incremental build
* Build scripts
* Tasks
* Plugins
* Testing
* Dependency management
* Multi-Project builds

## You

* Your background
    * What Groovy/Gradle experience do you have?
    * What build systems are you using or have experience with?

# Lab 01

Setup

## Gradle Setup

1. Download gradle-1.2-all-zip from [http://gradle.org/downloads](http://gradle.org/downloads) and extract it.
  (Alternatively, copy the zip from the USB stick.)
1. Clone [https://github.com/pniederw/gradle-workshop-javazone/](https://github.com/pniederw/gradle-workshop-javazone/) or download its zipball.
1. Add an environment variable `GRADLE_HOME` pointing to the top-level directory of the Gradle distribution.
1. Add `GRADLE_HOME/bin` to the `PATH` environment variable.
1. Activate the Gradle Daemon by setting the environment variable `GRADLE_OPTS` to `-Dorg.gradle.daemon=true`.
1. Open a terminal and execute `gradle -v`.

