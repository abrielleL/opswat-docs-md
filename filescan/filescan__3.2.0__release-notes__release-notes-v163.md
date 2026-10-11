<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v163 -->

# Release Notes for v1.63

View as Markdown Ask ChatGPT about this page Ask Claude about this page

---

### [Date: 28 November, 2022](/docs/filescan/3.2.0/release-notes/release-notes-v163#date-28-november-2022)

Fixed:

- remove "null"-byte padding from Javascript, which was throwing off the emulator
- fsBroker retry attempts would only try one time (verifyAppServersAreAvailableRetryMax) breaking automatic service restarts on slow machines

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
