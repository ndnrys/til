# スクレイピング(selenium)
## 概要
スクレイピング(selenium)メモ
## 詳細
### 1. インストール

```powershell
pip install selenium
```

### 2. chromeドライバーダウンロード

[https://chromedriver.chromium.org/download](https://chromedriver.chromium.org/downloads)

### 3. インポート

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

# Chrome起動
driver = webdriver.Chrome('./chromedriver')
```

### 4. よく使うコマンド

#### テキストを入力する

```python
driver.find_element_by_id("ID").send_keys("strings")
```

#### テキストを取得する

```python
driver.find_element_by_id("ID").text
```

#### 属性を取得する

```python
driver.find_element_by_id("ID").get_attribute("value")
```

#### タイトルを取得する

```python
driver.title
```

#### ページのソースを取得する

```python
driver.page_source
```

#### 要素を取得する

```python
driver.find_element_by_class_name("classname") # classでの指定
driver.find_element_by_id("id") # idでの指定
driver.find_element_by_xpath("xpath") # xpathでの指定
```

#### ある要素をクリックする

```python
driver.find_element_by_xpath("XPATH").click()
```

#### ある要素までスクロールする

```python
element = driver.find_element_by_id("ID") # 適切なIDに変更してください。
actions = new Actions(driver)
actions.move_to_element(element)
actions.perform()
```

#### ドロップダウンを選択したいとき

```python
element = driver.find_element_by_xpath("xpath")
Select(element).select_by_index(indexnum) # indexで選択
Select(element).select_by_value("value") # valueの値
Select(element).select_by_text("text") # 表示テキスト
```

#### 特定のURLでブラウザを起動する

```python
driver.get("URL")
```

#### 1つ前に戻る

```python
driver.back()
```

#### 現在のURLを取得する

```python
driver.forward()
```

#### ブラウザを更新する

```python
driver.refresh()
```

### Seleniumクイックリファレンス

[https://www.seleniumqref.com/api/webdriver_gyaku.html](https://www.seleniumqref.com/api/webdriver_gyaku.html)