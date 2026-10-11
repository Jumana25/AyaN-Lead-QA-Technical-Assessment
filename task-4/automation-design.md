# Task 4 — Automation Design

## 1. Project structure and Page Object Model design

```text
📦 BankOperationsAutomation
┣ 📂 src
┃ ┣ 📂 main
┃ ┃ ┗ 📂 java
┃ ┃   ┗ 📂 org
┃ ┃     ┗ 📂 example
┃ ┃       ┣ 📂 pageObjects
┃ ┃       ┃ ┣ 📄 LoginPage.java
┃ ┃       ┃ ┣ 📄 BankOperationsPage.java
┃ ┃       ┃ ┣ 📄 OnboardingTab.java
┃ ┃       ┃ ┣ 📄 KycTab.java
┃ ┃       ┃ ┣ 📄 TransferLimitsTab.java
┃ ┃       ┃ ┣ 📄 FeesTab.java
┃ ┃       ┃ ┗ 📄 NotificationsTab.java
┃ ┃       ┗ 📂 utils
┃ ┃         ┣ 📄 BrowserActions.java
┃ ┃         ┣ 📄 JsonUtils.java
┃ ┃         ┣ 📄 JSUtils.java
┃ ┃         ┣ 📄 Screenshooter.java
┃ ┃         ┣ 📄 SeleniumActions.java
┃ ┃         ┣ 📄 BaseWebDriver.java
┃ ┃         ┗ 📄 TestDataFactory.java
┃ ┣ 📂 test
┃ ┃ ┣ 📂 java
┃ ┃ ┃ ┗ 📂 org
┃ ┃ ┃   ┗ 📂 example
┃ ┃ ┃     ┣ 📂 stepdefinitions
┃ ┃ ┃     ┃ ┗ 📄 BankOperationsSteps.java
┃ ┃ ┃     ┣ 📂 testRunner
┃ ┃ ┃     ┃ ┗ 📄 TestRunner.java
┃ ┃ ┃     ┗ 📂 hooks
┃ ┃ ┗ 📂 resources
┃ ┃   ┣ 📂 features
┃ ┃   ┃ ┗ 📄 TestFeature.feature
┃ ┃   ┣ 📂 TestData
┃ ┃   ┃ ┗ 📄 Users.json
┃ ┃   ┣ 📄 cucumber.properties
┃ ┃   ┗ 📄 log4j2.xml
┣ 📂 reports
┣ 📂 logs
┣ 📂 target
┣ 📄 .gitignore
┣ 📄 pom.xml
┣ 📄 Jenkinsfile
┣ 📄 README.md
┗ 📄 extent.properties
```

* **BankOperationsPage.java:** Handles shared console elements and tab navigation.
* **Individual tab classes:** Each tab has its own Page Object to manage its fields and actions.
* **Reusable field interactions:** Common methods handle text inputs, checkboxes, and dropdowns.
* **Utilities:** Centralize browser interactions, JSON operations, JavaScript execution, screenshots, and test-data
  generation.
* **Reporting and logging:** Reports and logs support failure investigation and execution tracking.
* **CI integration:** `Jenkinsfile` supports automated execution through Jenkins.

## 2. Locator strategy

* **Unique label:** Locate the field directly using its label when it uniquely identifies the target.
* **Stable wrapper:** Locate the parent wrapper using its visible label or a unique descriptive attribute, then locate
  the child control inside it.
* **Partial dynamic identifier:** Use the fixed portion of an identifier only when it is unique and stable.
* **Avoid dynamic identifiers:** Do not rely on generated identifiers, such as `slot="field-145"`, as primary locators.

### Handling Different Control Types

Use reusable methods to identify and interact with the control inside the field wrapper:

* **Text input:** Enter or retrieve the field value.
* **Checkbox:** Check or uncheck it based on the expected state.
* **Dropdown:** Select or verify the expected option.

This approach keeps field interactions consistent across tabs while accommodating different control types.

## 3. Handling dynamic DOM

* **Use `By` locators:** Locate elements when needed instead of retaining `WebElement` references, reducing stale
  element issues after tab switches or scrolling.
* **Use explicit waits:** Wait for elements to meet the required condition, such as being visible, enabled, clickable,
  or invisible, depending on the business case.
* **Avoid fixed waits:** Prefer condition-based waits to handle dynamic rendering reliably.
* **Re-locate elements:** Reuse the locator when interacting with elements after a tab switch or DOM refresh.

## 4. Test data strategy

| Data type            | Approach                                                                                                                      |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------|
| UI labels            | Include directly in examples if localization isn't required.                                                                  |
| Environment settings | Store URLs and other environment-specific configurations in a project config file.                                            |
| Test data            | Store in JSON files, separating read-only data from data used to create or modify records.                                    |
| Unique values        | Generate dynamically when needed to avoid conflicts between test runs.                                                        |
| Cleanup              | Restore modified configurations and avoid destructive operations, as the environment is shared and cannot be reset on demand. |

## 5. Reusability and scalability

* **Adding tabs and fields:** Reuse existing field interaction methods and create a new Page Object only when adding a new tab.
* **Execution time:** Avoid unnecessary navigation and use explicit waits instead of fixed delays.
* **Parallel execution:** Isolate test data and avoid concurrent modifications to the same configuration.
* **Scaling:** Keep tab-specific logic separate from shared functionality so the framework can grow from 7 to 20 tabs with minimal structural changes.

## 6. Tooling

I would lean toward **Selenium with Java**, given my hands-on experience and familiarity with its ecosystem. This would allow me to design and maintain the framework effectively.

However, I would consider the following trade-offs:

* **Selenium:** My existing experience reduces the learning curve, but pipeline execution time and test stability would need to be evaluated and optimized.
* **Playwright:** Its built-in auto-waiting and browser context isolation are attractive, but I wouldn't assume they automatically guarantee fewer flaky tests or better pipeline performance.

**Final decision:** I would start with Selenium, measure execution time and stability in the CI pipeline, and optimize based on the results rather than switching tools based on assumptions.
