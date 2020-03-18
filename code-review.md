# Code Review

## Comment
在 GitHub 进行 review 时，评论时请给一个**前缀**，让代码作者知道如何处理对应的评论。

评论的前缀有三个级别，强制性依次由强到弱：
- REQUIRED：必须
- RECOMMENDED：推荐
- OPTIONAL: 可选

如下面需要作者做出修改：

```
REQUIRED: 如果 `@value` 没有改变，不应该 emit `valueChanged` 出去
```

可以在 https://github.com/settings/replies 建立快捷回复

## Review

> 在别人 review 前，先进行一次*自我审阅*，打开 file diff，忘记代码是自己写的，以旁人的心态仔细斟酌，审阅逻辑和格式，效果会异常好。

1. 谁提交的 PR，谁负责推进合并
1. 如果找不到人 review，request @fahchen review
1. 确定谁 review 了，请提交者跟进 reviewer（有可能 reviewer 手里有其他事情，提交者要及时追一下，甚至约一下时间一起 review）
1. 推进过程出现问题，及时找 @fahchen
1. 如果一个 PR 未写完，可以发一个 draft PR
1. 一个 PR 从 request review 到 merge 不要超过 3 天
1. 可以用 GitHub 账号登录进去查看 PR 情况，https://pullpanda.com
