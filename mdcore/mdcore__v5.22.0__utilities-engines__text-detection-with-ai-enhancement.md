<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/utilities-engines/text-detection-with-ai-enhancement -->

# Text detection with AI

This feature is designed to address the challenge of text-based file detections. These files, such as log files, script files, and readme files, are all simply "text" and lack distinct characteristics revealed by other methods. Analyzing the contents is crucial for accurate classification.

To enable this AI feature:

- At **Inventory > Modules > Utilities > FileType**, Tick **Enable Machine Learning module**

- At **Workflow Management > Workflows > [Workflow name] > File Type > General**, Enable **Classify with Machine Learning**

Without AI enabled, CUDA source code is detected as a text file.

With AI enhancement, CUDA source code is detected as a CUDA file

Info

This feature is disabled by default. If you enable the AI-powered feature, OPSWAT will not use your content to train or fine tune its services. Unlike file signature matching, AI-based relies on heuristics and is not guaranteed to be precise. Experiment with your own dataset to determine if the AI engine fits your need.
