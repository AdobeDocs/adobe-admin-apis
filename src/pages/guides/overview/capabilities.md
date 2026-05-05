# Storage management capabilities

The Adobe Admin APIs for Storage Management provide powerful functionality for developers to integrate Adobe's storage management capabilities into their workflows, scripts, and tools. Each capability addresses a specific need for managing content stored in Adobe storage for business.

## Content retention policy for inactive users

The content retention policy governs the assets of inactive (deactivated) users stored in the **individual user folders**. It ensures assets are preserved for a defined retention period and automatically deleted when the period ends. Policies can be applied retroactively and modified (extended, shortened, or expired immediately). Reactivating a user cancels retention, while re-deactivation starts a new retention period.

**Key points:**

- **Policy application:** Assets of deactivated users enter the retained state; retention starts from the deactivation date.
- **Expiry and deletion:** Assets are permanently deleted when the retention period ends. The minimum retention period is 30 days.
- **Retroactive application:** Policies can apply to users deactivated before policy creation; retention starts from the original deactivation date.
- **Reactivation:** Reactivating a user cancels retention; re-deactivation starts a new retention period from the new deactivation date.
- **Policy modification:** Retention period can be extended or shortened. If the shortened period is less than 30 days, it is automatically set to 30 days.
- **Policy deletion:** Ends retention; assets remain inactive but are not deleted.

**Assets deleted:** Synced assets of an inactive user's **individual user folder**, including:

- Creative Cloud files
- Libraries stored in the cloud
- Cloud documents (Photoshop, Illustrator, and XD documents)
- Adobe Express files (only applicable to files that are created after 08/16/2023)

**Note:** Assets not included:

- Published documents
- Acrobat Sign agreements
- Adobe Express social posts
- Mobile creations
- Lightroom files
- Behance assets
- Portfolio assets

## Move Assets Policy

The Move Assets Policy determines whether users in your organization can move assets into shared projects or folders outside your organization’s storage.

**Key Points:**

- **Enabled (default):** You can use this default setting to allow users in your organization to move assets into shared projects or folders outside your organization’s storage.
- **Disabled:** You can use this setting to prevent users in your organization from moving assets into shared projects or folders outside your organization’s storage.

**Note:**  

- Regardless of the policy’s state, users with Administrator role can move assets into shared projects or folders outside your organization’s storage.
- Regardless of the policy’s state, users outside your organization CANNOT move assets outside your organization’s storage.

## Content Retention Policy for Work-in-Progress (WIP) Content

The Content Retention Policy for Work-in-Progress (WIP) content defines how long Creative Cloud Projects are retained after being marked as complete, before they are permanently deleted.

**Key points:**

- **Configuring retention policies:** Admins can create one or more Content Retention Policies for WIP Content within an organization.
- **Marking a Project as Complete:** A Creative Cloud Project is considered Marked as Complete when it has reached the end of its working lifecycle and is no longer active work. This status is set through an integration with an external system—such as a project management or workflow tool—using Adobe Admin APIs. The external system explicitly signals that the Project has reached lifecycle completion.
- **Policy application and precedence:** When a Project is marked as Complete, retention begins based on the applied WIP Content Retention Policy. If multiple policies apply to the same Project, the policy with the earliest retention date takes precedence.
- **Retention lifecycle:** At the end of the retention period, the Project is soft deleted and moved to the Deleted view. After 30 days of being soft deleted, the Project is permanently deleted from the system.
  - During the soft-deleted period, users may restore and continue using the Project. Restoring a Project removes it from retention and does not reset retention.
  - Retention is re-applied only if an admin explicitly associates a retention policy with the Project. If the Project is subsequently marked as Complete again through an authorized system, a new retention period begins, anchored to the new completion date.
- **Policy modification:** The retention period of a policy can be extended or shortened. Changes apply to all active Projects governed by the policy, based on their original retention start dates.
- **Policy deletion:** Deleting a Content Retention Policy for WIP content immediately stops enforcement. Projects previously governed by the policy will not be deleted because the policy governing them has been deleted.

## Content Retention Policy for Inactive Content

The Content Retention Policy for Inactive Content defines how long end-user content is retained after it becomes inactive—based on lack of modification—before it is permanently deleted, independent of user status.

**Key points:**

- **Determining inactivity:** Content is considered inactive when it has not been modified for a configured inactivity threshold. Inactivity is evaluated based on the content’s Last Modified Date, regardless of whether the owning user is active or inactive or the asset is accessed/read.
- **Retention lifecycle:** When content crosses the configured inactivity threshold, the content is soft deleted and moved to the Deleted view. After 30 days of being soft deleted, the content is permanently deleted from the system.
  - Restoring content during the soft-deleted period cancel retentions and resets the inactivity evaluation.
  - An explicit content modification also resets inactivity and stops retention enforcement.
- **Policy modification:** The inactivity threshold of a policy may be extended or shortened. Changes apply to all content governed by the policy, based on their respective last modified dates.
- **Policy deletion:** Deleting a Content Retention Policy for Inactive Content immediately stops enforcement. Content previously governed by the policy remains available and is not deleted because of policy deletion.
