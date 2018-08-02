## 通过 selenium 加上 headless Chrome 来测试网页(爬虫神器)

废话无多，上码

```
from selenium import webdriver

options = webdriver.ChromeOptions()
options.binary_location = "/usr/sbin/chromium"
options.add_argument("headless")
options.add_argument("window-size=1200x600")
driver = webdriver.Chrome(chrome_options=options)

driver.get('https://lovesun.xyz')
print(driver.title)
driver.get_screenshot_as_file('main-page.png')
driver.close()

```

1. 需要安装 `pip install selenium`
1. 本机有chrome浏览器， 我的是在linux下，用的chromium， 所以路径是`/usr/sbin/chromium`

后续还在接着写呢。。。
