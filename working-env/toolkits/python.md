---
description: published at 2021-01-13
---

# python

## Pysocks

* In case of sometimes there may some problems caused by using proxy.

```bash
# pysocks allows you request through proxy
pip install pysocks

# turn off proxy
export all_proxy=""

# turn on proxy again
export all_proxy=socks5://127.0.0.1:1080  # replace with your own protocol and port
```

## Anaconda

### Installation

* download from [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual)
* install by double click in MacOS or by running `bash /path/to/package` in Ubuntu
* check if Anaconda is in the `PATH`, check `which python`, check `which conda`

#### Use Virtual Env with Conda

```bash
# Each project should work in an independent virtual environment
conda search "^python$"   # search a python distribution
conda create --name my_env python=3.9.1  # select a python distribution

# Activate
source activate my_env

python --version    # check python version
conda info --envs   # check envs list

# if want to remove an env
conda remove --name my_env --all

# do not auto activate base environment
conda config --set auto_activate_base False
# OR auto activate base environment
conda config --set auto_activate_base True
```

### Update

```bash
# Update under base env
conda update conda      # update conda
conda update anaconda   # will remove packages which are already installed and install whole new version
conda update --all      # will update the packages that are already installed
```

### Reinstall

```bash
# NOTE! always keep `requirments.txt` and `log.txt` in projects
pip freeze -> requirements.txt

# uninstall
rm -rf anaconda3

# remove from PATH, then install like above again

# recreate envs for projects by using `requirments.txt` and `log.txt`
pip install -r requirements.txt
```

## Scrapy

### Getting Start

* open  your virtual python env, enter your project dir;
* run `scrapy start project ProjectName`;
* enter the project and open editor;

## Selenium

* An open-source tool which is used for automating the test carried out on web browsers

### Tools Suite

* `Selenium IDE`: Install from chrome extension market or something like that
* Selenium with python:

  * [https://selenium-python.readthedocs.io/](https://selenium-python.readthedocs.io/)
  * `pip install selenium`
  * `ChromeDriver`: use exactly the same version with chrome browser.

    If using macOS: `brew install chromedriver`

  * To authorize ChromeDriver: `xattr -d com.apple.quarantine chromedriver`
  * start your python script like following:

  ```python
  import selenium
  from selenium import webdriver

  driver = webdriver.Chrome(chromedriverPATH)
  # no parameter if istall chromedriver with brew

  driver.get('https://www.tecmint.com')
  print(driver.title)
  ```

