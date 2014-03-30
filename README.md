
# NetKernel Module Template Library

This contains a library of module templates that can be used by
the NetKernel Gradle plugin authored by 1060 Research
and others. See https://github.com/1060NetKernel/gradle-plugin

## Library format

As of release 0.0.2 of the Gradle plugin place a new module template
under the modules directory in /src/main/resources.
The name of the module template's directory will be displayed to
the user so make this significant.

When the user runs the task to create a module from a template the
complete contents of the module template (files and directories)
are replicated in the target module.

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

### Not Supported

MODULE_DESCRIPTION - this is not supported in the 0.0.2 release

MODULE_VERSION - this is not supported in the 0.0.2 release

Sets are not supported. This is a concept in which a user can select a named set which
might contain one or more module templates. Sets can be used to mirror the creation
of an Apposite package structure.

library-properties.xml - this is a meta information file that will contain information
that will be used by a future release of the Gradle plugin.


