# Storage management capabilities

The Adobe Admin APIs for Storage Management provide powerful functionality for developers to integrate Adobe's storage management capabilities into their workflows, scripts, and tools. Each capability addresses a specific need for managing content stored in Adobe storage for business.

## Content retention policy for inactive users

The content retention policy governs the assets of inactive (deactivated) users stored in the **individual user folders**. It ensures assets are preserved for a defined retention period and automatically deleted when the period ends. Policies can be applied retroactively and modified (extended, shortened, or expired immediately). Reactivating a user cancels retention, while re-deactivation starts a new retention period.

### Key points

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

## Move Restrictions Policy

The Move Restrictions Policy determines whether users in your organization can move assets into shared projects or folders outside your organization’s storage.

### Key Points

- **Enabled (default):**

  When this policy is enabled, users in your organization can move assets into shared projects or folders outside your organization’s storage.

- **Disabled:**

  When this policy is disabled, users in your organization CANNOT move assets into shared projects or folders outside your organization’s storage.

**Note:**  

- Regardless of the policy’s state, users with Administrator role can move assets into shared projects or folders outside your organization’s storage.
- Regardless of the policy’s state, users outside your organization CANNOT move assets outside your organization’s storage.
