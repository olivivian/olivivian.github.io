# 插件

- 搜索

```$xslt
npm install hexo-generator-search --save
```

在 Hexo 根目录下的 _config.yml 文件中，新增以下的配置项：
```$xslt
search:
  path: search.xml
  field: post
```

- 中文链接转拼音

如果文章名称是中文，那么 Hexo 默认生成的永久链接也会有中文，这样不利于 SEO
```$xslt
npm i hexo-permalink-pinyin --save
```

在 Hexo 根目录下的 _config.yml 文件中，新增以下的配置项：
```$xslt
permalink_pinyin:
  enable: true
  separator: '-' # default: '-'
```

- 文章字数统计插件

```$xslt
npm i --save hexo-wordcount
```

# 修改

修改页脚
```$xslt
在主题文件的 /layout/_partial/social-link.ejs 文件中
```

