<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/secure-web-forms -->

# Secure Web Forms

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

The **Secure Web Forms** feature allows Administrators to design custom questionnaires that users must complete when uploading files. These questionnaires help collect important metadata that can later be used for **routing**, **compliance**, **security workflows**, and **supervisor approvals**. This guide walks through how the feature works end-to-end.

## [1. Typical Workflow](/docs/mdmft/v3.11.5/configuration/secure-web-forms#1-typical-workflow)

1. Admin defines questionnaire under **Settings > File Settings > Secure Web Forms** and publishes it.
2. (Optional) Admin creates **Sections** with dependent questions that appear conditionally based on the user's answers to root-level questions.
3. (Optional) Admin defines transfer policies that may refer to destination selections (single or multiple choice options) to drive routing and filtering.
4. User starts a file upload; if questionnaire was published by Admin, the questionnaire step appears and must be completed by the User (required questions are enforced).
5. Supervisor (if supervision is enabled) opens the approval modal and sees all captured answers — including answers to dependent questions — before making a decision on the approval.
6. If MFT-to-MFT is configured and policies match, each file plus its questionnaire data is forwarded; destination MFT persists the data and uses it for its own workflows (including supervision and transfer policies).

## [2. Roles At A Glance](/docs/mdmft/v3.11.5/configuration/secure-web-forms#2-roles-at-a-glance)

- **Administrator**: Creates, edits, publishes, deletes questionnaire; creates Sections with dependent questions; maps options to Sections; defines transfer policies (MFT-to-MFT routing).
- **User** (Uploader): Answers visible questions during file upload. Dependent questions appear dynamically based on selected answers.
- **Supervisor**: Reviews all submitted questionnaire answers — including dependent question answers — in the approval modal to make informed approval decisions.

## [3. Designing the Questionnaire](/docs/mdmft/v3.11.5/configuration/secure-web-forms#3-designing-the-questionnaire)

Navigating to **Settings > File Settings > Upload Questions** opens the upload questions builder interface. If no questionnaire is published, you see an empty builder ready for creation. If a questionnaire exists, you can view or modify it.

Questionnaire builder (empty)

To create a new questionnaire, fill in the questionnaire name and add questions as described below.

### [3.1 Adding Questions](/docs/mdmft/v3.11.5/configuration/secure-web-forms#31-adding-questions)

Click **Add Question** to create a new question then configure its attributes:

1. **Question**: Full text shown to users.
2. **Question Type**: Text, Single choice, Multiple choice.
3. **Question ID**: Uniquely identifies the question within the questionnaire. Can be referenced by transfer policies for routing.
4. **Column Title**: Short label used where space is limited.
5. **Answer Required**: If true, user must answer to proceed.
6. **Show Question** (hide or make it visible): Controls whether question appears or not. Hidden questions are never shown, even if 'required' (useful for drafting questions without publishing or simply hiding them temporarily).

Question attributes

#### [3.2 Selecting the question type](/docs/mdmft/v3.11.5/configuration/secure-web-forms#32-selecting-the-question-type)

#### [3.2.1 Text Questions](/docs/mdmft/v3.11.5/configuration/secure-web-forms#321-text-questions)

Choose **Text** as the Question Type to create a free-form text or integer input question. Specify **Required Format**: Text or Integer.

Text question

#### [3.2.2 Single and Multiple Choice Questions](/docs/mdmft/v3.11.5/configuration/secure-web-forms#322-single-and-multiple-choice-questions)

Choose **Single Choice** or **Multiple Choice** as the Question Type to create selection-based questions. Define a list of answers, each with:

