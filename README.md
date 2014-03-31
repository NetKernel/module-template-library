# NetKernel Module Template Library

This repository contains a library of module templates that can be used by
the NetKernel Gradle plugin authored by 1060 Research
and others. See https://github.com/1060NetKernel/gradle-plugin

Community members may add to this library or construct their
own module template libraries and publish them as JAR files.
The NetKernel Gradle plugin searches for template libraries
in Maven repositories - which may be local or in a public
location.

## Using the Gradle Plugin with Template Libraries

Include a Gradle build file with the following content:

    apply plugin: 'netkerneltemplates'
    apply plugin: 'maven'
    apply plugin: 'java'

    repositories {
      mavenLocal()
      mavenCentral()
      maven {
        url "http://maven.netkernelroc.org:8080/netkernel-maven"
      }
    }

    buildscript {
      repositories {
        mavenLocal()
        mavenCentral()
        maven {
          url "http://maven.netkernelroc.org:8080/netkernel-maven"
        }
      }
      dependencies {
        classpath group: 'org.netkernel', name: 'gradle-plugin', version: '0.0.2'
      }
    }

    dependencies {
      templates   group: 'org.netkernelroc',    name: 'module-template-library', version: '1.0.0'
    }

Note: It is suggested the you use a file name other than build.gradle and use the -b option when
running Gradle. The reason is that you will like only run the template feature once and then
create a more standard build.gradle file for your project.


## Template Library JAR File Format

The published template library JAR file must have the following
structure:

    /META-INF/MANFEST.FM
    /modules
            /<module-template-name>
                                   /src/main/resources
                                                      /module.xml
                                   /src/main/java/


The name given for the template (module-template-name) is displayed to
the user of the Gradle plugin and is used by the user to select
template, so make this representative of the template
and unique within the JAR file. (It also should be unique across all
module template libraries, however, this restriction will be lifted
in a subsequent release of the plugin.

## Template Substitution Variables

When creating files for a template library one can use the following
substitution markers.
The Gradle plugin will ask the user for certain information which will
be used to create substitution values for the variables.


User Input | Description | Substitution Variable | Description
----- | ----- | ----- | ----
Module URN | The globally unique identifier for the module. | MODULE_URN | Use where the full module URN as entered by the user should be used
  |  |  MODULE_URN_CORE | The URN entered by the user with the final portion stripped off. Use this when the user might enter some with a :test suffix and you need the URN without the final portion.
  |  |  MODULE_URN_RES_PATH | A res:/ URI scheme with the module's URN translated into a directory path. For example, the URN urn:org:netkernelroc:lang:scala will be converted to res:/org/netkernelroc/lang/scala .
  |  |  MODULE_URN_RES_PATH_CORE | A res:/ URI scheme with the module's URN (stripped of the final portion translated into a directory path). For example, the URN urn:org:netkernelroc:lang:scala:test will be converted to res:/org/netkernelroc/lang/scala .
Module Space Name | The name displayed in the Space Explorer | MODULE_SPACE_NAME | For example "Lang / Scala"
Module description | A brief description of the module | MODULE_DESCRIPTION | For example "Support for the Scala language."
Module version | The initial version number of the module | MODULE_VERSION | If not provided, defaults to 1.0.0

When the user of the NetKernel Gradle plugin requests the creation of a module from a template,
they will be asked a series of questions - such as the module's URN.
The answers to these questions are used by the plugin to create substitution values
for the substition markers as described above.
