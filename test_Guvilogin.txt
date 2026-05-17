from selenium import webdriver
from selenium.webdriver.common.by import By
import time


# ---------------- POSITIVE TEST CASE ---------------- #

def test_valid_login():
    # Open Chrome Browser
    driver = webdriver.Chrome()

    # Maximize Browser
    driver.maximize_window()

    # Open GUVI Website
    driver.get("https://www.guvi.in/")

    time.sleep(3)

    # Click Login Button
    driver.find_element(By.ID, "login-btn").click()

    time.sleep(3)

    # Validate Login Page URL
    assert "sign-in" in driver.current_url

    # Username Box
    username = driver.find_element(By.ID, "email")

    # Password Box
    password = driver.find_element(By.ID, "password")

    # Validate Username Visible and Enabled
    assert username.is_displayed()
    assert username.is_enabled()

    # Validate Password Visible and Enabled
    assert password.is_displayed()
    assert password.is_enabled()

    # Enter Valid Username
    username.send_keys("arunsakthivel@gmail.com")

    # Enter Valid Password
    password.send_keys("*******")

    time.sleep(2)

    # Click Submit Button
    driver.find_element(By.ID, "login-btn").click()

    time.sleep(5)

    # Validate Login Success
    assert "guvi.in" in driver.current_url

    print("Positive Test Case Passed")

    # Close Browser
    driver.quit()


# ---------------- NEGATIVE TEST CASE ---------------- #

def test_invalid_login():
    # Open Chrome Browser
    driver = webdriver.Chrome()

    # Maximize Browser
    driver.maximize_window()

    # Open GUVI Website
    driver.get("https://www.guvi.in/")

    time.sleep(3)

    # Click Login Button
    driver.find_element(By.ID, "login-btn").click()

    time.sleep(3)

    # Enter Invalid Username
    driver.find_element(By.ID, "email").send_keys("wrong@gmail.com")

    # Enter Invalid Password
    driver.find_element(By.ID, "password").send_keys("wrong123")

    time.sleep(2)

    # Click Submit Button
    driver.find_element(By.ID, "login-btn").click()

    time.sleep(3)

    # Validate Login Failed
    assert "sign-in" in driver.current_url

    print("Negative Test Case Passed")

    # Close Browser
    driver.quit()
