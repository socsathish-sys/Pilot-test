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


#--------Screenshot--------------
from selenium import webdriver
from selenium.webdriver.edge.service import Service
from webdriver_manager.microsoft import EdgeChromiumDriverManager
import time
import os

# Folder to save screenshots
screenshot_folder = r"C:\Users\Sathish\Downloads\TestScreenshots"
os.makedirs(screenshot_folder, exist_ok=True)

# Edge options
options = webdriver.EdgeOptions()

# Launch Edge browser
driver = webdriver.Edge(service=Service(EdgeChromiumDriverManager().install()), options=options)

# Open website
driver.get("https://the-internet.herokuapp.com/download")

# wait for page to load
time.sleep(3)

# Screenshot file path
screenshot_path = os.path.join(screenshot_folder, "website_screenshot.png")

# Take screenshot
driver.save_screenshot(screenshot_path)

print("Screenshot saved at:", screenshot_path)

driver.quit()

#--------------with Proxy----------

from selenium import webdriver
from selenium.webdriver.edge.service import Service
from selenium.webdriver.edge.options import Options
import os
import time

# ==========================
# PROXY CONFIGURATION
# ==========================

proxy = "http://proxy.company.com:8080"   # change to your proxy

os.environ['HTTP_PROXY'] = proxy
os.environ['HTTPS_PROXY'] = proxy

# ==========================
# SCREENSHOT FOLDER
# ==========================

screenshot_folder = os.path.join(os.getcwd(), "screenshots")
os.makedirs(screenshot_folder, exist_ok=True)

# ==========================
# EDGE OPTIONS
# ==========================

edge_options = Options()
edge_options.add_argument(f'--proxy-server={proxy}')

# ==========================
# START EDGE BROWSER
# ==========================

driver = webdriver.Edge(options=edge_options)

# ==========================
# OPEN WEBSITE
# ==========================

driver.get("https://the-internet.herokuapp.com/download")

time.sleep(3)

driver.maximize_window()

# ==========================
# TAKE SCREENSHOT
# ==========================

screenshot_path = os.path.join(screenshot_folder, "website_screenshot.png")

driver.save_screenshot(screenshot_path)

print("Screenshot saved at:", screenshot_path)

# ==========================
# CLOSE BROWSER
# ==========================

driver.quit()
