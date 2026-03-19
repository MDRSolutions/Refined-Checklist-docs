# Refined Checklist

**MDR Solutions - Version 1.0.2**

The **Refined Checklist** extension is a lightweight, highly configurable way to add checklists, "Definition of Done," or task-tracking directly into your Azure DevOps work item forms. It supports custom titles, reorderable items, and "Not Applicable" (N/A) status tracking, making it an essential tool for maintaining high standards and consistency across your projects.

---

## Key Features

-   **Configurable Templates:** Define unique checklist items for each Work Item Type (e.g., User Story, Bug, Feature).
-   **Custom Titles:** Label your sections as "Definition of Done," "Acceptance Criteria," or whatever fits your team's workflow.
-   **Intelligent Progress Tracking:** Monitor completion with a dynamic progress bar that turns green upon 100% completion.
-   **Reorderable Items:** Organize your checklist tasks in the exact sequence they should be performed.
-   **N/A Support:** Mark items as "Not Applicable" (N/A) to handle edge cases without affecting your 100% completion goal.
-   **Accountability:** Each check (or N/A) captures the user's name and a timestamp, helping teams stay aligned.

---

## 🛠️ Setup and Configuration

### 1. Installation

1.  **Azure DevOps Services (Cloud):** Search for "Refined Checklist" by **MDR Solutions** in the Visual Studio Marketplace and click **Get it free**. Select your organization to install.
2.  **Azure DevOps Server (On-Premise):** Download the `.vsix` package from the Marketplace, navigate to your Azure DevOps Server's local extension management page (`http://[server]:[port]/_gallery/manage`), and click **Upload Extension**.

---

### 2. Form Layout Configuration

To see the checklist on your work items, you must add the control to your work item form layout.

#### A. Inherited Process Model (Recommended)
1.  Navigate to **Organization Settings** > **Boards** > **Process**.
2.  Select your inherited process and choose a **Work Item Type** (e.g., *User Story*).
3.  Choose the **Layout** tab.
4.  Decide where you want the checklist (a new group in an existing page is usually best).
5.  Click **Add a group** or use an existing one, then click **Add a control**.
6.  Search for **Checklist** (provided by mdr-solutions) and click **Add Control**.

#### B. XML Process Model (On-Premise)
1.  Export the Work Item Type (WIT) definition XML file using `witadmin`.
2.  Locate the `<WebLayout>` section.
3.  Register the extension in the `<Extensions>` block:
    ```xml
    <Extensions>
        <Extension Id="mdr-solutions.refined-checklist" />
    </Extensions>
    ```
4.  Add the checklist group to a `<Section>` or `<Group>` of your choice:
    ```xml
    <Group Id="ChecklistGroup">
        <Control ContributionId="mdr-solutions.refined-checklist.checklist-group" />
    </Group>
    ```
5.  Import the updated XML back into your project collection.

---

### 3. Template Configuration

Once the control is on the form, you need to define what items should appear:

1.  Navigate to your **Project Settings**.
2.  In the left sidebar, under the **Extensions** (or General) category, click **Checklist Configuration**.
3.  Select the **Work Item Type** you wish to configure.
4.  Set a **Section Title** (e.g., "Definition of Done").
5.  Add your checklist items. Use the **Up/Down** arrows to reorder them.
6.  Click **Save Configuration**.

---

## Documentation

For more information and support, visit the [Refined Checklist GitHub repository](https://github.com/MDRSolutions/Refined-Checklist-docs).

## Feedback and Bug Reports

If you encounter any bugs, have questions, or want to suggest a feature:
-   **Issues:** Please open a [new issue](https://github.com/MDRSolutions/Refined-Checklist-docs/issues).
-   **Discussions:** Feel free to start a discussion for feedback or general inquiries.

---

*© 2026 MDR Solutions. All rights reserved.*
