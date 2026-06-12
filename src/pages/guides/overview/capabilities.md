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

## Content Retention Policy for Work-in-Progress (WIP) Content

Admins can create one or more content retention policies to manage the lifecycle of WIP (Work-in-Progress) Content within an organization. WIP content refers to Creative Cloud Projects stored in the Adobe cloud for business.

The Content Retention Policy for Work-in-Progress (WIP) content defines how long Creative Cloud Projects are retained after being marked as complete, before they are permanently deleted.

**Key points:**

- **Configuring retention policies:** Admins can create one or more content retention policies for WIP Content within an organization.
- **Marking a Project as Complete:** A Creative Cloud Project is considered Marked as Complete when it has reached the end of its working lifecycle and is no longer active work. This status is set through an integration with an authorized external system—such as a project management or workflow tool. The external system explicitly signals that the Project has reached lifecycle completion and based on that the Adobe Admin API is invoked to kickstart retention.
- **Policy application and precedence:** When a Project is identified as Complete, the retention period begins based on the Content Retention Policy that is associated with that Project at that time by the Admin. If multiple policies apply to the same Project, the policy with the earliest retention date takes precedence.
- **Retention lifecycle:**

| Stage                    | What happens                                         |
|--------------------------|------------------------------------------------------|
| Project marked complete  | Retention period begins                              |
| Retention period ends    | Project is soft-deleted and moves to Deleted view    |
| 30 days after soft delete| Project is permanently and irrecoverably deleted     |

During the soft-delete window, users may restore the Project and resume work. See **Restoring a Project** below.

- **Restoring a Project:**

  End-users can restore a soft-deleted Project within the 30-day window. On restore:

  - The Project is removed from the Deleted view and becomes active again.
  - The original retention period does not automatically restart.
  - Retention will only re-apply if an admin explicitly re-associates a retention policy with the Project.
  - If the Project is subsequently marked as Complete again by an authorized external system, a new retention period begins anchored to the new completion date.
- **Policy modification:** The retention period of a policy can be extended or shortened. Changes apply to all active Projects governed by the policy, calculated from each Project’s original retention start date.

  **Note:** If a retention period is shortened and a governed Project has already been in retention longer than the new period, that Project will be immediately queued for soft deletion. Admins should audit active Projects before shortening a policy period.
- **Policy deletion:** Deleting a Content Retention Policy for WIP Content immediately stops enforcement for all Projects governed by it. Projects are not deleted because of policy deletion — they remain active until a new policy is associated and triggered.

## Move Assets Policy

The Move Assets Policy determines whether users in your organization can move assets into shared projects or folders outside your organization’s storage.

**Key Points:**

- **Enabled (default):** You can use this default setting to allow users in your organization to move assets into shared projects or folders outside your organization’s storage.
- **Disabled:** You can use this setting to prevent users in your organization from moving assets into shared projects or folders outside your organization’s storage.

**Note:**  

- Regardless of the policy’s state, users with Administrator role can move assets into shared projects or folders outside your organization’s storage.
- Regardless of the policy’s state, users outside your organization CANNOT move assets outside your organization’s storage.
