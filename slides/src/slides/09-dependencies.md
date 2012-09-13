#Dependencies

##Dependencies

* Repository dependencies
    * e.g. from Maven Central
    * with module descriptors (pom.xml/ivy.xml)
* Repository-less dependencies (specified by path)
* Project dependencies in a multi-project build
* Artifacts you want to upload
* Domain objects:
    * Repository
    * Dependency
    * Configuration
    * Artifact

##Dependencies

<!-- -->

    apply plugin: 'java'
    repositories {
      mavenCentral()
    }
    dependencies {
      //by String (GAV - group:artifact:version):
      compile 'junit:junit:4.10', 'org.mockito:mockito-core:1.9.0'

      //by Map:
      compile group: 'junit', name: 'junit', version: '4.10'

      //repository-less dependencies via FileCollection, FileTree instances:
      compile files('file1.jar'), fileTree('lib')

      //project dependencies:
      compile project(':otherProject')
    }

##Dependencies & Java Plugin

<!-- -->

    apply plugin: 'java'

    configurations {
      myConf.extendsFrom compile
    }

    dependencies {
      compile 'junit:junit:4.10'
      runtime group:'asm', name:'asm-all', version:'3.2'
      testCompile files('file1.jar')
      myConf 'log4j:log4j:1.2.9'
    }

* The Java plugin adds configurations
* Many Java plugin tasks use those configurations as default input values (e.g. test)
* Configurations can extend each other

##Working with Dependencies

* A configuration extends the FileCollection
* Configuration has a rich API

<!-- -->

    configurations.runtime.each { file ->
      println file
    }

    configurations.runtime.dependencies { dep ->
      dep.group == 'org.gradle'
    }.each {
      println it
    }

    copy {
      from configurations.runtime
      into 'someFolder'
    }

#Lab 09

Dependencies

##Transitive Dependencies

* Advantage of repository dependencies
* pom.xml/ivy.xml model describes the transitive dependencies
* Default version conflict resolution is *newest*
* Option to use *fail* conflict resolution
* Transitive resolution is customizable

<!-- -->

    dependencies {
      compile('org.hibernate:hibernate:3.1') {
        force = true
        exclude module: 'cglib'
      }
      compile('org:somename:1.0-SNAPSHOT') {
        transitive = false
        changing = true
      }
    }
    configurations.myconf {
      transitive = false
      resolutionStrategy.failOnVersionConflict()
    }

##Repositories

* Any Maven/Ivy repository can be used
* Very flexible layouts are possible for Ivy repositories

<!-- -->

    repositories {
      mavenLocal()
      mavenCentral()
      maven {
        name 'codehaus'
        url 'http://repository.codehaus.org'
      }

      ivy {
        url 'http://repo.mycompany.com'
        layout 'gradle' // default
      }

      flatDir(dirs: ['dir1', 'dir2'])
    }

##Uploading

* Upload your artifacts to any Maven/Ivy repository
* ivy.xml/pom.xml is generated
* Repository metadata (e.g. maven-metadata.xml) is generated

##Uploading to Ivy Repos

<!-- -->

    task myJar(type: Jar)

    artifacts {
      archives myJar
    }

    uploadArchives {
      repositories {
        ivy {
          url 'http://repo.mycompany.com'
          credentials {
            username 'john'
            password 'secret'
          }
        }
      }
    }

##Uploading to Maven Repos

* The uploaded POM is fully customizable
* You can use all wagon protocols for uploading
* You can install to your local Maven repo

##Customizing the Pom

<!-- -->

    uploadArchives {
      repositories.mavenDeployer {
        repository(url: 'file://localhost/mavenRepo/')
        pom.project {
          licenses {
            license {
              name 'Apache License, Version 2.0'
              url 'http://.../LICENSE-2.0.txt'
            }
          }
        }
        whenConfigured { pom ->
          pom.dependencies.
            find { it.artifactId == 'junit' }.
              optional = true
        }
      }
    }