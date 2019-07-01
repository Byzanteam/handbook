# GitHub flow

> 基于 [git-flow](https://github.com/nvie/gitflow)

主分支是 `develop`，线上分支为 `master`（生产环境）.

## 如何开始工作

1. 先将 repo `fork` 到自己账号下
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

### Commit 格式
can
提交信息首行简要描述该提交涉及的改动，建议以动词开头。如需添加相关 `issue` 或 `jira` 任务的链接，须与首行之间保留一个空行，从第三行开始。可参考以下格式：
```log
第一行 [<type>:] 简要描述该提交涉及的改动，建议以开头动词 [(<scope>)]
第二行 空行
第三行 相关的链接（issue 或 jira 等）
第四行 更多必要信息
```
type（可选）:
```log
feat: 新功能
fix: 修复问题
docs: 添加或者修改文档
test: 添加或者测试用例
refactor: 重构（既不涉及新功能，也不是修复问题）
chore: 构建工具或者辅助工具的变动
style: 调整格式
```
scope（可选）:
 比如fix涉及的范围 组件名、文件名等等逗号分隔

例子：
```log
Integrate immutable.js (A,B,C)

https://trello.com/c/yIglLjvq
```

```shell
# add it to profile(如：~/.zshrc)
alias gclc='git commit -v --reset-author -c `git log --pretty=%H -n1`'
```

### Emoji For Your Commit Messages

| emoji | code | message |
|---|---|---|
| :art: | `:art:` | Improving structure / format of the code |
| :zap: | `:zap:` | Improving performance |
| :fire: | `:fire:` | Removing code or files |
| :bug: | `:bug:` | Fixing a bug |
| :ambulance: | `:ambulance:` | Critical hotfix |
| :sparkles: | `:sparkles:` | Introducing new features |
| :pencil: | `:pencil:` | Writing docs |
| :rocket: | `:rocket:` | Deploying stuff |
| :lipstick: | `:lipstick:` | Updating the UI and style files |
| :tada: | `:tada:` | Initial commit |
| :white_check_mark: | `:white_check_mark:` | Updating tests |
| :lock: | `:lock:` | Fixing security issues |
| :apple: | `:apple:` | Fixing something on macOS |
| :penguin: | `:penguin:` | Fixing something on Linux |
| :checkered_flag: | `:checkered_flag:` | Fixing something on Windows |
| :robot: | `:robot:` | Fixing something on Android |
| :green_apple: | `:green_apple:` | Fixing something on iOS |
| :bookmark: | `:bookmark:` | Releasing / Version tags |
| :rotating_light: | `:rotating_light:` | Removing linter warnings |
| :construction: | `:construction:` | Work in progress |
| :green_heart: | `:green_heart:` | Fixing CI Build |
| :arrow_down: | `:arrow_down:` | Downgrading dependencies |
| :arrow_up: | `:arrow_up:` | Upgrading dependencies |
| :pushpin: | `:pushpin:` | Pinning dependencies to specific versions |
| :construction_worker: | `:construction_worker:` | Adding CI build system |
| :chart_with_upwards_trend: | `:chart_with_upwards_trend:` | Adding analytics or tracking code |
| :recycle: | `:recycle:` | Refactoring code |
| :whale: | `:whale:` | Work about Docker |
| :heavy_plus_sign: | `:heavy_plus_sign:` | Adding a dependency |
| :heavy_minus_sign: | `:heavy_minus_sign:` | Removing a dependency |
| :wrench: | `:wrench:` | Changing configuration files |
| :globe_with_meridians: | `:globe_with_meridians:` | Internationalization and localization |
| :pencil2: | `:pencil2:` | Fixing typos |
| :poop: | `:poop:` | Writing bad code that needs to be improved |
| :rewind: | `:rewind:` | Reverting changes |
| :twisted_rightwards_arrows: | `:twisted_rightwards_arrows:` | Merging branches |
| :package: | `:package:` | Updating compiled files or packages |
| :alien: | `:alien:` | Updating code due to external API changes |
| :truck: | `:truck:` | Moving or renaming files |
| :page_facing_up: | `:page_facing_up:` | Adding or updating license |
| :boom: | `:boom:` | Introducing breaking changes |
| :bento: | `:bento:` | Adding or updating assets |
| :ok_hand: | `:ok_hand:` | Updating code due to code review changes |
| :wheelchair: | `:wheelchair:` | Improving accessibility |
| :bulb: | `:bulb:` | Documenting source code |
| :beers: | `:beers:` | Writing code drunkenly |
| :speech_balloon: | `:speech_balloon:` | Updating text and literals |
| :card_file_box: | `:card_file_box:` | Performing database related changes |
| :loud_sound: | `:loud_sound:` | Adding logs |
| :mute: | `:mute:` | Removing logs |
| :busts_in_silhouette: | `:busts_in_silhouette:` | Adding contributor(s) |
| :children_crossing: | `:children_crossing:` | Improving user experience / usability |
| :building_construction: | `:building_construction:` | Making architectural changes |
| :iphone: | `:iphone:` | Working on responsive design |
| :clown_face: | `:clown_face:` | Mocking things |
| :egg: | `:egg:` | Adding an easter egg |
| :see_no_evil: | `:see_no_evil:` | Adding or updating a .gitignore file |
| :camera_flash: | `:camera_flash:` | Adding or updating snapshots |
| :alembic: | `:alembic:` | Experimenting new things |
| :mag: | `:mag:` | Improving SEO |
| :wheel_of_dharma: | `:wheel_of_dharma:` | Work about Kubernetes |
| :label: | `:label:` | Adding or updating types (Flow, TypeScript) |

例子：
```log
🐛: fix ...

card / issue url
```

工具:
- [alfred-emoji-workflow](https://github.com/carlosgaldino/alfred-emoji-workflow)

### Pull Request 格式
1. 以 `jira` 对应的 card 的 title 作为标题
1. 描述里面附加本次 PR 的说明
1. 描述里面附加 `jira` 对应 card 的 link
1. 适当添加一些 todo list
1. 尽量使用 [squash merge](https://github.com/conventional-changelog/standard-version#should-i-always-squash-commits-when-merging-prs)

#### 参考：
- [Understanding the GitHub flow](https://guides.github.com/introduction/flow/)
- [Using git-flow to automate your git branching workflow](https://jeffkreeftmeijer.com/git-flow/)
- [Git工作流指南](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)
- [Conventional Commits](https://www.conventionalcommits.org)
- [gitmoji - An emoji guide for your commit messages](https://gitmoji.carloscuesta.me/)