- **Answer**: Full text shown to users.
- **Answer ID**: Unique identifier for the answer within the question. These identifiers can be used to define transfer policies (these are attributes that can be filtered for). See more details in [6.1 Transfer Policies & Routing](/docs/mdmft/v3.11.5/configuration/secure-web-forms#61-transfer-policies--routing).

Single choice question

Multiple choice question

### [3.3 Sections (Dependent Questions)](/docs/mdmft/v3.11.5/configuration/secure-web-forms#33-sections-dependent-questions)

Sections allow you to create groups of dependent questions that only appear when a user selects a specific answer to a **Single Choice** question. This enables dynamic, branching questionnaires where follow-up questions are shown conditionally.

Info

**Constraints:**

- Section mapping is only available for **Single Choice** questions. Text and Multiple Choice questions do not support dependent questions.
- The maximum nesting depth is **2 levels**: a root question can map to a Section, and a Single Choice question inside that Section can map to another Section, but no further nesting is allowed.
#### [3.3.1 Creating a Section](/docs/mdmft/v3.11.5/configuration/secure-web-forms#331-creating-a-section)

At the bottom of the questionnaire builder, click **Create New Section** (next to the Add Question button) to create a new Section. A new Section is created with a default name (e.g., "Section 1") and appears below the root questions, separated by a divider. Click on the Section name to rename it.

#### [3.3.2 Adding Questions to a Section](/docs/mdmft/v3.11.5/configuration/secure-web-forms#332-adding-questions-to-a-section)

- Inside a Section, click **Add Question to Section** to add a dependent question.
- Configure the dependent question the same way as a root-level question (question text, type, ID, required, visible, etc.).
- Questions within a Section can be reordered via drag-and-drop.

#### [3.3.3 Mapping an Answer to a Section](/docs/mdmft/v3.11.5/configuration/secure-web-forms#333-mapping-an-answer-to-a-section)

To make a Section's questions appear conditionally based on a user's answer:

- Open a root-level **Single Choice** question for editing.
- Each answer displays a **Select section** dropdown on the right side.
- Select the Section that should appear when the user chooses that option.

*An option can only be mapped to one Section at a time. Multiple options can map to the same Section if the same follow-up questions should appear for different choices.*

#### [3.3.4 Deleting a Section](/docs/mdmft/v3.11.5/configuration/secure-web-forms#334-deleting-a-section)

To delete a Section, click the **Delete section** button on the Section header. This removes the Section and all its dependent questions. Any option-to-Section mappings pointing to the deleted Section are also cleared.

### [3.4 Publishing & Validation](/docs/mdmft/v3.11.5/configuration/secure-web-forms#34-publishing--validation)

Once complete, click **Publish** to make the questionnaire active.

- Publishing fails when required conditions (title, answer requirements, IDs) aren’t met.
- Successful publishing instantly makes questionnaire available for Users.
- Editing requires republishing for changes to take effect.

#### [3.5 Editing, reordering and deleting questions](/docs/mdmft/v3.11.5/configuration/secure-web-forms#35-editing-reordering-and-deleting-questions)

To open a question for editing, click on the top bar of the question card.

To reorder questions, use the drag handle on the top of the question card.

To delete a question, open it for editing and click the **Delete** button at the bottom-right.

To apply any of the changes, click **Update** in the top-right, which will also republish the questionnaire with the changes.

## [4. Answering the Questionnaire (User Upload Step)](/docs/mdmft/v3.11.5/configuration/secure-web-forms#4-answering-the-questionnaire-user-upload-step)

If a published questionnaire with visible questions exists, users see the questionnaire step during file upload.

Check out [Uploading files](/docs/mdmft/v3.11.5/operating/upload-files#upload-questions) on how it works in the upload process.

## [5. Supervisor approval](/docs/mdmft/v3.11.5/configuration/secure-web-forms#5-supervisor-approval)

When supervisor approval is set up, the approval modal displays all captured answers exactly as submitted — **including answers to dependent questions**.

Purpose: User to provide context and/or reasoning for uploading the file(s). Supervisor to use additional information for approval decision.

Check out [Supervisor Approval](/docs/mdmft/v3.11.5/operating/supervisor-approval) for more information.

## [6. MFT-to-MFT](/docs/mdmft/v3.11.5/configuration/secure-web-forms#6-mft-to-mft)

If the source MFT instance forwards files to destination MFT(s):

- Each forwarded file carries its questionnaire data, including all answers to dependent questions.
- Destination MFT persists the received questionnaire alongside the file record.
- If supervision active on destination, the same approval interface (with answers) applies.

### [6.1 Transfer Policies & Routing](/docs/mdmft/v3.11.5/configuration/secure-web-forms#61-transfer-policies--routing)

Policies can filter based on questionnaire answers. Check out [Transfer Policies](/docs/mdmft/v3.11.5/configuration/transfer-policies#upload-questions) for more information on how to set them up.

## [7. Primary use cases](/docs/mdmft/v3.11.5/configuration/secure-web-forms#7-primary-use-cases)

### [7.1 Destination Selection](/docs/mdmft/v3.11.5/configuration/secure-web-forms#71-destination-selection)

To allow users to choose where their files will be forwarded:

1. Add a single (for single destination) or multiple choice (for multiple destinations) question labeled clearly (e.g., "Select Destination" or "Forward To location").
2. Populate answers with each MFT destination you support. Display text should be meaningful to users; answer IDs can be technical (used internally for mapping).
3. Link transfer policies and destination mappings to these answer IDs (see Transfer Policies section).
4. Publish the questionnaire.

Expected outcome:

1. Users can define where their file should be routed to at the time of upload.
2. File will be automatically routed based on the transfer policy settings.

### [7.2 Compliance & Classification Metadata Collection](/docs/mdmft/v3.11.5/configuration/secure-web-forms#72-compliance--classification-metadata-collection)

Many organizations require users to classify files before sharing or transferring them. Upload Questions enable Admins to enforce this consistently.

Example questions:

- “What is the data classification level?” (Public / Internal / Confidential / Restricted)
- “Does this file contain personal data?” (Yes / No)
- “Business justification for uploading this file” (Text)

How it helps:

- Ensures every upload includes required compliance metadata.
- Supports automated policies (e.g., block or route differently based on sensitivity).
- Gives Supervisors more context during approval.
- Creates an auditable trail of reasoning and classification.

Expected outcome: organizations gain tighter governance, consistent classification, and better auditability for file uploads.
