# Selenium_DB

#import package
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.keys import Keys
import matplotlib.pylab as plt
import sys
import json
import chardet
import time
from bs4 import BeautifulSoup
import re
import pandas as pd
import csv
import datetime
```

```
from webdriver_manager.chrome import ChromeDriverManager

driver = webdriver.Chrome(ChromeDriverManager().install())
```
#get the data
```
url = "https://movie.douban.com/subject/34812928/comments?percent_type=h&limit=20&status=P&sort=new_score"
driver.get(url)
```

```
comments = []
timess = []
```
```
houye = driver.find_element_by_class_name('next')
houye.click()
```

```
info = driver.find_elements_by_class_name('comment-content')
times = driver.find_elements_by_class_name('comment-time')
for i in info:
    comments.append(i.text)

for ii in times:
    timess.append(ii.text)

print(str(len(comments))+"+"+str(len(timess)))
```

```
data_good = {
    'comment':comments,
    'time':timess
}

data_good = pd.DataFrame(data_good)
data_good
```

```
data_good.to_excel('douban_bad.xlsx')
```

