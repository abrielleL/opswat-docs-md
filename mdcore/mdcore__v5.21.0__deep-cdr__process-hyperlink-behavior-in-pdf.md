<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/deep-cdr/process-hyperlink-behavior-in-pdf -->

# Process Hyperlink Behavior in PDF

## [Overview](/docs/mdcore/v5.21.0/deep-cdr/process-hyperlink-behavior-in-pdf#overview)

To configure the **Process Hyperlink Behavior**, please check **Process Hyperlink Behavior** in **PDF Configuration**.

## [**Options for Process Hyperlink Behavior**](/docs/mdcore/v5.21.0/deep-cdr/process-hyperlink-behavior-in-pdf#options-for-process-hyperlink-behavior)

- **Do nothing:** Keep hyperlinks as is.

- **Remove hyperlink annotations only**: Remove hyperlink annotations. Text links (hyperlinks but written as texts in the content) may still be highlighted by PDF readers.

- **Remove hyperlink annotations and text links**: Remove hyperlink annotations and replace text links with null links (`http://#`). Text links will not be clickable.

- **Remove hyperlink annotations and prevent clickable links auto-turning**: Prevent the clickable links auto-turning feature of readers by changing "." to "[.]" in text that is in hyperlink format.

- **Remove hyperlink annotations and leave them in text form**: Remove hyperlink annotations and leave them in text form.

- **Add hyperlink prefix**: Prefix hyperlinks to allow redirecting them to a hyperlink verification or processing service.

- **Return list of hyperlinks**: Do nothing with hyperlinks, but list them in the returned message.
