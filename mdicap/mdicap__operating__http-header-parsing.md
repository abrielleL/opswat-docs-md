<!-- source: https://www.opswat.com/docs/mdicap/operating/http-header-parsing -->

# HTTP Header Parsing

View as Markdown Ask ChatGPT about this page Ask Claude about this page

In this page, we document HTTP header that MetaDefender ICAP Server is using for logging and scanning.

## [Flowchart](/docs/mdicap/operating/http-header-parsing#flowchart)

## [Details](/docs/mdicap/operating/http-header-parsing#details)

The steps below detail how MetaDefender ICAP Server parses HTTP information from content-disposition.

1. Check if **filename*** parameter is present

   1. Get the value of the parameter
   2. Look for the last " **'** " character in the value (see [Grammar of filename*'s value](https://tools.ietf.org/html/rfc5987#section-3.2))

      1. If no " **'** " character is present then the format considered to be invalid (no filename or extension is returned)
      2. If " **'** " is found then the text after it is considered as the filename (not decoded)
   3. Extension is considered to be the substring after the last "**.**" in the filename
2. If **filename*** is not present then look for **filename**

   1. Get the value of the parameter
   2. Check if the first char is a " **"** " (quote mark)

      1. If we start with a quote mark then the filename will be the substring between the opening and closing quote mark (if no closing quote mark is present we consider it as an invalid and no filename or extension is returned)
      2. Otherwise the whole value is considered as the filename
   3. Extension is considered to be the substring after the last "**.**" in the filename
3. If none of the parameters are present, then give it a try with **name**

   1. If **name** parameter is present then the filename will be the parameter's value (between quote mark) and the extension will be empty
4. If none of the above succeeded or the extension contains special characters then the filename and extension parsing is failed in this step.

### [Good examples](/docs/mdicap/operating/http-header-parsing#good-examples)

The following table includes good Content-Disposition examples.

| Parameter format example | Filename | Extension |
| --- | --- | --- |
| filename=*utf8''test%20test.a.b.c | test%20test.a.b.c | c |
| filename="test.txt" | test.txt | txt |
| filename=test.txt | test.txt | txt |
| filename="test a.txt"; filename*=utf8'en'test%20a.txt | test%20a.txt | txt |
| filename = test.txt | test.txt | txt |
| name="test" | test |  |

### [Bad examples](/docs/mdicap/operating/http-header-parsing#bad-examples)

The following table includes bad Content-Disposition examples.

| Parameter format examle | Error |
| --- | --- |
| filename=*utf8test.txt | No " **'** " char |
| filename="test.txt | No closing quote mark |
| filename=test.t?x | Special character in extension |
| name=test | No quote marks |

### [Parse from URL](/docs/mdicap/operating/http-header-parsing#parse-from-url)

Parsing is made using the URL via the GET HTTP method. This method receives the text after the last "/" in the URL path until the first "?" character or until the first "#" character if "?" is not present, or until the end of the URL is neither is present.

The extension is considered to be the substring after the last "." character. If the extension is empty or contains special characters, it is considered a failure.

#### [Good examples](/docs/mdicap/operating/http-header-parsing#good-examples)

The following table includes good URL examples.

| URL | Filename | Extension |
| --- | --- | --- |
| /a/b/c/test.txt | test.txt | txt |
| /test.a.b | test.a.b | b |
| /a/test.php?get=x.txt | test.php | php |
| /a/test.php#abc | test.php | php |
| /a/b/test.php?abc&d=b&g#hjk | test.php | php |

#### [Bad examples](/docs/mdicap/operating/http-header-parsing#bad-examples)

The following table includes bad URL examples.

| URL | Error |
| --- | --- |
| /test | No extension |
| /test/? | Empty part between the last "/" and "?" |

## [Additional Details](/docs/mdicap/operating/http-header-parsing#additional-details)

The following parameters are handled case insensitively: filename, filename*. It means that FILENAME, FiLeNaMe* etc. will be also found.

Optional whitespaces are handled in the Content-Disposition header. So both "filename=test.txt" and "filename = test.txt" is supported now.
