#Multi-Project Builds

##Multi-Project Builds

* Flexible directory layout
* Configuration injection
* Project dependencies & partial builds
* Separate configuration/execution hierarchy

##Configuration Injection

* __ultimateApp__
    * api
    * webservice
    * shared

<!-- -->

    subprojects {
      apply plugin: 'java'
      dependencies {
        testCompile 'junit:junit:4.7'
      }
      test {
        jvmArgs '-Xmx512M'
      }
    }

##Filtered Injection

* __ultimateApp__
    * api
    * webservice
    * shared

<!-- -->

    configure(nonWebProjects()) {
      jar.manifest.attributes
         Implementor: 'Gradleware'
    }

    def nonWebProjects() {
      subprojects.findAll { project ->
        !project.name.startsWith('web')
      }
    }

##Project Dependencies

* ultimateApp
    * __api__
    * webservice
    * shared

<!-- -->

    dependencies {
      compile 'commons-lang:commons-lang:2.4'
      compile project(':shared')
    }

##Partial Builds

* ultimateApp
    * __api__
    * webservice
    * shared

<!-- -->

    >gradle build
    >gradle buildDependents
    >gradle buildNeeded

##Multi-Project Builds

* There is  no __one-size-fits-all__ project structure  for the  enterprise
* The physical  structure of your  projects should  be determined by your  requirements

##Name Matching Execution

* __ultimateApp__
    * api
    * webservice
    * shared

<!-- -->

    >gradle build
    >gradle classes
    >gradle war

##Task/Project Paths

* For projects and tasks there is a fully qualified path notation:
    * : (root project)
    * :clean (the clean task of the root project)
    * :api (the api project)
    * :services:webservice (the webservice project)
    * :services:webservice:clean (the clean task of webservice)

<!-- -->

    >gradle :api:classes

##Defining a Multi Project Build

* settings.gradle (location defines the root)
* root project is implicitly included

<!-- -->

    //declare projects:
    include 'api','shared','services:webservice'

    //Everything is configurable:

    //default: root dir name
    rootProject.name = 'main'

    //default: 'api' dir
    project(':api').projectDir = '/myLocation'

    //default: 'build.gradle'
    project(':shared').buildFileName = 'shared.gradle'

#Lab 10

Multi-Project Builds