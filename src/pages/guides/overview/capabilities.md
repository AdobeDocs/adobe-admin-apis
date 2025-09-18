# Administrative Capabilities

Adobe Admin APIs provide enterprise organizations with programmatic control over administrative tasks in the Adobe Admin Console, enabling them to integrate Adobe's administrative capabilities into their workflows, scripts, and tools to automate administrative processes. Each capability addresses a specific need for managing organizational assets stored in Adobe Cloud Storage.

## Content Retention Policy for Inactive Users

The Content Retention Policy governs the assets of inactive (deactivated) users stored in the **Individual User Folders**, ensuring they are preserved for a set retention period and automatically deleted when the period ends. Policies can apply retroactively and be modified (extended, shortened, or expired immediately). Reactivating a user cancels retention, while re-deactivation starts a new retention period.

### Key Points

- **Policy Application:** Assets of deactivated users enter the retained state; retention starts from the deactivation date. [Learn more](#)
- **Expiry & Deletion:** Assets are permanently deleted when the retention period ends. The minimum retention period is 30 days. [Details](#)
- **Retroactive Application:** Policies can apply to users deactivated before policy creation; retention starts from the original deactivation date. [More info](#)
- **Reactivation:** Reactivating a user cancels retention; re-deactivation starts a new retention period from the new deactivation date. [See how](#)
- **Policy Modification:** Retention period can be extended or shortened. If the shortened period is less than 30 days, it is automatically set to 30 days. [Policy settings](#)
- **Policy Deletion:** Ends retention; assets remain inactive but are not deleted. [Policy deletion guide](#)

#### Assets deleted: Synced assets of an Inactive user's **individual user folder**, including:

- Creative Cloud files [Reference](#)
- Libraries stored in the cloud [Reference](#)
- Cloud documents (**Photoshop**, **Illustrator**, and **XD** documents) [Reference](#)
- **Adobe Express** files (Only applicable to files that are created after 08/16/2023) [Reference](#)

> ![Dummy image for assets deleted](#)

**Note:** Assets not included:

- Published documents [Reference](#)
- Acrobat Sign agreements [Reference](#)
- **Adobe Express** social posts [Reference](#)
- Mobile creations [Reference](#)
- Lightroom files [Reference](#)
- Behance assets [Reference](#)
- Portfolio assets [Reference](#)
