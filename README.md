# pyyaml-erb

> 解析 yaml 配置文件中的的环境变量

------

## 运行环境

![](https://img.shields.io/badge/Python-3.8%2B-brightgreen.svg)


## 介绍

模仿 Ruby 的 [ERB](https://docs.ruby-lang.org/en/2.3.0/ERB.html) 能力，把 yaml 配置文件中的环境变量做简单解析。


## 使用说明

在代码中引入 pyyaml-erb 包，读取配置 yml 配置文件即可：

```python
import erb.yml as yaml
with open(SETTING_PATH, 'r', encoding='utf-8') as file :
    settings = yaml.load(file.read())
```

配置示例可参考 [settings.yml](./tests/config/settings.yml)，使用教程可参考单元测试 [test_yaml_erb.py](./tests/test_yaml_erb.py)。

例如环境变量为 `JAVA_HOME`，只需要在 yaml 配置为 `<%= ENV["KEY"] %>` 或 `<%= ${KEY} %>` 的值表达式即可识别并解析。

一般而言，值表达式有以下几种配置模式：

- `key_1: <%= ENV["VAR_1"] %>`： 默认的使用方式
- `key_2: <%= ENV["VAR_2"] or None %>`： 跟默认方式一样，多了默认值为 None，没意义
- `key_3: <%= ENV["VAR_3"] || null %>`： 跟默认方式一样，多了默认值为 None，没意义
- `key_4: <%= ENV["VAR_4"] || "nil" %>`： 跟默认方式一样，多了默认值为 None，没意义
- `key_5: <%= ENV["VAR_5"] || default %>`： 若环境变量不存在，会设置为默认值
- `key_6: "<%= ENV['VAR_6'] or 'default' %>"`： 若环境变量不存在，会设置为默认值
- `key_7: <%= ENV["VAR_7"] || 7 %>`： 若环境变量不存在，会设置为默认值，且默认值会解析为整型
- `key_8: <%= ENV["VAR_8"] || 1.23 %>`： 若环境变量不存在，会设置为默认值，且默认值会解析为浮点型
- `key_9: <%= ENV["VAR_9"] || true %>`： 若环境变量不存在，会设置为默认值，且默认值会解析为布尔型
- `key_10: <%= ENV["VAR_10"] || 'False' %>`： 若环境变量不存在，会设置为默认值，且默认值会解析为布尔型
- `key_0: '<%= ENV["VAR_0"] || ${VAR_11} or default %>'`： 混合模式

> 引号用双引号或单引号都可以，值表达式外围用不用引号包围都可以，表达式之间用 `||` 或 `or` 都可以


## 开发者说明

<details>
<summary>展开</summary>
<br/>

### 手动打包项目

每次修改代码后，记得同步修改 [`setup.py`](setup.py) 下的版本号 `version='x.y.z'`。

```
# 构建用于发布到 PyPI 的压缩包
python setup.py sdist

# 本地安装（测试用）
pip install .\dist\pyyaml-erb-?.?.?.tar.gz

# 本地卸载
pip uninstall pyyaml-erb
```

### 手动发布项目

首先需要在 [PyPI](https://pypi.org/) 上注册一个帐号，并在本地用户根目录下创建文件 `~/.pypirc`（用于发布时验证用户身份），其内容如下：

```
[distutils]
index-servers=pypi

[pypi]
repository = https://upload.pypi.org/legacy/
username = <username>
password = <password>
```

其次安装 twine 并上传项目： 

```
# 首次发布需安装
pip install twine

# 发布项目， 若发布成功可在此查看 https://pypi.org/manage/projects/
twine upload dist/*
```

发布到 [PyPI](https://pypi.org/) 的项目名称必须是全局唯一的，即若其他用户已使用该项目名称，则无法发布（报错：`The user 'xxx' isn't allowed to upload to project 'yyy'.`）。此时只能修改 [`setup.py`](setup.py) 下的项目名称 `name`。


> 本项目已集成了 Github Workflows，每次推送更新到 master 即可自动打包并发布到 PyPI


### 关于测试

详见 [单元测试说明](tests)


### 参考资料

- [python package 开发指引](https://packaging.python.org/#python-packaging-user-guide)
- [python package 示例代码](https://github.com/pypa/sampleproject)

</details>



## 赞助途径

| 支付宝 | 微信 |
|:---:|:---:|
| ![](imgs/donate-alipay.png) | ![](imgs/donate-wechat.png) |


## 版权声明

　[![Copyright (C) EXP,2016](https://img.shields.io/badge/Copyright%20(C)-EXP%202016-blue.svg)](http://exp-blog.com)　[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

- Site: [http://exp-blog.com](http://exp-blog.com) 
- Mail: <a href="mailto:289065406@qq.com?subject=[EXP's Github]%20Your%20Question%20（请写下您的疑问）&amp;body=What%20can%20I%20help%20you?%20（需要我提供什么帮助吗？）">289065406@qq.com</a>


------
