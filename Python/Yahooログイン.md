# Yahooログイン
## 概要
Yahooに自動ログインする
ID,Passはコンフィグで設定
## 詳細

```Python
# ログインにpin入力するときに必要、キーボード入力操作
import pyautogui
# 設定ファイルを使うのに必要
import configparser

def yahooLogin():
    driver.get(config['yahoo']['login'])
    driver.set_page_load_timeout(getWait('load'))

    driver.find_element_by_id("username").send_keys(config['yahoo']['id'])
    driver.find_element_by_id("btnNext").click()
    time.sleep(getWait('async'))

    # pin
    #pyautogui.write(config['yahoo']['pin'])

    # password
    driver.find_element_by_id("passwd").send_keys(config['yahoo']['password'])
    driver.find_element_by_id("loginSubmit").click()

    time.sleep(getWait('sync'))
```