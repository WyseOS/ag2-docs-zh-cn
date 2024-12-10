---
myst:
  html_meta:
    "description lang=zh-cn": |
      安装 AutoGen AgentChat
    "charset": "utf-8"
---

# 安装

## 创建一个虚拟环境 (可选)

当在本地安装 AgentChat 时，我们建议使用虚拟环境进行安装。这将确保 AgentChat 的依赖项与系统其余部分隔离。

``````{tab-set}

`````{tab-item} venv

创建并激活：

```bash
python3 -m venv .venv
source .venv/bin/activate
```

要停用，请运行：

```bash
deactivate
```

`````

`````{tab-item} conda

[安装 Conda](https://docs.conda.io/projects/conda/en/stable/user-guide/install/index.html)。


创建并激活：

```bash
conda create -n autogen python=3.10
conda activate autogen
```

要停用，请运行：

```bash
conda deactivate
```


`````



``````

## 使用 pip 安装 AgentChat 包

使用 pip 安装 `autogen-agentchat` 包：

```bash

pip install 'autogen-agentchat==0.4.0.dev6'
```

## 安装 OpenAI 模型客户端

要使用 OpenAI 和 Azure OpenAI 模型，您需要安装以下扩展：

```bash
pip install 'autogen-ext[openai]==0.4.0.dev6'
```

## 安装 Docker 用于代码执行

我们建议使用 Docker 用于代码执行。

要安装 Docker，请遵循 [Docker 网站](https://docs.docker.com/get-docker/) 上的操作系统说明。

一个简单的使用 Docker 进行代码执行的示例如下：

<!-- ```{include} stocksnippet.md

``` -->

要了解更多关于执行代码的代理，请参阅 [agent tutorial](./tutorial/agents.ipynb)。
