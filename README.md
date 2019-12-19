# kkutu-hack Project

> # First Day

- Date - 2019 - 12 / 18
  - Doing 
    - HTML CODE is Transformation
      - nomal condition -> my turn
- - - 

    class="game-user" -> class="game-user game-user-current"

- - - 

> # Seceond Day

- Date - 2019 - 12 / 19
  - Doing
    -use python and crolling naver word to db
```
import pymysql
from selenium import webdriver
import time
import re

driver = webdriver.Chrome("C:\\Users\\Owner\\Desktop\\chromedriver.exe")
driver.implicitly_wait(3)
cnt=3
word_num=0
conn = pymysql.connect(host='localhost',user='root',password='apmsetup',db='kkutu',charset='utf8')
for i in range(0,2000):
    word_num+=1
    if i == 0:
        driver.get("https://ko.dict.naver.com/#/search?range=entry&page=1&query=%EA%B0%80")
        continue
    if i%10==0:
        cnt+=1
        word_num=0
        driver.get("https://ko.dict.naver.com/#/search?range=entry&page=1&query=%EA%B0%80")
    if "나" in driver.find_element_by_xpath('//*[@id="searchPage_entry"]/div/div['+str(word_num % 10 + 1)+']/div/a/strong').text:
        words = driver.find_element_by_xpath('//*[@id="searchPage_entry"]/div/div['+str(word_num % 10 + 1)+']/div/a').text
        print(words)
        words = re.findall(u'[\uAC00-\uD7A3]+',words)
        sql="insert into word(word) values('"+words[0]+"')"
        print(sql)
        print("page:"+str(cnt))
        print("num:"+str(word_num))
        conn.query(sql)
    else:
        continue
print(rows)
conn.close()

```
