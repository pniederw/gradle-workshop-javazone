#Build Scripts

##Groovy

* A Ruby or Python like language that is tightly integrated with the Java platform
* Compiles to byte code
* Design goal is to be easily picked up by Java developers
* Reuse of Java semantics and API

##Groovy Closures

* Closures are code blocks
* Related to lambdas, function pointers, anonymous inner classes
* The Gradle DSL and the Groovy API uses them extensively

<!-- -->

    def sayHello = { println "Hello!" }
    sayHello()

    def sayHelloTo = { person -> println "Hello " + person + "!" }
    sayHelloTo("John")

    void foo(String name, Closure block) {
      println block.call(name)
    }

    // prints gredle
    foo("gradle") { String name ->
      name.replace ("a", "e")
    }

##Groovy Collection Operations

    [1, [2,3]].flatten() // [1, 2, 3]
    ['a', 'b'].each { item -> println item }
    ['a', 'b'].collect { it + '1' } // ['a1', 'b1']
    ['a', 'b', 'c'].findAll { it != 'c' } // ['a', 'b']
    [1, 2, 3].every { it < 3 } // false
    [1, 2, 3].any { it < 3 } // true
    // many more

* Thanks to Groovy, Gradle's API can stay light-weight
* Learning Groovy has many benefits. It is a powerful tool for many purposes (e.g. testing)
* The book Groovy in Action (2nd Ed) is the standard reference for Groovy

##Gradle Build Scripts

* Must be compilable by Groovy
* Can’t be executed by plain Groovy runtime
* Delegate to an associated org.gradle.api.Project object

<!-- -->

    // does not compile:
    println 'Gradle

    // compiles, fails when run with Groovy or Gradle:
    println zipCode

    // compiles, fails when run with plain Groovy:
    println name

##Gradle Build Scripts

* **Configure** the Project object
* Do **not** execute the build

##Gradle Build Daemon

* Using the daemon
    * enable by --daemon command line option
    * or better via 'org.gradle.daemon=true' line in your 'gradle.properties'
    * you can stop the daemon via `gradle --stop`
* Long running process
* Snappy builds
* The future of Gradle (preemptive UP-TO-DATE checks, remote dependency check, etc.)
