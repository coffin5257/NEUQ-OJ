# NEUQ-OJ

## 项目结构

### project结构

这里定义的是python开源项目目录结构中的$PROJ_NAME目录内的内容，需要与python开源项目目录结构结合起来。

```
PROJ_NAME/
     __init__.py      这几个文件是django创建project所必须的，不做过多说明
     manage.py
     settings.py
     urls.py
     apps/               即使是“小”工程，也建议分成多个app，每个app足够简单，只解决某一个方面的问题 （注1）
         myapp1/
         myapp2/
     extra_apps/     引用的其他app。
     libs/                加载第三方模块，可以避免版本冲突，按照标准的site-packages管理（注2）
           python*.*/　　指定python版本号
               site-packages/
               requirements.pip    #pip的依赖说明文件
     tests/          project级别的测试，对于每个app，还要有自己的测试代码
     static/          静态内容
            css/
            js/
            images/
     uploads/       上传文件所在目录
     templates/    模板目录，覆盖app的模板
            flatpages/
            comments/
            example/
            app1/
            app2/
     templatetags/    tag目录
```

注1：指定app加载，在settings.py中设置：

sys.path.insert(0, os.path.join(PROJECT_ROOT, 'apps'))
sys.path.insert(0, os.path.join(PROJECT_ROOT, 'extras'))
sys.path.insert(0, os.path.join(PROJECT_ROOT, 'libs'))

注2：自定义libs的加载，在settings.py中设置：

sys.path.insert(0, '/{{MY_LIB)}/site-packages/*****.egg')
sys.path.insert(0, '/{{MY_LIB}} /site-packages/')

### app目录结构

```
$APP_NAME/
     tests/                    app级别的测试代码
     models/                 注1
          __init__.py
          Amodels.py
          Bmodels.py
     templates/              注2
     templatetags/        tag目录
```

注1：如果很好的控制app的规模，Model类数量少，可以使用惯用的models.py文件中, 否则将models做成一个package

接下来可以有两种做法：

1. 在__init__.py中import所有的Model类
2. 指定Model的元类（Meta）的app_label, 参考这里

注2：如果extend 工程下的base.html， 使用 !base.html

## 安装

## 开发