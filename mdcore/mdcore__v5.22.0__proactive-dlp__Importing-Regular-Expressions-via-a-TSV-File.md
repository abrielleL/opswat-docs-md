<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/proactive-dlp/Importing-Regular-Expressions-via-a-TSV-File -->

# Importing Regular Expressions via a TSV File

In this section, we will guide you through the process of importing regular expressions using a TSV (Tab-Separated Values) file and integrating them into the PDLP. We'll cover the basics of preparing your TSV file for regular expressions and the steps to import them effectively into the PDLP.

## [Structure of the TSV File](/docs/mdcore/v5.22.0/proactive-dlp/Importing-Regular-Expressions-via-a-TSV-File#structure-of-the-tsv-file)

- Only UTF-8 file encoding is supported.
- Each regular expression should be represented on a single line. The format of each line could be:

  - <NAME> <TAB> <RegEX>
  - <RegEX>
- NAME: Should not exceed 64 characters and may contain alphanumeric characters and underscores ([a-zA-Z0-9_]).

  - If the NAME is not provided, a default will be generated in the format: CUSTOM_FILE_REGEX_<line number>.
- SEPARATOR: A TAB character will be used
- REGULAR EXPRESSION: Everything following the TAB character is treated as the regular expression. If the NAME and TAB are not present, the entire line will be considered as the regular expression.

## [Enabling Importing Regular Expression](/docs/mdcore/v5.22.0/proactive-dlp/Importing-Regular-Expressions-via-a-TSV-File#enabling-importing-regular-expression)

Policies > Workflow rules > "Workflow name" > Proactive DLP > Check for regular expressions > Load regular expressions from file

Let's discuss each section and provide an example:

- **Regular expression file:** Path to TSV formatted regular expression file

Important Notice

- In the event of an error, non-compliance with the specified format, or incorrect regex, the engine will fail. Please consult the engine logs to determine if there are any errors in the file you provided.

Limitations

These are the current limitations related to TSV custom regex feature.

- Max TSV file size: 500 * 1024 byte (~500 Kb)
- Max TSV line number: 255 Line
- Max TSV Line characters: 300 character (Name length + tabulator + regex length)
- Max regex Name length: 64 character

Samples

Below is an example of a regular expressions file you can use

Email ([a-zA-Z0-9_\.-]+)@([\da-zA-Z\.-]+)\.([a-zA-Z\.]{2,6})
URL https?:\/\/(?:www\.)?([-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,6}\b)*(\/[\/\d\w\.-]*)*(?:[\?])*(.+)*
US_Address \d{1,5}(\s[\w.,]*){1,6},\s[A-Z]{2}\s\d{5}\b
California_Driver_License California: \b[A-Za-z]{1}[0-9]{7}\b
Date_of_Birth (Date of birth:|Birthday:)\s+(?:19\d{2}|20[01][0-9]|2020)[-/.](?:0[1-9]|1[012])[-/.](?:0[1-9]|[12][0-9]|3[01])\b
Full name:\s[A-Z][a-z]+(?:[ \t]*[A-Z]?[a-z]+)?[ \t]*[A-Z][a-z]+\b
(Passport Number|Passport No|Passport #|Passport#|PassportID|Passportno|passportnumber)\W*\d{9}\b
