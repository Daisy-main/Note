# Material for MkDocs

`mkdocs`基于`python`环境

[mkdocs安装](https://mkdocs.org.cn/user-guide/installation/)

## Material for MkDocs主题的安装

使用`pip`命令安装，在终端输入以下安装指令

=== "最新"

    ```bash
    pip install mkdocs-material
    ```

=== "9.x"

    ```bash
    pip install mkdocs-material==9.5.0
    ```
---

## 显示效果

主要参考 [Material for MkDocs配置](https://squidfunk.github.io/mkdocs-material/reference/)进行配置，更加个性化的配置需要自定义CSS文件

### 内容标签页 (Content Tabs)

内容标签页 (Content Tabs)，允许你在同一个区域切换显示不同的内容，写法如下

```markdown title="markdown"

=== "标签1"

    这是标签1的内容

=== "标签2"

    这是标签2的内容
```

显示效果如下：

=== "橘子"

    这是🍊

=== "柠檬"

    这是🍋

> ***TIPS***: 

> 使用 `=== "标签名称"` 的语法来包裹代码块

> 连续出现的 `===` 会被自动识别为一个组 

> 拆分方框可以在两个标签块之间加一行文字

> [yml配置](#Content Tabs)

---

## mkdocs.yml配置

### 主题配置

```yaml title="yml"

theme:
  language: zh
  name: material

  logo: images/orange-96.png    #个人logo
  favicon: images/orange-96.png #网站图标

  font:
    text: Inter      
    code: Fira Code  

  #暗夜模式和明亮模式  
  palette:
    - scheme: default
      toggle:
          icon: material/brightness-7 
          name: Switch to dark mode
      
      primary: white
      accent: cyan

    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode

      primary: white
      accent: cyan
```

<div id="Content Tabs"></div>

### 内容标签页配置

```yaml title="yml"

markdown_extensions:
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true # 卡片式风格
```

## 参考资料

> [Material for MkDocs官网](https://squidfunk.github.io/mkdocs-material/)

> [Material for MkDocs emoji](https://mkdocs.dbtgo.com/reference/icons-emojis/)

> [Material for MkDocs配置](https://squidfunk.github.io/mkdocs-material/reference/)