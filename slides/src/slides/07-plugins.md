#Plugins

##Two Flawors of Plugins

* Script plugin: Another (local or remote) build script
* Binary plugin: A class implementing org.gradle.api.Plugin

##Applying Plugins

* Any Gradle script can act as a plugin
* Binary plugins must be on the build script class path
    * Can have ID (mapped to class name via plugin descriptor)
    * Will learn later how to add elements to the build script class path
    * The built-in plugins are already on the build script class path

<!-- -->

    //script plugin:
    apply from: 'otherScript.gradle'
    apply from: 'http://mycomp.com/otherScript.gradle'

    //object plugin:
    apply plugin: org.gradle.api.plugins.JavaPlugin
    apply plugin: 'java'

##What Plugins Can Do

* Configure the project object (e.g. add task instances)
* Add other classes to class path (e.g. custom task types)
* Add properties and methods to project object (extend DSL)
* Build script decomposition
    * Separate imperative from declarative
    * Modularization
* Code reuse

##Non Project Plugins

<!-- -->

    apply {
      from 'http://mycompany.com/jarPlugin.gradle'
      to jarTask1, jarTask2  
    }

##Standard Gradle Plugins

* Standard plugins apply other plugins:
* 'Base' plugins have a role of an unopinionated toolkit

<!-- -->

    base
    java -> java-base -> base
    groovy -> groovy-base -> java-base
    scala -> scala-base -> java-base
    application -> java
    war -> java
    jetty -> war
    ear -> base
    osgi -> java-base
    antlr -> java
    code-quality -> reporting-base
    maven -> base
    eclipse
    idea
    announce
    sonar
    signing	-> base
    cpp-lib	-> cpp
    cpp-exe	-> cpp

#Lab 07

Applying Plugins