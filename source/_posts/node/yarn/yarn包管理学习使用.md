---
title: yarn包管理学习使用
date: 2019-2-15
author: alanJiang
tags:
    - Yarn
    - Node
categories:
    - Node
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: yarn包管理学习使用
---
# 安装
## windows
文件下载安装
[下载](https://yarnpkg.com/latest.msi)

Chocolatey windowns包管理器下载
>   choco install yarn

Scoop 是一个 Windows 的命令行安装程序
>   scoop install yarn

如果 Node.js 没有安装，scoop 将给你一个建议来安装它。 例如：
>   scoop install nodejs

## node安装
>   node install -g yarn

---

# 使用
<div class="guide-content">

<p>现在Yarn已经 <a href="/zh-Hans/docs/install">安装</a>完毕，可以开始使用。以下是一些你需要的最常用的命令：</p>
<p><strong>初始化新项目</strong></p>
<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn init
</code></pre></div></div>

<p><strong>添加依赖包</strong></p>

<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn add <span class="o">[</span>package]
yarn add <span class="o">[</span>package]@[version]
yarn add <span class="o">[</span>package]@[tag]
</code></pre></div></div>

<p><strong>将依赖项添加到不同依赖项类别</strong></p>

<p>分别添加到 <code class="highlighter-rouge">devDependencies</code>、<code class="highlighter-rouge">peerDependencies</code> 和 <code class="highlighter-rouge">optionalDependencies</code>：</p>

<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn add <span class="o">[</span>package] <span class="nt">--dev</span>
yarn add <span class="o">[</span>package] <span class="nt">--peer</span>
yarn add <span class="o">[</span>package] <span class="nt">--optional</span>
</code></pre></div></div>

<p><strong>升级依赖包</strong></p>

<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn upgrade <span class="o">[</span>package]
yarn upgrade <span class="o">[</span>package]@[version]
yarn upgrade <span class="o">[</span>package]@[tag]
</code></pre></div></div>

<p><strong>移除依赖包</strong></p>

<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn remove <span class="o">[</span>package]
</code></pre></div></div>

<p><strong>安装项目的全部依赖</strong></p>

<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn
</code></pre></div></div>

<p>或者</p>

<div class="language-sh highlighter-rouge"><div class="highlight"><pre class="rougeHighlight"><code>yarn install
</code></pre></div></div>

</div>

---

# 修改镜像源

查看使用的镜像源
>   yarn config get registry

配置使用的镜像源
>   yarn config set registry 'https://registry.npm.taobao.org'

npm 的源只需要把yarn改成npm就可以一样修改