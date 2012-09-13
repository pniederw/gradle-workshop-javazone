#Testing

##Test Task

* Support for JUnit and TestNG
* Parallel Testing
* Custom Fork Frequency
* Test Listeners
* Tests auto-detected in sourceSets.test.output
* name: 'test', type: Test
* input: sourceSets.test.output, sourceSets.test.runtimeClasspath

##Test Task Example

<!-- -->

    test {
      jvmArgs '-Xmx512M'
      include '**/tests/special/**/*Test.class' //disables auto-detection
      exclude '**/Old*Test.class'
      forkEvery = 30
      maxParallelForks = guessMaxForks()
      testLogging {
	    events "started", "passed", "skipped", "failed", "standardOut", "standardError"
	    showExceptions true
	    showStackTraces true
	    stackTraceFilters "truncate", "groovy"
      }
    }

    def guessMaxForks() {
      int processors = Runtime.runtime.availableProcessors()
      return Math.max(2, (int) (processors / 2))
    }

##Test Task Listeners

<!-- -->

    test {
      beforeTest { desc ->
        // do something
      }
      afterTest { desc, result ->
        // do something
      }
      afterSuite { desc, result ->
        // do something
      }
    }

##Check Task

* Hook for all validation tasks
* For example used by the code-quality plugin
* name: 'check', type: DefaultTask
* dependsOn: 'test', code quality tasks

#Lab 08

Testing