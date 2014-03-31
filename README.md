
# NetKernel Module Template Library

This contains a library of module templates that can be used by
the NetKernel Gradle plugin authored by 1060 Research
and others. See https://github.com/1060NetKernel/gradle-plugin

Community members may add to this library or construct their
own module template libraries and publish them as JAR files.
The NetKernel Gradle plugin searches for template libraries
in Maven repositories - which may be local or in a public
location.

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


| User Input | Description | Substitution Variable |
| Module URN | The URN for the module | MODULE_URN |

The user will be asked for the URN of the module and that information
will be used to create substitutions within any file that is copied
from the template.

The following substitutions are supported:

MODULE_URN - this is exactly the URN provided by the user.

MODULE_URN_CORE - this is the URN provided by the user with the trailing portion removed.
For example, if the user enters urn:org:netkernelroc:lang:groovy:test the corresponding
MODULE_URN_CORE is urn:org:netkernelroc:lang:groovy.

MODULE_URN_RES_PATH - this is an ROC res: URI constructed from the URN. For example
a URN of urn:org:netkernelroc:lang:groovy will have a corresponding MODULE_URN_RES_PATH
of res:/org/netkernelroc/lang/groovy.

MODULE_URN_RES_PATH_CORE - this is an ROC res: URI constructed from the user provided
URN with the trailing part removed. For example, a URN of urn:org:netkernelroc:lang:groovy:test
will have a corresponding MODULE_URN_RES_PATH_CORE of res:/org/netkernelroc/lang/groovy.

MODULE_SPACE_NAME - this is the name that is displayed in the Space Explorer. For example
"Lang / Kotlin" is the space name for the Kotlin language core support module.

## Not Supported

MODULE_DESCRIPTION - this is not supported in the 0.0.2 release

MODULE_VERSION - this is not supported in the 0.0.2 release

Sets are not supported. This is a concept in which a user can select a named set which
might contain one or more module templates. Sets can be used to mirror the creation
of an Apposite package structure.

library-properties.xml - this is a meta information file that will contain information
that will be used by a future release of the Gradle plugin.


