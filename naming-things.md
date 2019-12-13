## 有意义的命名

大家都说，好的代码处理逻辑通顺，还需要字显其义，看起来足够的清晰。

### 命名足够揭露本意

``` go
var (
	days     					int64 
  elapsedTimeInDays int64
)
```

某些情况下，尤其是局部变量，很多人会用短的缩写（比如首字母）。在上下文环境很明确的情况下，短命名是没有问题的。但是在复杂的系统，还是更推荐长命名。无论长命名还是短命名，一定要注意：命名一定要清晰的表达需要传递的意义。

如果用单词缩写来命名的，尽量用一些通用的词语，比如 `i18n、addr、msg、btn`。这里有一个推荐的网站，帮助查询[缩写词](https://www.abbreviations.com/) 。缩写词必须保持一致，比如都大写或者小写：

| 示例        |      |
| :---------- | :--- |
| `URL`       | ✓    |
| `Url`       | ✕    |
| `url`       | ✓    |
| `HTTP`      | ✓    |
| `ID`        | ✓    |
| `Id`        | ✕    |
| `sendOAuth` | ✓    |
| `oauthSend` | ✓    |

### 变量名支持搜索

在开发的过程中，不只是单单某一个人在参与， 在多人参与的情况下，会涉及到复用、重构等概念。比如

``` py
class Person(object):
    ...
    get_ageiymd() // get age in year, month, days
    get_lmdiymd() // get last modified in year, month, days
    ...
```

** Person** 这个 `model` 等两个函数对人很不友好，可以改写成：

``` py
class Person(object):
    ...
    get_age_year_month_days()
    get_last_modified_year_month_days()
    ...
```

### 类命名实践

类是实体的抽象，用**名词**是一个比较通用的规则，比如 `Person`、 `Car` 。但是不要用通用的或者非常特殊的词语，比如 `Info`, `Manager` and `Controller` 

### 方法命名的实践

`方法命名：前缀(可以不需要) + 动词(do) + 名词(something)`

这里需要注意的是，在抽象这个动词的时候，多个人有多个想法，有人喜欢用 `Fetch`, 也有人推荐 `Retrieve`, 当然更多的是用`Get` 。一般，类的`getter`和`setter`函数，倾向用 `getSomeAttr` 这样的写法；通过包括但不限于`web` 请求（例如向 `Redis` 请求）获取外部的资源时，倾向用 `fetchSomeResource` 这样的写法。但是在对待同一个功能点，挑选一个通用的（团队统一的）词语，这样也可以避免在代码量增多的时候，有很多模棱两可的方法名。

实际编码过程中，对于 `getActiveCustomers` 和 `getActiveCustomersInfo` 两个方法函数来说都有可能出现，职责范围似乎有重复，或者其实就是一个功能。在同一套代码中，不推荐这种有歧义的写法。

### 变量名的实践

`变量命名：前缀(可以不需要) + 描述行词语(ad) + 名词(something)`

这个实践并不算是通用的，举个🌰，比如有一个 `class:` `MemberAddress` , 它有一个字段 `status` 。在某些特定的上下文环境里，也有其他的一些抽象也存在一个 "`status`" ，如果都需要使用的时候，可以用 `member_address_state`来表示 `MemberAddress` 的 `status`。

例如，**moneyAmount** 和 **money** 区别不大；但是 **moneyInRupees** 和 **moneyInDollars** 就能明显区分

### 最后

如果在编码过程中，对命名很头疼的时候，可以参考著名的的[codelf](https://unbug.github.io/codelf/)。