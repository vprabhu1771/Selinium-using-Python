`LoginTest.py`

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time
import os


def login_page_load_test(driver):
    print("🟢 Running login_page_load_test()")
    driver.get('http://127.0.0.1:8000/admin')

    time.sleep(3)
    driver.save_screenshot("screenshot/login_page_load_test.png")
    print("📸 Saved login_page_load_test.png")


def login_test(driver):
    print("🟢 Running login_test()")
    driver.get('http://127.0.0.1:8000/admin/')

    try:
        WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.ID, 'form.email'))
        )
    except Exception:
        print("❌ Could not find element with ID 'id_username'. Check your page HTML.")
        print("🔍 Page source snippet:\n", driver.page_source[:500])
        raise

    username_input = driver.find_element(By.ID, 'form.email')
    password_input = driver.find_element(By.ID, 'form.password')

    username = "admin@gmail.com"
    password = "admin"

    username_input.send_keys(username)
    password_input.send_keys(password)
    password_input.send_keys(Keys.RETURN)

    # WebDriverWait(driver, 10).until(
    #     EC.url_contains("http://127.0.0.1:8000/dashboard")
    # )
    time.sleep(5)

    driver.save_screenshot("screenshot/login_test.png")
    print("📸 Saved login_test.png")


def logout_test(driver):
    print("🟢 Running logout_test()")
    driver.get('http://127.0.0.1:8000/admin')
    time.sleep(5)
    driver.find_element(By.XPATH, "//input[@type='submit']").click()
    print("🔘 Clicked Sign out button")

    time.sleep(2)
    driver.save_screenshot("screenshot/signout_test.png")
    print("📸 Saved signout_test.png")


if __name__ == "__main__":
    os.makedirs("screenshot", exist_ok=True)

    driver = webdriver.Firefox()
    driver.maximize_window()

    try:
        login_page_load_test(driver)
        login_test(driver)
        logout_test(driver)
    except Exception as e:
        print("❌ Test failed:", e)
    finally:
        time.sleep(3)
        driver.quit()
        print("✅ Browser closed.")
```