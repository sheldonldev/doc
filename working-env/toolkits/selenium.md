---
description: 2021-01-13
---

# Selenium

- An open-source tool which is used for automating the test carried out on web browsers

## Tools Suite

- `Selenium IDE`: Install from chrome extension market or something like that

- Selenium with python:
  - <https://selenium-python.readthedocs.io/>
  - `pip install selenium`
  - `ChromeDriver`: use exactly the same version with chrome browser.
    If using macOS: `brew install chromedriver`
  - start your python script like following:
  ```py
  import selenium
  from selenium import webdriver

  driver = webdriver.Chrome(chromedriverPATH) 
  # no parameter if istall chromedriver with brew

  driver.get('https://www.tecmint.com')
  print(driver.title)
  ```
