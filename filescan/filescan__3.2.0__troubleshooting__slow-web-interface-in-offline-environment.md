<!-- source: https://www.opswat.com/docs/filescan/3.2.0/troubleshooting/slow-web-interface-in-offline-environment -->

# Slow web interface in offline environment

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Opening the Aether web interface might be slower than expected in an offline environment.

The underlying issue is that the web UI references the following external resources:

https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css
https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap

If the offline environment is configured correctly to immediately drop external requests, then everything works as expected.

If the offline network setup is not fully consistent, and these external requests go to a gateway/router node where they are not dropped, then a timeout will occur on the browser side (perhaps after waiting 30-40 seconds).

The recommended solution is modifying `/home/sandbox/sandbox/webservice-front/index.html` to disable these external references.

Please open that file on the sandbox server using any text editor (e.g. nano) and locate the following section:

index.htmlCopy<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css" />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap" rel="stylesheet">

Then **comment out** these 2 lines using `<!--` and `-->`. This should be the end result:

index.htmlCopy<!-- <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css" /> -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<!-- <link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap" rel="stylesheet"> -->

Please **save the modified index.html file** and open the Sandbox UI again in your browser!

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
