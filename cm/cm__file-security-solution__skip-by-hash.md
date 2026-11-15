<!-- source: https://www.opswat.com/docs/cm/file-security-solution/skip-by-hash -->

# Skip by Hash

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Skip By Hash lets you centrally manage file-hash rules across your entire MetaDefender Core fleet from My OPSWAT Central Management.

You create hash lists, assign them to Core policies, and every Core instance governed by those policies automatically receives and applies the rules. As you update entries, changes sync incrementally, no manual push required.

## [Before You Begin](/docs/cm/file-security-solution/skip-by-hash#before-you-begin)

| Requirement | Detail |
| --- | --- |
| **Supported products** | MetaDefender Core only |
| **Permissions** | Your role must have the **Skip By Hash** permission to use this feature |
| **Assignment required** | A hash list has no effect until it is assigned to at least one Core policy. See [Assign Hash List to Policy](/docs/cm/file-security-solution/skip-by-hash#assign-hash-list-to-policy) |
| **Core-side setting** | Whether a Core instance accepts skip-hash settings from My OPSWAT Central Management is controlled on the Core instance itself. This setting cannot be viewed or changed from My OPSWAT Central Management |
| **Upgrading from earlier versions** | Group-based assignments are not migrated. After upgrading, re-assign each list to the appropriate policy |
| **Deployment models** | Supported on Cloud, Windows (MSI), Linux (RPM), OVA, and High Availability, including air-gapped environments |
| **Hash actions available** | - Blocklist: File is denied immediately, no scan performed - Allowlist: File is allowed immediately, scanning is skipped - Skip Engines: File is scanned, but specific AV engines you choose are excluded |

## [Step-by-Step Workflow](/docs/cm/file-security-solution/skip-by-hash#step-by-step-workflow)

1. [Create a Hash List](/docs/cm/file-security-solution/skip-by-hash#create-a-hash-list)
2. [Assign Hash List to Policy](/docs/cm/file-security-solution/skip-by-hash#assign-hash-list-to-policy)
3. [Manage Hash List Entries](/docs/cm/file-security-solution/skip-by-hash#manage-hash-list-entries)

## [Create a Hash List](/docs/cm/file-security-solution/skip-by-hash#create-a-hash-list)

**Step 1**: Navigate to **File Security → Skip By Hash**

1. Click **Create New List** on the Skip By Hash page
2. Enter a Name and Description
3. The new list starts empty and unassigned.

**Step 2**: Under Hashes tab, choose **Add Hash** or **Import Hash**

| Actions | Details |
| --- | --- |
| Add Hash | - Select action - Enter Hash value (MD5, SHA1, SHA256, or SHA512, any case) - Add an optional Description - If the action is Skip Engines, also choose which engines to exclude - (Optional) Choose an **Expiration Date**    - No expiration (default): The entry stays in place until you delete it   - 1 day, 3 days, 7 days, 14 days, 30 days: The entry expires that long after you click Add   - Custom: Enter a whole number (minimum 1) and choose Days or Hours   Note MetaDefender Core **version 5.24.0 or later** shows the expiration date on centrally-managed entries. |
| Import Hash | - Select action - Upload a CSV (up to 500 MB, 10,000+ entries supported)   Note Any rows with errors are skipped, you'll see which ones failed so you can fix and re-import. |

Note If the hash already exists in the list, you'll be asked to confirm overwriting the existing entry.

## [Assign Hash List to Policy](/docs/cm/file-security-solution/skip-by-hash#assign-hash-list-to-policy)

A hash list only takes effect once assigned to a policy.

**Step 1:** Navigate to **Inventory → Skip By Hash.** Open the Assignments tab.

| Actions | How |
| --- | --- |
| Assign hash list to a policy | Click **Assign Policy** → select one or more Core policies  Note *A policy can only carry one list. Assigning a list to a policy that already has a different one replaces it silently, without warning.* |
| Remove an assignment | Click the remove action on the assignment row |

**Step 2**: Verify hash list has been assigned to policy

1. Navigate to **File Security > Policies**
2. Select the policy that you've assign hash list to
3. Go to Skip By Hash tab
4. Verify the hash list appears under this tab

Once a hash list is assigned to a policy, all changes sync automatically to every connected Core instance, no manual push needed. Instances that are offline will pick up the latest updates as soon as they reconnect.

## [Manage Hash List Entries](/docs/cm/file-security-solution/skip-by-hash#manage-hash-list-entries)

Open any hash list to view, edit, or delete entries.

| Actions | Details |
| --- | --- |
| Edit | You can change the action, description, and engines, but the hash value itself is read-only. To change a hash, delete and re-add. |
| Delete | Removes the entry from the list and propagates the removal to all affected Core instances. |
| Search and filter | - Search by hash or description (case-insensitive substring match). - Filter by action type (Blocklist / Allowlist / Skip Engines) |

## [What Happens When an Entry Expires?](/docs/cm/file-security-solution/skip-by-hash#what-happens-when-an-entry-expires)

1. **My OPSWAT Central Management removes the entry.** This usually happens within about a minute of the expiration time.
2. **Each Core instance removes the hash on its next sync.** Until then, the Core instance keeps applying the entry. Offline instances pick up the removal when they reconnect.
