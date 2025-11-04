# 1 - Introduction

Certainly! Here's an explanation of the code snippet:

1. First, we import the necessary modules from the Selenium package:
   ```python
   from selenium import webdriver
   from selenium.webdriver.common.by import By
   from selenium.webdriver.common.keys import Keys
   ```

2. We create an instance of the web driver using the appropriate driver for your browser (Chrome in this example):
   ```python
   driver = webdriver.Chrome()
   ```

3. Next, we navigate to the Django admin login page by using the `get()` method and passing the URL as a parameter:
   ```python
   driver.get('http://localhost:8000/admin/')  # Replace with your Django admin URL
   ```

4. To find the username and password input fields, we use the `find_element()` method with the `By.NAME` selector, which allows us to locate elements by their name attribute:
   ```python
   username_input = driver.find_element(By.NAME, 'username')
   password_input = driver.find_element(By.NAME, 'password')
   ```

5. We enter the login credentials by using the `send_keys()` method on the respective input fields:
   ```python
   username_input.send_keys('your_username')
   password_input.send_keys('your_password')
   ```

6. To submit the login form, we simulate pressing the Enter key by sending the `Keys.RETURN` key using the `send_keys()` method on the password input field:
   ```python
   password_input.send_keys(Keys.RETURN)
   ```

7. After submitting the form, you can perform further actions as needed within the Django admin interface using Selenium's API.

8. Finally, we close the web driver to clean up the resources:
   ```python
   driver.close()
   ```

Make sure to replace `'http://localhost:8000/admin/'` with the actual URL of your Django admin interface, and `'your_username'` and `'your_password'` with your own login credentials.

# 2 - app.py

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

# Use webdriver.Firefox() for Firefox
driver = webdriver.Firefox()

# Replace with your Django admin URL
driver.get('http://127.0.0.1:8000/admin/')

username_input = driver.find_element(By.NAME,'username')
password_input = driver.find_element(By.NAME,'password')

username = "admin@gmail.com"
password = "admin"

username_input.send_keys(username)
password_input.send_keys(password)

password_input.send_keys(Keys.RETURN)

#driver.close()
```

# 3 - app.py

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

class DjangoAdminLogin:
    def __init__(self, url):
        self.url = url
        self.driver = webdriver.Firefox()  # Use webdriver.Chrome() for Chrome

    def login(self, username, password):
        self.driver.get(self.url)

        username_input = self.driver.find_element(By.NAME, 'username')
        password_input = self.driver.find_element(By.NAME, 'password')

        username_input.send_keys(username)
        password_input.send_keys(password)

        password_input.send_keys(Keys.RETURN)

    def close(self):
        self.driver.close()

# Create an instance of the DjangoAdminLogin class
admin_login = DjangoAdminLogin('http://127.0.0.1:8000/admin/')

# Replace with your admin credentials
username = 'admin@gmail.com'
password = 'admin'

# Call the login method with the credentials
admin_login.login(username, password)

# Close the web driver
#admin_login.close()
```

# 4 - Export Requirements
```
pip freeze requirements.txt
```

# 5 - requirements.txt
```
selenium==4.9.1
```