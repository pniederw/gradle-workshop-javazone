#Wrapper

##Wrapper Task

* Wrapper task generates:
    * wrapper scripts
    * wrapper jar
    * wrapper properties

<!-- -->

    task wrapper(type: Wrapper) {
      gradleVersion = '1.2'
    }

##Wrapper Files

* build.gradle
* gradle
    * gradle-wrapper.jar
    * gradle-wrapper.properties
* gradlew
* gradlew.bat

<!-- -->

    >./gradlew assemble
