# GitHub flow

> 基于 [git-flow](https://github.com/nvie/gitflow)

1. 对于区分线上和测试环境的 repo: 主分支是 `develop`，线上分支为 `main`（生产环境）
1. 对于类似与 package 的 repo: 主分支为 `main`

## 如何开始工作

1. 从远程分支开新分支进行开发
1. 开发完毕后 push 到 GitHub
1. 到 GitHub 提交 `Pull Request`，打上对应的 `label`，然后 request 对应的同事 review

## 什么样的代码才能合并进 `develop`/`main` 分支：

- 规定数量的 approved
- 经过 GitHub Actions 或其他 CI

## Branch naming

```
{type}/{username}/{branch-name}
```

例子: `feat/fahchen/integrate-immutable-js`

## Commit 格式

提交信息首行简要描述该提交涉及的改动，建议以动词开头。如需添加相关 `issue` 或任务等的链接，须与首行之间保留一个空行，从第三行开始。可参考以下格式：
```log
第一行 [<type>:] 简要描述该提交涉及的改动，建议以开头动词 [(<scope>)]
第二行 空行
第三行 相关的链接（issue 或任务链接等）
第四行 更多必要信息
```

**type（可选）:**

```log
feat: 新功能
fix: 修复问题
docs: 添加或者修改文档
test: 添加或者测试用例
refactor: 重构（既不涉及新功能，也不是修复问题）
chore: 构建工具或者辅助工具的变动
style: 调整格式
```

**scope（可选）:**

比如 fix 涉及的范围 组件名、文件名等等逗号分隔

```log
Integrate immutable.js (A,B,C)

https://trello.com/c/yIglLjvq
```

## Pull Request 格式
1. 以对应的任务作为标题
1. 描述里面附加本次 PR 的说明
1. 描述里面附加任务相关的链接
1. 适当添加一些 todo list
1. 尽量使用 [squash merge](https://github.com/conventional-changelog/standard-version#should-i-always-squash-commits-when-merging-prs)

## 常用命令

```shell
# add it to profile(如：~/.zshrc)
alias gclc='git commit -v --reset-author -c `git log --pretty=%H -n1`'
```

## 工具
使用 [Commitizen](https://github.com/commitizen/cz-cli) 来帮你写 commit message


## 参考：
- [Understanding the GitHub flow](https://guides.github.com/introduction/flow/)
- [Using git-flow to automate your git branching workflow](https://jeffkreeftmeijer.com/git-flow/)
- [Git工作流指南](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)
- [Conventional Commits](https://www.conventionalcommits.org)
- [gitmoji - An emoji guide for your commit messages](https://gitmoji.carloscuesta.me/)
- [Developing AngularJS](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits)
