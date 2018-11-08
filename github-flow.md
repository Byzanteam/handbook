# GitHub flow

> 基于 [git-flow](https://github.com/nvie/gitflow)

主分支是 `develop`，线上分支为 `master`（生产环境）.

## 如何开始工作
1. 先讲 repo `fork` 到自己账号下
1. 然后开新分支进行开发
1. 开发完毕后 push 到自己的 repo
1. 到 GitHub 提交 `Pull Request`，打上对应的 `label`，然后 request 对应的同事 review

### 什么样的代码才能合并进 develop 分支：

- 有至少一个同事的 approved
- 被产品或者设计验收通过
- 经过 CodeClimate 和 单元测试（CircleCI）
  - CodeClimate 的 issues 原则上不能自己点通过，一定是和团队协商通过，或者修改 rules

### Master Branch
master 分支作为线上运行的版本，初步定在让运维来发 release。





#### 参考：
- https://guides.github.com/introduction/flow/
- https://jeffkreeftmeijer.com/git-flow/
