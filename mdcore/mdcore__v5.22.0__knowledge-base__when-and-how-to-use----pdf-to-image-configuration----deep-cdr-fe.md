<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/when-and-how-to-use----pdf-to-image-configuration----deep-cdr-fe -->

# When and how to use “PDF to Image Configuration” Deep CDR feature?

**Introduction**:

This knowledge base article provides detailed instructions on how and when to use the “PDF to Image Configuration” feature which is part of Deep CDR.

**Details**:

“PDF to Image Configuration” feature is taking effect only when you use PDF to image(ex.: jpg etc.) conversion for PDF files.

This can be configured using the following path: in MetaDefender Core when Deep CDR engine is licensed using the following path: Under “Workflow Management” - click on“Workflows” - Choose the workflow in scope - click on tab “Deep CDR” - Enable Deep CDR if it’s disabled - scroll down to the section “Enable for filetypes” - click on “Edit” - expand “Adobe Files” - enable “PDF” - under section “Output” select “jpg” - click “OK” - click “Save changes”

The feature “PDF to Image Configuration” can be found in MetaDefender Core when Deep CDR engine is licensed using the following path: Under “Workflow Management” - click on“Workflows” - Choose the workflow in scope - click on tab “Deep CDR” - Enable Deep CDR if it’s disabled - scroll to the bottom of the page - click “Advanced Configuration” - scroll down to the section “File type handling” - expand “Adobe” - click on “PDF” - in the new window scroll down as per screenshot below -click “OK” - click “Save changes”

Below is an example of such implementation:

- Using the sample file:

**Conversion: PDF to JPG.**

- **LOW setting:** file size 340KB, dimension is 1759x2490 pixels.

- **MEDIUM setting**: file size 916KB, dimension is 3497x4950 pixels.

- **HIGH setting**: file size 1.55MB, dimension is 4960x7020 pixels.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
