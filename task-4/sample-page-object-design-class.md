### Example: Tab Page Object Structure

```java
public class KycTab {

    // Locators
    private By kycThreshold = By.xpath("...");
    private By saveButton = By.xpath("...");
    private By successMessage = By.xpath("...");

    // Action methods
    public void enterKycThreshold(String value) {
        // Enter the threshold value
    }

    public void saveConfiguration() {
        // Save the configuration
    }

    // Assertion methods
    public void verifySuccessMessage(String expectedMessage) {
        // Verify the success message
    }
}
```

This structure separates element identification, user interactions, and verification while keeping tab-specific functionality organized and reusable.
