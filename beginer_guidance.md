# 我所理解的pull-request流程
## 一、开发前的准备工作。
1. 将公司的项目repo-X, fork到我自己的github帐户内(假定为：repo-Y)。
2. `git clone repo-Y`（clone到本地，进行开发）
3. 至此，前期开始准备工作完成。

## 二、开发中的过程。
1. 与repo-X的owner一道，沟通、建立（确立）ISSUE.（一个或多个）
2. 针某个ISSUE，来针对性的开发。（比如，需要新增Genstage功能？规范、需求等在Issue中讨论 列出）
3. 在本地repo，git checkout -b feature/jason/genstage   # 在我本地repo上，开一个新分支上来开发（新增功能、修复bug、。。。）。分支的命名规范？
4. 本地开发中，可能会有一个或多个本地的提交。# 对本地commit的规范要求？
5. 如果开发时间较长，（几天或一周），而upstream（也就是：repo-X）的提交更新频率、活跃时）：
    1. `git remote add upstream https://github.com/repo-X`
    2. `git remote set-url --push upstream no_push`
    3. `git checkout master`
    4. `git pull upstream `# 随时更新本地的master，与upstream：repox-X的main同步。
    5. `git checkout -b feature/jason/genstage`
    6. `git merge master` （开发分支更新，并在本地解决冲突）
    7. 以上iii - vi步骤，在提交pull-request前，会多次执行。

6. 当针对这个Issue的开发完成后（包含有一个或多个提交。对一个pr提交的中包含的commit的数量 ？涉及变动大小？等的要求？），转入pull-request阶段。

## 三、Pull-Request
1. 发起pr前，再次检查，本地的main与upstream的main，是否同步？不同步的话，需要再次pull upstream main到本地, 本地开发分支rebase到main上。确保无冲突。如果有，先在本地解决。
2. 本地做git push，推送更新到远程克隆来的：repo-Y
3. 登录到github, repo-Y页面，发起pull-request.(对pr的comment的要求？内容的要求？以及其它？）
4. 如果pull-request被接受，并被合并处理：
    1. 可删除此开发分支：feature/jason/genstage
    2. 将本地的main与upstream（repo-X）的main，做一个同步。拉取最新的合并后的代码。
    3. 转而去步骤二，继续解决其它Issue。
5. 如果pull-request被拒绝，并沟通给出不足、需要改进之处？
    1. 继续在本地feature/jason/genstage，做开发、提交。并及时的push到repo-Y（同一个pr? Upstream的owner可随时看到此pr上的后续提交？）
    2. 直至，此pr被owner接受。并被合并到repo-X的main中。
