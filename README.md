# Pilot-test

Selenium download test

from selenium import webdriver
from selenium.webdriver.common.by import By
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service
import time

download_folder = r"C:\Users\Administrator\Desktop\Sellenium"

options = webdriver.ChromeOptions()
prefs = {"download.default_directory": download_folder}
options.add_experimental_option("prefs", prefs)

driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)

driver.get("https://the-internet.herokuapp.com/download")

time.sleep(3)

# get all links
files = driver.find_elements(By.CSS_SELECTOR, "a")

print("Total files:", len(files))

# extract download URLs
links = []
for f in files:
    links.append(f.get_attribute("href"))

print("Starting downloads...")

# open each download link
for link in links:

    print("Downloading:", link)
    driver.get(link)

    time.sleep(2)

print("All downloads completed")

driver.quit()
