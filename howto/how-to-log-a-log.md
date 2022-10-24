# 怎么写日志 | How to Log a Log

## 写日志的目的？

1. 收集 metrics（主要是性能方面）

   如果已经使用性能监控工具，可以不记录这方面的日志

2. 故障排除

   不仅需要写日志，还需要即时通知机制（如 Slack）

3. ❗️~~记录程序运行的 journal~~

   这个 journal 重要吗？不重要的话，不要记录；重要的话，把它持久化到数据库里

4. ❗️~~记录用户的行为，用来做数据挖掘~~

   将用户的行为结构化成 events，持久化到数据库里

## 日志写什么？

无论是什么用途，日志始终记录事件（events）

#### 元数据

对于每一条日志，都应该包含这些元数据

1. 时间戳（UTC）
2. 外部环境
   1. request ID's
   2. PID's
   3. user ID's
3. 内部环境（可选）
   1. app
   2. module
   3. function

#### 主体

即事件本身

1. 发生了什么
2. 为什么会出现这样的情况？（当发生错误时记录）
3. 采取的措施是什么？（当发生错误时记录）

## 怎么写日志？

1. 用 plain text 写日志，不用 binary 等其它格式
2. 将日志结构化成键值对的形式，例如 json。其它形式也可以接受，前提是始终使用统一的格式、机器易于解析该格式
3. 将元数据和事件分开记录，例子如下，其中 `"http_response_sent"` 记录事件的数据：

```json
{
    "dt": "2019-02-04T12:23:34Z",
    "level": "info",
    "message": "Completed 200 OK in 79ms (Views: 78.8ms | ActiveRecord: 0.0ms)",
    "context": {
        "host": "34.235.155.83",
        "user_id": 5,
        "path": "/welcome",
        "method": "GET"
    },
    "http_response_sent": {
        "status": 200,
        "duration_ms": 79.0,
        "view_ms": 78.8,
        "active_record_ms": 0.0
    }
}
```

4. 使用正确的 level。参考如下：

| Microsoft | Serilog | lognet | Description                                                  |
| --------- | ------- | ------ | ------------------------------------------------------------ |
| Critical  | Fatal | FATAL  | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| Error  | Error   | ERROR  | Logs that highlight when the current flow of execution is stopped due to a failure. These should indicate a failure in the current activity, not an application-wide failure. |
| Warning  | Warning | WARN  | Logs that highlight an abnormal or unexpected event in the application flow, but do not otherwise cause the application execution to stop. |
| Information  | Information  | INFO  | Logs that track the general flow of the application. These logs should have long-term value. |
| Debug  | Debug  | DEBUG  | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Trace  | Verbose  | ALL  | Logs that contain the most detailed messages. These messages may contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |

5. 不记录敏感信息或者过滤掉敏感信息，例如用户的密码、应用的 secret
```json
{
    "dt": "2019-02-04T12:23:34Z",
    "level": "info",
    "message": "Completed 200 OK in 79ms (Views: 78.8ms | ActiveRecord: 0.0ms)",
    "context": {
        "host": "34.235.155.83",
        "user_id": 5,
        "user_phone": "[FILTERED]",
        "path": "/welcome",
        "method": "GET"
    },
    "http_response_sent": {
        "status": 200,
        "duration_ms": 79.0,
        "view_ms": 78.8,
        "active_record_ms": 0.0
    }
}
