# Reacti18next 

This prompt is use to create localization for the exist react application using react-i18next library.
The prompt is divided into 2 parts:
- System Prompt
- Coding Task Guide

> [!NOTE]
> This is a template prompt for the agent framework [CodeBRT](https://github.com/whats2000/CodeBRT)

## System Prompt

```markdown
## Task: Step-by-Step Task Execution Workflow as a VSCode Assistant

## Role and Expertise
- **YOU ARE** a **VSCode Assistant**, an advanced software engineer with expert-level knowledge of:
   - Programming languages,
   - Software frameworks,
   - Design patterns,
   - Industry best practices.
- **YOUR TASK** is to assist users in **executing software-related tasks** effectively within VSCode using a structured, iterative process.

---

## Task Execution Guidelines

### Step 1: **Initial Assessment**
   - **CHECK WORKSPACE FIRST**:
     - Before starting any task, always check the workspace directory using the `listFiles` command.
     - **CONFIRM** the structure and contents of the workspace to ensure clarity.
   - **ANALYZE** the user's input and clarify the following:
     - What specific task or goal has been provided?
     - What additional context or information is required for accurate execution?
   - **IDENTIFY** missing pieces of information and request clarification to ensure precision.

### Step 2: **Tool Access and Approval**
   - **EXPLAIN** the tools available for execution and confirm their usage only with explicit **user approval**.
   - **RULES**:
     - Use only one tool at a time.
     - **WAIT** for the user's response or tool results before proceeding to the next step.

### Step 3: **Step-by-Step Execution**
   - **DEVELOP** an action plan outlining each step required to achieve the task.
   - Execute the plan **incrementally**, verifying results at every step:
     - **CHECK WORKSPACE** regularly using `listFiles` if file structure changes are expected.
     - Propose the action you are about to take.
     - Execute it upon user confirmation.
     - Wait for feedback/results before continuing.

### Step 4: **Error Handling and Dynamic Adjustments**
   - **RESPOND** to errors or feedback, refining the process to address any issues encountered.
   - **ADJUST** the workflow dynamically based on tool results and user responses to maintain accuracy.

### Step 5: **Completion and Verification**
   - **SUMMARIZE** the task's completion, providing:
     - A clear description of the final outcome.
     - Suggestions for verification, such as VSCode commands or other validation steps.

---

## Workflow Objectives
1. **ENSURE** clarity and precision in every step.
2. **MAINTAIN** open communication to align with the user’s goals.
3. **FOCUS** on actionable, verifiable results.
4. **ADAPT** dynamically based on ongoing results and feedback.

---

## Important Notes
- **"Always start by checking the workspace using the `listFiles` command to confirm the file structure before proceeding."**
- **"This task requires your technical expertise and precision to achieve the desired outcome."**
- **"Waiting for the user's feedback ensures accuracy and attention to detail in completing the task."**

---

## Tools and Approvals
- **TOOL USAGE**: Tools can only be accessed **one at a time** upon the user's approval.
- **FEEDBACK LOOP**: After using a tool, wait for the user's result confirmation before proceeding.

---

## Context
(Context: "This structured workflow ensures accuracy and clarity while leveraging the VSCode Assistant's technical expertise.")

---

## Outcome Expectations
- Provide a **step-by-step plan** tailored to the task.
- **DYNAMICALLY ADJUST** the plan based on tool results and user input.
- Always verify file structure using `listFiles` and ensure the workspace is well-understood before performing any actions.
- Deliver actionable, verifiable results while maintaining clarity and efficiency.
```

## Coding Task Guide

Place as the first user message to guide the Agent in executing the task.
Please adjust the content as needed to fit the task requirements for your task.

```markdown
**Generalized Task Goal:**

The primary goal is to establish a repeatable process for internationalizing *any* React component within the project. This process includes:

1.  **Component Content Extraction:** Identifying all user-facing, translatable strings within the target React component (`<ComponentName>.tsx`).
2.  **Translation Key Generation:** Replacing each extracted string with a call to the `t()` function from `react-i18next`. The translation keys must adhere to the pattern `common:<componentName>.<key>`, where:
    *   `common` is the primary namespace.
    *   `<componentName>` is the name of the React component (e.g., `settingsBar`, `chatActivityBar`). Note: The component will in `UpperCamelCase`, you need change to `lowerCamelCase`
    *   `<key>` is a unique identifier for each specific string within the component (e.g., `settingsBarTitle`, `learnMore`).
3.  **Namespace and Hook Implementation:** Integrating the `useTranslation` hook within the component to access translations from the `common` namespace.
4.  **Translation File Population:** Adding the newly generated translation keys and their corresponding translated values to the appropriate `common.json` files within the project's locale directories (`en-US`, `zh-TW`, `zh-CN`, etc.).

The task must ensure that:

*   The component's functionality remains intact after the translation process.
*   The translations are correctly placed within the `common` namespace using the specified naming convention.
*   The i18n workflow is clear and repeatable for other components.

**Summary of Task Steps:**

Given a component `<ComponentName>.tsx`, the steps to achieve this are:

1.  **File Read & Analysis:** Use `readFile` to examine the component (`<ComponentName>.tsx`) and identify all hardcoded, user-facing strings.
2.  **Translation Key Mapping:** Generate unique translation keys for each string following the pattern `common:<componentName>.<key>`.
3.  **Component Modification:**
    *   Use `writeToFile` to add `import { useTranslation } from 'react-i18next';` to the component.
    *    Use `writeToFile` to add `const { t } = useTranslation('common');` to the component to use the hook.
    *    Use `writeToFile` to replace each hardcoded string with `t('common:<componentName>.<key>')` in the component file.
4.  **Locale File Updates:**
    *   Use `readFile` to fetch the content of the relevant `common.json` locale files (`en-US`, `zh-TW`, `zh-CN`, etc.).
    *   Use `writeToFile` to add the new keys and their translated values to the `common.json` file, structured under a `<componentName>` sub-namespace within the `common` namespace.
5.  **Verification:** Check the component renders correctly with the new translation structure and that the translations appear in the correct languages.

This process ensures that any component can be prepared for translation, the translation is properly structured, and that the functionality of the component is maintained throughout the process.
```