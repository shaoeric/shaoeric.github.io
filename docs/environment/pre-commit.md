# pre-commit

## pre-commit介绍

在提交代码（git commit）时，对代码的规范进行排查，不符合要求时无法提交。参考资料

## 原理

git本身提供了 hook 功能（可参考git相关内容），其中一类就是在commit前调用的，即 .git/hooks/pre-commit.sample 中定义的。pre-commit 的作用就是生成 git 能够识别的 pre-commit hook 脚本。

pre-commit 要解决两个问题：

问题一：pre-commit 中要执行哪些命令。

通过配置文件 .pre-commit-config.yaml 选择要执行的命令。

问题二：命令来源是什么。

在配置文件 .pre-commit-config.yaml 中有指定各类命令对应的 github/gitlab 库。

## 基本流程
1. 在当前环境下安装pre-commit
`pip install pre-commit`

2. 在项目中编写配置文件.pre-commit-config.yaml，具体设置后续介绍
3. 执行命令运行pre-commit
```
pre-commit install
#命令会在.git/hooks目录下生成pre-commit目录
```

4. 后续执行git commit时自动调用相关的检查脚本
  a. 当所有检查通过时，git commit成功
  b. 当有不通过时，git commit失败，重新修改，符合所有规范后重新git add，git commit提交

## pre-commit-config.yaml文件
- 顶层有一个参数名为repos 。
- repos中每个元素为 repo ，代表一个代码库，当指定github/gitlab仓库时，repo设置为对应的链接，当使用本地建立的代码库时，repo设置为local。
- 每个 repo 中有一个或多个 hook ，每个 hook 代表一个任务。
- 每个任务里可理解为一个命令行指令，例如flake8/yapf/black，或者本地的脚本文件

主要任务就是确定要执行哪些任务，即哪些hooks。

示例
```
repos:
# yapf检查
-   repo: https://github.com/PaddlePaddle/mirrors-yapf.git
    sha: 0d79c0c469bab64f7229c9aca2b1186ef47f0e37
    hooks:
    -   id: yapf
        files: \.py$
# 本地代码库检查LICENSE和NOTICE
-   repo: local
    hooks:
    -   id: license-check
        name: Check for LICENSE and NOTICE
        entry: python copyright/license_check.hook
        language: system
        stages: [commit]
        pass_filenames: false
```