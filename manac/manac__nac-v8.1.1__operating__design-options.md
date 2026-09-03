<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/operating/design-options -->

# Design Options

All of the web messages include common elements such as a header image and color and links to an Acceptable Use Policy and FAQ. These elements can be edited from the Policy Manager by navigating to “Policy Manager > Web UI Menu > Design Options”.

Any elements changed on the "Design Options" page will affect all end user web messages with those elements.

## [General Settings](/docs/manac/nac-v8.1.1/operating/design-options#general-settings)

- To make design changes, press "Save" in the lower right corner.
- After clicking save, preview by pressing "View Web Message".

## [Color Choices](/docs/manac/nac-v8.1.1/operating/design-options#color-choices)

Design Options offers color customization in seven different categories:

- **Headers, Borders, and Buttons**-- Modifies the color of circles behind list numbers, the heading tags located beneath your logo, and the border of the notification button.
- **Body Background**-- Modifies the main background color beneath the logo.
- **Body Text**-- Modifies the main text color beneath the headings.
- **Notification Box Background**-- Modifies the color of the notification boxes backgrounds'.
- **Notification Box Text**-- Modifies the color of the text within the notification boxes.
- **Button Text**-- Modifies the color of text within buttons.
- **Header Background**-- Modifies the color that appears behind the logo.

## [Helpful Tips](/docs/manac/nac-v8.1.1/operating/design-options#helpful-tips)

- Colors within unspecified and grouped areas you wish to modify need to be manually edited on the raw JSP or CSS files.
- An overview of color hex codes can be found here: <http://www.w3schools.com/html/html_colors.asp>.
- A color picker can be found here: <https://www.webpagefx.com/web-design/color-picker/>.
- If there are multiple buttons, then one or more of the buttons may reverse the typical behavior of the "Button Text" and "Headers and Boarders" options so that the "Button Text" entry is the color of a button's background and the "Headers and Boarders" color is that of a button's text.

## [Header Logo](/docs/manac/nac-v8.1.1/operating/design-options#header-logo)

- OPSWAT recommends using a transparent PNG file of the organization logo for the header background.
- If a transparent PNG file of the organization logo is not readily available, the following tutorials demonstrate how to create a transparent logo:

  - Photoshop (commercial): [http://youtube.com/watch?v=jzOxYxj-N-c](https://youtu.be/jzOxYxj-N-c)
  - GIMP (free): <https://youtu.be/nmBvCAp1Lgs>

## [Organization Name/Footer](/docs/manac/nac-v8.1.1/operating/design-options#organization-namefooter)

- The Organization Name appears in the footer of most notifications. It's often used to display organizations' copyright.
- For multiline organization names, enter "\a" without parentheses before each new line.
- In some instances, a special character appears in front of the copyright symbol. To solve this problem, enter "\00a9" without parentheses in place of the copyright symbol itself.
- Note that different notifications have different colored backgrounds. To ensure the best contrast, preview your Body Text color choices in a variety of notifications by navigating to "Policy Manager > Web UI Menu > Web Messages". Select a web message from the Web Messages scroll box and press "Preview Web Message". Repeat for several different messages.
