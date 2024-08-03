# FitpeoProject
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

# Initialize WebDriver (Assuming Chrome)
driver = webdriver.Chrome()

# Step 1: Navigate to the FitPeo Homepage
driver.get('https://www.fitpeo.com')

# Step 2: Navigate to the Revenue Calculator Page
revenue_calculator_link = driver.find_element(By.LINK_TEXT, 'Revenue Calculator')
revenue_calculator_link.click()

# Step 3: Scroll Down to the Slider section
time.sleep(3)  # Wait for the page to load completely
slider = driver.find_element(By.ID, 'slider')  # Replace with the actual ID or class
driver.execute_script("arguments[0].scrollIntoView();", slider)

# Step 4: Adjust the Slider to 820
# Use JavaScript to adjust the slider value to 820
driver.execute_script("arguments[0].value = 820;", slider)

# Alternatively, you can move the slider by simulating a drag-and-drop operation

# Validate that the text field associated with the slider is updated to 820
text_field = driver.find_element(By.ID, 'slider-value')  # Replace with the actual ID or class
assert text_field.get_attribute('value') == '820', "Slider value did not update to 820"

# Step 5: Update the Text Field with value 560
text_field.clear()
text_field.send_keys('560')
text_field.send_keys(Keys.RETURN)  # Simulate pressing Enter

# Validate that the slider's position is updated to reflect the value 560
time.sleep(2)
assert slider.get_attribute('value') == '560', "Slider position did not update to 560"

# Step 6: Validate Total Recurring Reimbursement
# Assuming there's an element that shows the reimbursement value
reimbursement_value = driver.find_element(By.ID, 'reimbursement-value')  # Replace with actual ID or class
assert reimbursement_value.text == '$110700', "Total Recurring Reimbursement did not update correctly"

# Close the browser after task completion
driver.quit()
