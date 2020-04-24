## selenium的使用

### 声明浏览器对象

```python
from selenium import webdriver
browser = webdriver.Chrome()
```

### 访问界面

```python
from selenium import webdriver

browser = webdriver.Chrome()
browser.get('https://www.taobao.com')
print(browser.page_source)
browser.close()
```

### 单个节点

```python
find_element_by_id
find_element_by_name
find_element_by_xpath
find_element_by_link_text
find_element...
```

Selenium还提供了find_element这个通用方法，它需要传入两个参数：查找方式By和值。实际上，find_element就是find_element_by_id这种方法的通用函数版本find_element_by_id(id) 就等价于 find_element(By.ID, id)，二者得到的结果完全一致。

### 多个节点

如果查找所有满足条件的节点,需要用 find_elements 这样的方法。

```python
lis = browser.find_elements_by_css_selector('.service-bd li') 
```

### 节点交互

输入文字时send_keys方法,清空文字时用clear方法,点击按钮时用click方法

```python
browser.get("")
input = browser.find_element_by_id('')
input.send_keys()
input.clear()
button = browser.find_element_by_class_name("")
button.click()
```

### 执行js

selenium api 并没有提供实现某些操作的方法,比如下拉进度条,但是可以直接运行js,此时使用execute_script方法即可实现

```python
browser = webdriver.Chrome()

browser.get("")
browser.execute_script('window.scrollTo(0,document.body.scrollHeight)')
```

### 获取节点信息

#### 获取属性

我们可以使用get_attribute方法来获取节点的属性,前提选中这个节点

```python
browser = webdriver.Chrome()

url='https://dynamic2.scrape.cuiqingcai.com/'
browser.get(url)
logo=browser.find_element_by_class_name('logo-image')
print(logo)
print(logo.get_attribute('src'))
```

### 延时等待

#### 隐式等待

如果selenium没有找到dom节点,将继续等待,超出设定的时间后,抛出找不到节点的异常

```python
browser = webdriver.Chrome()
browser.implicitly_wait(10)
browser.get('https://dynamic2.scrape.cuiqingcai.com/')
input=browser.find_element_by_class_name("logo-image")
print(input)
```

#### 显式等待

页面加载可能会受到网络的影响,所以隐式等待的效果并不是那么好

显式等待指定要查找的节点,指定一个最长等待时间,如果在规定的时间内加载出来就返回,如果没有则抛出异常.

### 前进后退

```python
browser = webdriver.Chrome()
browser.get('https://www.baidu.com/')
browser.get('https://www.taobao.com/')
browser.get("https://www.python.org/")
browser.back()
time.sleep(1)
browser.forward()
browser.close()
```

### cookie

使用selenium,可以方便的对cookie进行管理

```python
browser = webdriver.Chrome()
browser.get("https://www.zhihu.com/explore")

print(browser.get_cookies())

browser.add_cookie({})
browser.delete_all_cookies()
```

