#### 按功能分层次
```
test-demo
├── config.py
├── instance
│   └── config.py
├── requirements.txt
├── run.py
└── test_demo
    ├── forms
    │   └── __init__.py
    ├── __init__.py
    ├── models
    │   ├── __init__.py
    │   └── User.py
    ├── static
    │   └── style.css
    ├── templates
    │   ├── admin
    │   │   └── base.html
    │   ├── api
    │   │   └── base.html
    │   └── base.html
    ├── utils
    │   └── __init__.py
    └── views
        ├── admin
        │   ├── __init__.py
        ├── api
        │   ├── __init__.py
        └── __init__.py
```


#### 按模块分层次
```
.
├── config.py
├── instance
│   └── config.py
├── requirements.txt
├── run.py
└── test_demo
    ├── admin
    │   ├── forms
    │   │   └── __init__.py
    │   ├── models
    │   │   ├── __init__.py
    │   │   └── User.py
    │   ├── templates
    │   │   └── base.html
    │   ├── utils
    │   │   └── __init__.py
    │   └── views
    │       └── __init__.py
    ├── api
    │   ├── forms
    │   │   └── __init__.py
    │   ├── models
    │   │   ├── __init__.py
    │   │   └── User.py
    │   ├── static
    │   │   └── style.css
    │   ├── templates
    │   │   └── base.html
    │   ├── utils
    │   │   └── __init__.py
    │   └── views
    │       └── __init__.py
    └── __init__.py
```

#### 各自优点：
1. 按功能分层次的优点是各种功能联系紧密， 公用的代码易于管理。 适合中小型的项目。 比如blog, cms, 简易的网上商城。
2. 按模块分层次的优点是将各个功能分离出来， 适合模块化的迁移和公用。 适合稍大的项目, 模块间联系不是很紧密的情况。

#### 各自的缺点：
1. 功能分层的话， 代码后期的迁移难度增加， 代码间的公用性太强， 容易牵一发而动全身。 而且当代码量增加之后， 维护性较差。
2. 模块分层的话， 代码的冗余太多， 许多可以公用的地方无法很好处理， 构造繁琐， 工期较长。

#### flask结构常见文件的作用
1. **config.py** 主要存放配置信息。 比如DEBUG, mysql, sercertkey等。 可以通过flask的 app.config.from_object('config') 自动导入。
2. **instance/config.py** 主要是私人的信息， 可以通过 flask 提供的 app.config.from_pyfile('config.py') 覆盖前者的配置。
3. **requirements** 存放所需要引入的包。
4. **run.py** 运行文件， 加入一些运行配置， 比如使用gunicorn配置， 也可以通过添加manager.py文件管理。
5. **views** 文件存放路由信息， 俗称蓝图。 类似于MVC架构中的controllers。
6. **models** 数据存放与处理的信息。 类似MVC中的Models。
7. **forms** 表单存放的位置。
8. **static** 静态文件的存放。 images/js/css
9. **templates** jinja模板文件。
10. **utils** 一些常用的方法集合。

后续还有...
