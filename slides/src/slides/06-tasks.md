#Tasks

##Tasks

* Tasks are the basic unit of work in Gradle
* Tasks have a list of actions to be executed

<!-- -->

	// A task with one action 
	task hello {
	  doLast { 
	    println "Hello!"
	  }
	} 
	
	tasks.add(“hello”).doLast { println "world" }
	
	hello.doFirst { print "Hello " }
	
	
#Lab 04

Tasks

##DSL Syntax And Tasks

<!-- -->
    // declare a task:
	task hello 
	
	// direct access is fine for single statements:
	hello.dependsOn otherTask
	
	// for multiple statements use block syntax: 
	hello { 
	  dependsOn otherTask 
	  doLast { println 'Hello' }
	}
	 
	// declare and configure task at once:
	task hello { 
	  dependsOn otherTask 
	  doLast { println 'Hello' } 
	}
	
## Task Types and API

* Tasks have a type and API
* If not specified, type is DefaultTask
* All tasks implement the Task interface 
* Many built-in task types
* Most task types already have an action

## Task Types and API

<!-- -->

    // a task of type DefaultTask:
	task hello { 
	  doLast { 
		println 'Hello' 
	  } 
	}
	
	// using the task API:
	hello.onlyIf { day == 'monday' }
	
	// 'Copy' type and 'from' API:
	task copy(type: Copy) { 
	  from 'someDir' 
	} 
	
## Custom Task Types

* Extend DefaultTask
* Declare action with @org.gradle.api.tasks.TaskAction

<!-- -->

	class FtpTask extends DefaultTask { 
	  String host = 'docs.mycompany.com'
	   
	  @TaskAction 
	  void ftp() { 
		// do something complicated
	  } 	
	}
	
#Lab 05

Custom Tasks

## Why custom tasks

* Avoid global properties and methods
* Separate the imperative from the declarative
* Easy to refactor (e.g. from build script to Jar)

## Task dependencies

* Tasks can depend on each other
* Execution of one task requires prior execution of another task
* Executed tasks form a directed acyclic graph

<!-- -->

	task foo

	// multiple ways to declare task dependencies 
	task bar(dependsOn: foo)  
	bar { dependsOn foo } 
	bar.dependsOn foo 
	  
	// What happens here? 
	task bar { 
	  doLast { 
		dependsOn foo
	  }
	}

#Lab 06

Task dependencies