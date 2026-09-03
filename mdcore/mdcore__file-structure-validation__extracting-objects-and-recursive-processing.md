<!-- source: https://www.opswat.com/docs/mdcore/file-structure-validation/extracting-objects-and-recursive-processing -->

# Extracting objects and recursive processing

Breaks files into discrete components (macros, hyperlinks, metadata, images, and embedded executables) for comprehensive visibility inside complex and nested file formats.

**Routing extracted objects to other engines:** You can choose which object classes are returned as output files.

Enable "*Include Structural Output Objects*"

And enable "Return Analyzed Objects", choose which objects should be processed recursively.

Objects that FSV extracts are handed back to the analysis workflow as regular files, so Multiscanning, Proactive DLP, Adaptive Sandbox, and other configured engines act on the child object rather than only on the outer container. Extracted objects are processed by every engine in the workflow (except Deep CDR).

An example an PDF file contains a zip attachment

The attachment is extracted by the Archive module and its child file is processed as well.
