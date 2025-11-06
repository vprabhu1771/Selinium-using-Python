You can easily add a **1-second delay** before closing the browser using Python’s built-in `time.sleep()` function.
Here’s your corrected and complete Selenium script 👇

```python
from selenium import webdriver
import time

# Initialize Firefox WebDriver
driver = webdriver.Firefox()

# Open the Django site
driver.get('http://127.0.0.1:8000/')

# Take a screenshot
driver.save_screenshot("screenshot/home_test.png")

# Wait for 1 second before closing
time.sleep(1)

# Close the browser
driver.close()
```

✅ **Explanation:**

* `time.sleep(1)` → pauses the script for **1 second**.
* `driver.save_screenshot()` → saves a screenshot to the specified path.
* `driver.close()` → closes the browser window.

If you want to completely quit the browser session (including background processes), replace `driver.close()` with:

```python
driver.quit()
```
