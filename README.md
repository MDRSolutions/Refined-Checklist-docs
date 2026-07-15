# Refined Checklist

**MDR Solutions - Version 1.0.9**

The **Refined Checklist** extension is a lightweight, highly configurable way to add checklists, "Definition of Done," or task-tracking directly into your Azure DevOps work item forms. It supports multiple named checklists per work item type, custom titles, reorderable items, and "Not Applicable" (N/A) status tracking, making it an essential tool for maintaining high standards and consistency across your projects.

---

## Key Features

-   **Configurable Templates:** Define unique checklist items for each Work Item Type (e.g., User Story, Bug, Feature).
-   **State Transition Gates:** Prevent work items from transitioning to specific states when required checklist items are incomplete.
-   **Completion Field Mapping:** Sync checklist completion status to a boolean field on the work item, enabling Azure DevOps process rules to enforce checklist completion on state transitions from any surface (boards, bulk edit, REST API).
-   **Multiple Checklists:** Create multiple named checklists per work item type (e.g., "Definition of Done," "QA Review," "Security Checklist") shown as independent progress sections.
-   **Team-Specific Checklists:** Assign checklists to teams, restrict visibility to team members only, and checklists are grouped by team on work items.
-   **Item Assignment:** Assign checklist items to team members via @mention with notifications.
-   **Guidance Text:** Add Markdown guidance text above each checklist, displayed on the work item form to provide context or instructions.
-   **Tree View Selector:** Navigate work item types and their configured checklists in an auto-expanded tree view within the settings hub, with one-click access to any type or checklist.
-   **Custom Titles:** Label your sections as "Definition of Done," "Acceptance Criteria," or whatever fits your team's workflow.
-   **Intelligent Progress Tracking:** Monitor completion with a dynamic progress bar that turns green upon 100% completion.
-   **Reorderable Items:** Organize your checklist tasks in the exact sequence they should be performed.
-   **N/A Support:** Mark items as "Not Applicable" (N/A) to handle edge cases without affecting your 100% completion goal.
-   **Accountability:** Each check (or N/A) captures the user's name and a timestamp, helping teams stay aligned.

---

## Known Limitations

-   **Board Drag-and-Drop Bypasses State Gates:** State transition gates are only enforced when a work item's state is changed through the **state dropdown** on the work item form. If a state is changed by **dragging and dropping** a card on a board (Kanban or sprint board), the gate check is bypassed and the transition will proceed without verifying checklist completion. **Workaround:** Use [Completion Field Mapping](#4-integration-with-azure-devops-process-rules) in combination with Azure DevOps process rules to enforce checklist completion from any state change surface.

---

## Setup and Configuration

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
3.  Select a **Work Item Type** from the auto-expanded tree view.
4.  **Add one or more named checklists:** Click **Add Checklist** and enter a name (e.g., "Definition of Done," "QA Review").
5.  Click on a checklist to select it, then edit its properties:
    - **Checklist Name:** Rename the checklist.
    - **Team:** Assign the checklist to a team (or keep it project-wide).
    - **Visible only to members:** Restrict visibility to team members only (team-assigned checklists only).
    - **Enable assignments:** Toggle item assignment (@mention) for this checklist.
    - **Guidance text:** Optional Markdown text displayed above the checklist items on the work item form.
    - **Completion Field:** Map this checklist's completion status to a boolean field on the work item type. When all items are complete, the field is set to `true`; otherwise `false`. Each field can only be assigned to one checklist.
6.  Add items using the **Add** button. Click any item's text to rename it directly. Use the **Up/Down** arrows to reorder items.
7.  Click **×** on a checklist pill to delete it.
8.  Click **Save Configuration**.

---

### 4. Integration with Azure DevOps Process Rules

The built-in **State Transition Gates** (step 3 above) only enforce checklist completion when the state is changed through the **state dropdown** on the work item form. State changes made by **dragging cards on boards**, **bulk editing**, or the **REST API** bypass these gates.

The **Completion Field Mapping** feature bridges this gap by keeping a boolean field on the work item in sync with each checklist's completion status. You can then use Azure DevOps process rules to enforce checklist completion regardless of how the state change is triggered.

#### A. Create a boolean field on the work item type

##### Inherited Process Model
1.  Navigate to **Organization Settings** > **Boards** > **Process**.
2.  Select your inherited process and choose the **Work Item Type** (e.g., *User Story*).
3.  Click the **New Field** button.
4.  Enter a **Name** (e.g., "Code Review Complete") and set the **Type** to **Boolean**.
5.  Click **Add Field**.

##### XML Process Model
1.  Export the Work Item Type XML using `witadmin`.
2.  Add a `<FIELD>` element inside `<FIELDS>`:
    ```xml
    <FIELD name="Code Review Complete" type="Boolean" />
    ```
3.  Import the updated XML back into your project collection.

#### B. Map the field to a checklist

1.  Open **Project Settings** > **Checklist Configuration** and select the work item type.
2.  Click on the checklist you want to map.
3.  In the **Completion Field** dropdown, select the boolean field you created.
4.  Click **Save Configuration**.

The field is updated in real time as users check and uncheck checklist items.

#### C. Create a process rule

1.  Navigate to **Organization Settings** > **Boards** > **Process**.
2.  Select your inherited process and choose the **Work Item Type**.
3.  Click **Rules** > **New Rule**.
4.  Set the **When** condition to the state transition you want to guard (e.g., *State changed to Done*).
5.  Add a **Condition**: your boolean field **equals** `False`.
6.  Set the **Action** to **Block save** with a message (e.g., "Complete the checklist before moving to Done.").
7.  Click **Save Rule**.

This prevents the state transition when the checklist is incomplete, regardless of whether the change is made from the work item form, a board, bulk edit, or the REST API.

> **Note:** Each boolean field can only be mapped to one checklist. If you have multiple checklists, create a separate boolean field for each and configure a rule for each one.

---

## Feedback and Bug Reports

If you encounter any bugs, have questions, or want to suggest a feature:
-   **Issues:** Please open a [new issue](https://github.com/MDRSolutions/Refined-Checklist-docs/issues).
-   **Discussions:** Feel free to start a discussion for feedback or general inquiries.

---

*© 2026 MDR Solutions. All rights reserved.*
