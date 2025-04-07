---
title: Team Open API Version 2 中文版本
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.28"

---

# Team Open API Version 2 中文版本

生产环境 URLs: https://<替换成生产域名></a>

域名指向的IP获取方式：
* 首先在 UCloud 云平台上创建 MAXIR AI 实例，并在详情页获取OpenAPI地址;
* 外网访问的情况下，客户需通过ALB（应用负载均衡器）获取并绑定外网地址,可参考[相关文档](https://docs.ucloud.cn/maxirai/introduction/access)；
* 将自己的业务域名指向该外网地址，以完成配置。


# Authentication

* API Key (apikey-header-x-pd-api-key)
    - Parameter Name: **x-pd-api-key**, in: header. 

# Session

## POST Create session

POST /v2/team/sessions

创建会话。
会话即用户与 MAXIR AI 在单次对话中的持续交互过程。每个用户至多可以同时保留 150 个会话。达到此上限后，如需创建新会话，可以删除不再使用的会话后，再进行创建。

> Body 请求参数

```json
{
  "name": "My session",
  "output_language": "FR",
  "job_mode": "AUTO",
  "max_contextual_job_history": 10,
  "agent_id": "DATA_ANALYSIS_AGENT",
  "user_id": "tmm-dafasdfasdfasdf"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 |none|
|» name|body|string| 是 |会话名称，至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|» output_language|body|string| 否 |MAXIR AI 的回复语言。例如，当设置为 `EN` 时，则 MAXIR AI 使用英语进行回复。如不指定，将使用默认值 `AUTO`，即 MAXIR AI 会根据提示词自动选择合适的回复语言。可选值包括：|
|» job_mode|body|string| 否 |任务类型。可选值包括：|
|» max_contextual_job_history|body|integer| 否 |作为下一个任务上下文的历史任务数，取值范围为 `0` 到 `10`，默认值为 `10`。如设置为 `0`，则当前任务将不使用任何历史任务作为上下文信息。|
|» agent_id|body|string| 否 |AI 智能体的 ID。该参数为保留参数，无需制定或设置为 **DATA_ANALYSIS_AGENT**。|
|» user_id|body|string| 是 |用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**» output_language**: MAXIR AI 的回复语言。例如，当设置为 `EN` 时，则 MAXIR AI 使用英语进行回复。如不指定，将使用默认值 `AUTO`，即 MAXIR AI 会根据提示词自动选择合适的回复语言。可选值包括：

- `AUTO`：根据提示词自动识别
- `EN`：英语
- `ES`：西班牙语
- `AR`：阿拉伯语
- `PT`：葡萄牙语
- `ID`：印尼语
- `JA`：日语
- `RU`：俄语
- `HI`：印地语
- `FR`：法语
- `DE`：德语
- `VI`：越南语
- `TR`：土耳其语
- `PL`：波兰语
- `IT`：意大利语
- `KO`：韩语
- `ZH-CN`：简体中文
- `ZH-TW`：繁体中文

**» job_mode**: 任务类型。可选值包括：

- `AUTO`：MAXIR AI 根据你的提问进行意图判断，决定该任务为数据分析任务或信息检索任务。
- `DATA_ANALYTICS`：MAXIR AI 会根据你的输入进行数据分析。

如不指定，则采用默认值 `AUTO`。如果您明确地想要进行数据分析，我们建议您将值设置为 **DATA_ANALYTICS**，从而 MAXIR AI 可以跳过意图识别步骤，加快问题处理速度。

#### 枚举值

|属性|值|
|---|---|
|» output_language|AUTO|
|» output_language|EN|
|» output_language|ES|
|» output_language|AR|
|» output_language|PT|
|» output_language|ID|
|» output_language|JA|
|» output_language|RU|
|» output_language|HI|
|» output_language|FR|
|» output_language|DE|
|» output_language|VI|
|» output_language|TR|
|» output_language|PL|
|» output_language|IT|
|» output_language|KO|
|» output_language|ZH-CN|
|» output_language|ZH-TW|
|» job_mode|AUTO|
|» job_mode|DATA_ANALYTICS|
|» agent_id|DATA_ANALYSIS_AGENT|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "session-dasfasdgasdgfasdgasdg"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||返回的数据对象。|
|»» id|string|true|none||会话 ID。<br /><br />如后续要使用该会话来 [执行任务](/api-reference/create-job)，请保存该 ID。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET List sessions

GET /v2/team/sessions

返回您创建的会话列表。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|page_number|query|integer| 否 |分页返回的起始页码。如不指定，则使用默认值 `1`。|
|page_size|query|integer| 否 |每页返回的记录数量。如不指定，则使用默认值 `10`。|
|search|query|string| 否 |搜索关键词，最多支持 128 个字符。所有名称中包含该关键词的会话将被返回。|
|user_id|query|string| 是 |用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**search**: 搜索关键词，最多支持 128 个字符。所有名称中包含该关键词的会话将被返回。

如果省略此项，将列出所有会话。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "total_items": 8,
    "page_size": 10,
    "page_number": 1,
    "records": [
      {
        "id": "04b69928-532d-408a-8716-8f5e70fcacc6",
        "name": "Finding Your Inner Spark",
        "output_language": "AUTO",
        "job_mode": "AUTO",
        "max_contextual_job_history": 10,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "7e9941af-ad1b-4834-a421-4b37b54aae19",
        "name": "session_trade_analyze_001",
        "output_language": "EN",
        "job_mode": "AUTO",
        "max_contextual_job_history": 1,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "a137ecc8-9554-42c3-b042-2458dd2aeb36",
        "name": "My first session",
        "output_language": "AUTO",
        "job_mode": "AUTO",
        "max_contextual_job_history": 10,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "4440ab38-3df0-465b-a66c-bf6acb0f1bc2",
        "name": "New name",
        "output_language": "EN",
        "job_mode": "AUTO",
        "max_contextual_job_history": 10,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "3eb5e294-11eb-4bf0-8854-7177c415d15c",
        "name": "trade_analyze_001",
        "output_language": "ZH-CN",
        "job_mode": "AUTO",
        "max_contextual_job_history": 10,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "ccca6d34-894f-4f6f-a8b5-c9df93126309",
        "name": "lhtest-old",
        "output_language": "ZH-CN",
        "job_mode": "AUTO",
        "max_contextual_job_history": 5,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "c28a1f47-da68-4456-bb0b-e85bf5a0e98e",
        "name": "lhtest-newest",
        "output_language": "ZH-TW",
        "job_mode": "AUTO",
        "max_contextual_job_history": 6,
        "agent_id": "DATA_ANALYSIS_AGENT"
      },
      {
        "id": "fbde9b45-69cd-408e-97d1-f874236aadac",
        "name": "General-session",
        "output_language": "ZH-CN",
        "job_mode": "AUTO",
        "max_contextual_job_history": 10,
        "agent_id": "DATA_ANALYSIS_AGENT"
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||会话的分页列表。|
|»» total_items|integer|true|none||返回的会话总数量。|
|»» page_number|integer|true|none||当前页面的页码。|
|»» page_size|integer|true|none||每页返回的会话数量。|
|»» records|[object]|true|none||当前页面返回的会话列表。|
|»»» id|string|true|none||会话 ID，会话在当前项目中的唯一标识。|
|»»» name|string|true|none||会话名称。如名称长度超过 128 个字符，将仅返回前 128 个字符。|
|»»» output_language|string|false|none||MAXIR AI 的返回语言。可能值包括：<br /><br />- `AUTO`：根据提示词自动识别<br />- `EN`：英语<br />- `ES`：西班牙语<br />- `AR`：阿拉伯语<br />- `PT`：葡萄牙语<br />- `ID`：印尼语<br />- `JA`：日语<br />- `RU`：俄语<br />- `HI`：印地语<br />- `FR`：法语<br />- `DE`：德语<br />- `VI`：越南语<br />- `TR`：土耳其语<br />- `PL`：波兰语<br />- `IT`：意大利语<br />- `KO`：韩语<br />- `ZH-CN`：简体中文<br />- `ZH-TW`：繁体中文|
|»»» job_mode|string|false|none||任务类型。可能值包括：<br /><br />- `AUTO`：MAXIR AI 根据您的提问进行意图判断，决定任务是数据分析任务还是信息检索任务。<br />- `DATA_ANALYTICS`：MAXIR AI 根据您的输入进行数据分析。|
|»»» max_contextual_job_history|integer|false|none||在会话中保留作为下一个任务上下文的任务数量，取值范围为 `0` 到 `10`，默认值为 `10`。值为 `0` 时表示会话中的任务在执行时不会使用历史任务执行结果作为上下文信息。|
|»»» agent_id|string|false|none||AI 智能体的 ID。该参数为保留参数，无实际意义，请忽略。|

#### 枚举值

|属性|值|
|---|---|
|output_language|AUTO|
|output_language|EN|
|output_language|ES|
|output_language|AR|
|output_language|PT|
|output_language|ID|
|output_language|JA|
|output_language|RU|
|output_language|HI|
|output_language|FR|
|output_language|DE|
|output_language|VI|
|output_language|TR|
|output_language|PL|
|output_language|IT|
|output_language|KO|
|output_language|ZH-CN|
|output_language|ZH-TW|
|job_mode|AUTO|
|job_mode|DATA_ANALYTICS|
|agent_id|DATA_ANALYSIS_AGENT|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## POST Modify session

POST /v2/team/sessions/{id}

修改会话配置。

> Body 请求参数

```json
{
  "name": "hello",
  "output_language": "EN",
  "job_mode": "DATA_ANALYSIS",
  "max_contextual_job_history": 3,
  "user_id": "tmm-ddsdfsfgs"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |要修改的会话 ID。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 |none|
|» name|body|string| 是 |会话名称，至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|» output_language|body|string| 否 |MAXIR AI 的回复语言。例如，当设置为 `EN` 时，则 MAXIR AI 使用英语进行回复。如不指定，将使用默认值 `AUTO`，即 MAXIR AI 会根据提示词自动选择合适的回复语言。可选值包括：|
|» job_mode|body|string| 否 |任务类型。可选值包括：|
|» max_contextual_job_history|body|integer| 否 |作为下一个任务上下文的历史任务数，取值范围为 `0` 到 `10`，默认值为 `10`。如设置为 `0`，则当前任务将不使用任何历史任务作为上下文信息。|
|» user_id|body|string| 是 |用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**id**: 要修改的会话 ID。

如需查看项目中存在的会话，请调用 [GET /v2/team/sessions](/api-reference/list-sessions) 接口。

**» output_language**: MAXIR AI 的回复语言。例如，当设置为 `EN` 时，则 MAXIR AI 使用英语进行回复。如不指定，将使用默认值 `AUTO`，即 MAXIR AI 会根据提示词自动选择合适的回复语言。可选值包括：

- `AUTO`：根据提示词自动识别
- `EN`：英语
- `ES`：西班牙语
- `AR`：阿拉伯语
- `PT`：葡萄牙语
- `ID`：印尼语
- `JA`：日语
- `RU`：俄语
- `HI`：印地语
- `FR`：法语
- `DE`：德语
- `VI`：越南语
- `TR`：土耳其语
- `PL`：波兰语
- `IT`：意大利语
- `KO`：韩语
- `ZH-CN`：简体中文
- `ZH-TW`：繁体中文

**» job_mode**: 任务类型。可选值包括：

- `AUTO`：MAXIR AI 根据你的提问进行意图判断，决定该任务为数据分析任务或信息检索任务。
- `DATA_ANALYTICS`：MAXIR AI 会根据你的输入进行数据分析。

如不指定，则采用默认值 `AUTO`。如果您明确地想要进行数据分析，我们建议您将值设置为 **DATA_ANALYTICS**，从而 MAXIR AI 可以跳过意图识别步骤，加快问题处理速度。

#### 枚举值

|属性|值|
|---|---|
|» output_language|AUTO|
|» output_language|EN|
|» output_language|ES|
|» output_language|AR|
|» output_language|PT|
|» output_language|ID|
|» output_language|JA|
|» output_language|RU|
|» output_language|HI|
|» output_language|FR|
|» output_language|DE|
|» output_language|VI|
|» output_language|TR|
|» output_language|PL|
|» output_language|IT|
|» output_language|KO|
|» output_language|ZH-CN|
|» output_language|ZH-TW|
|» job_mode|AUTO|
|» job_mode|DATA_ANALYTICS|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||操作成功则返回 null。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## DELETE Delete session

DELETE /v2/team/sessions/{id}

删除会话。一旦删除，该会话及其任务历史记录将被永久删除，且无法恢复。

> Body 请求参数

```json
{
  "user_id": "tmm-dafasdfasdfasdf"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |要删除的会话 ID。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 |none|
|» user_id|body|string| 是 |用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**id**: 要删除的会话 ID。

如需查看项目中存在的会话，请调用 [GET /v2/team/sessions](/api-reference/list-sessions) 接口。

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|false|none||操作成功则返回 null。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET Get session

GET /v2/team/sessions/{id}

获取指定会话的配置信息。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |目标会话的 ID。|
|user_id|query|string| 是 |用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**id**: 目标会话的 ID。

如需查看项目中存在的会话，请调用 [GET /v2/team/sessions](/api-reference/list-sessions) 接口。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "cckrXXg68P8lmb59dg4yO",
    "name": "Analyze performance",
    "output_language": "HI",
    "job_mode": "AUTO",
    "max_contextual_job_history": 76,
    "agent_id": "DATA_ANALYSIS_AGENT"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||会话对象。|
|»» id|string|true|none||会话 ID，会话在当前项目中的唯一标识。|
|»» name|string|true|none||会话名称。如名称长度超过 128 个字符，将仅返回前 128 个字符。|
|»» output_language|string|false|none||MAXIR AI 的返回语言。可能值包括：<br /><br />- `AUTO`：根据提示词自动识别<br />- `EN`：英语<br />- `ES`：西班牙语<br />- `AR`：阿拉伯语<br />- `PT`：葡萄牙语<br />- `ID`：印尼语<br />- `JA`：日语<br />- `RU`：俄语<br />- `HI`：印地语<br />- `FR`：法语<br />- `DE`：德语<br />- `VI`：越南语<br />- `TR`：土耳其语<br />- `PL`：波兰语<br />- `IT`：意大利语<br />- `KO`：韩语<br />- `ZH-CN`：简体中文<br />- `ZH-TW`：繁体中文|
|»» job_mode|string|false|none||任务类型。可能值包括：<br /><br />- `AUTO`：MAXIR AI 根据您的提问进行意图判断，决定任务是数据分析任务还是信息检索任务。<br />- `DATA_ANALYTICS`：MAXIR AI 根据您的输入进行数据分析。|
|»» max_contextual_job_history|integer|false|none||在会话中保留作为下一个任务上下文的任务数量，取值范围为 `0` 到 `10`，默认值为 `10`。值为 `0` 时表示会话中的任务在执行时不会使用历史任务执行结果作为上下文信息。|
|»» agent_id|string|false|none||AI 智能体的 ID。该参数为保留参数，无实际意义，请忽略。|

#### 枚举值

|属性|值|
|---|---|
|output_language|AUTO|
|output_language|EN|
|output_language|ES|
|output_language|AR|
|output_language|PT|
|output_language|ID|
|output_language|JA|
|output_language|RU|
|output_language|HI|
|output_language|FR|
|output_language|DE|
|output_language|VI|
|output_language|TR|
|output_language|PL|
|output_language|IT|
|output_language|KO|
|output_language|ZH-CN|
|output_language|ZH-TW|
|job_mode|AUTO|
|job_mode|DATA_ANALYTICS|
|agent_id|DATA_ANALYSIS_AGENT|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET Get job history in session

GET /v2/team/sessions/{id}/history

获取指定会话中的任务记录。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |目标会话的 ID。|
|page_number|query|integer| 否 |分页返回的起始页码。如不指定，则使用默认值 `1`。|
|page_size|query|integer| 否 |每页返回的记录数量。如不指定，则使用默认值 `10`。|
|user_id|query|string| 是 |用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**id**: 目标会话的 ID。

如需查看项目中存在的会话，请调用 [GET /v2/team/sessions](/api-reference/list-sessions) 接口。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "total_items": 1,
    "page_number": 1,
    "page_size": 10,
    "records": [
      {
        "job_id": "job-1dsfasddfasgddsaffds",
        "question": {
          "blocks": [
            {
              "type": "MESSAGE",
              "content": "Check for negative values across all sales columns"
            }
          ]
        },
        "answer": {
          "blocks": [
            {
              "type": "MESSAGE",
              "content": "- Check for negative values across all sales columns.\n- Filter the DataFrame to retain only rows with no negative sales values.",
              "group_id": "ba582fc9-bb36-4c5d-a8e8-d35bda6389cd",
              "group_name": "Identify the channels with negative sales values by examining each day's sales data. Filter out the rows where any sales value is negative.",
              "stage": "Analyze"
            },
            {
              "type": "CODE",
              "content": "```python\n\nimport pandas as pd\n\ndef invoke(input_0: pd.DataFrame) -> pd.DataFrame:\n    '''\n    input_0: pd.DataFrame  SalesByChannelByDay_Summary_Demo.Sheet1_0_table_1.csv\n    '''\n    # Identify columns that represent sales data (all except the first column)\n    sales_columns = input_0.columns[1:]\n    \n    # Filter rows where any sales value is negative\n    filtered_df = input_0[~(input_0[sales_columns] < 0).any(axis=1)]\n    \n    # Assign the result to the output variable\n    output = filtered_df\n    \n    return output\n\n```",
              "group_id": "ba582fc9-bb36-4c5d-a8e8-d35bda6389cd",
              "group_name": "Identify the channels with negative sales values by examining each day's sales data. Filter out the rows where any sales value is negative.",
              "stage": "Analyze"
            },
            {
              "type": "TABLE",
              "content": "https://s3.amazonaws.com/xxxtest/tmp_datasource_cache/code_result/clvl4cad2001q01l1m522hxlu/baf7d6d1-fb81-4fdb-bcdd-32923d214c7b.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241018T104617Z&X-Amz-SignedHeaders=host&X-Amz-Expires=599&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20241018%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9bcb5af552793f162e35f41d62fb9306cf90888924bfbdce81ea687265fddf83",
              "group_id": "ba582fc9-bb36-4c5d-a8e8-d35bda6389cd",
              "group_name": "Identify the channels with negative sales values by examining each day's sales data. Filter out the rows where any sales value is negative.",
              "stage": "Analyze"
            },
            {
              "type": "MESSAGE",
              "content": "- Sum the sales across all days for each channel.\n- Create a new DataFrame with the channel names and their corresponding total sales.",
              "group_id": "47183fd1-307b-4408-9986-e9238d952ec1",
              "group_name": "Calculate the overall sales trend for the identified channels with negative sales values. This involves summing up the sales across all days for each channel and analyzing the trend.",
              "stage": "Analyze"
            },
            {
              "type": "CODE",
              "content": "```python\n\nimport pandas as pd\n\ndef invoke(negative_sales_channels: pd.DataFrame) -> pd.DataFrame:\n    '''\n    negative_sales_channels: pd.DataFrame  negative_sales_channels.csv\n    '''\n    # Sum the sales across all days for each channel\n    total_sales = negative_sales_channels.iloc[:, 1:].sum(axis=1)\n    \n    # Create a new DataFrame with the channel names and their corresponding total sales\n    output = pd.DataFrame({\n        'Channel': negative_sales_channels.iloc[:, 0],\n        'Total Sales': total_sales\n    })\n    \n    return output\n\n```",
              "group_id": "47183fd1-307b-4408-9986-e9238d952ec1",
              "group_name": "Calculate the overall sales trend for the identified channels with negative sales values. This involves summing up the sales across all days for each channel and analyzing the trend.",
              "stage": "Analyze"
            },
            {
              "type": "TABLE",
              "content": "https://s3.amazonaws.com/xxxtest/tmp_datasource_cache/code_result/clvl4cad2001q01l1m522hxlu/10cffac2-8bf3-45f4-86e6-1ed8457329f2.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241018T104617Z&X-Amz-SignedHeaders=host&X-Amz-Expires=600&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20241018%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=c6f5b522d2ddceea730304b86a45d5f5165f05f9fda3c1d275d11e9022c1e7ac",
              "group_id": "47183fd1-307b-4408-9986-e9238d952ec1",
              "group_name": "Calculate the overall sales trend for the identified channels with negative sales values. This involves summing up the sales across all days for each channel and analyzing the trend.",
              "stage": "Analyze"
            },
            {
              "type": "MESSAGE",
              "content": "- Replace any negative sales values with zero in the data.\n- Sum the sales across all days for each channel.\n- Create a new data structure with the summed sales values.",
              "group_id": "6b93c2b1-8908-4c2b-afb2-2a81f2d24739",
              "group_name": "Calculate the overall sales trend for the same channels but excluding the negative sales values. This involves setting negative values to zero or removing them and then summing up the sales across all days for each channel.",
              "stage": "Analyze"
            },
            {
              "type": "CODE",
              "content": "```python\n\nimport pandas as pd\n\ndef invoke(negative_sales_channels: pd.DataFrame) -> pd.DataFrame:\n    '''\n    negative_sales_channels: pd.DataFrame  negative_sales_channels.csv\n    '''\n    # Replace negative values with zero\n    negative_sales_channels.iloc[:, 1:] = negative_sales_channels.iloc[:, 1:].clip(lower=0)\n    \n    # Sum the sales across all days for each channel\n    sales_sum = negative_sales_channels.iloc[:, 1:].sum(axis=1)\n    \n    # Create a new DataFrame with the summed sales values\n    output = pd.DataFrame({\n        'Channel': negative_sales_channels.iloc[:, 0],\n        'Total Sales': sales_sum\n    })\n    \n    return output\n\n```",
              "group_id": "6b93c2b1-8908-4c2b-afb2-2a81f2d24739",
              "group_name": "Calculate the overall sales trend for the same channels but excluding the negative sales values. This involves setting negative values to zero or removing them and then summing up the sales across all days for each channel.",
              "stage": "Analyze"
            },
            {
              "type": "TABLE",
              "content": "https://s3.amazonaws.com/xxxtest/tmp_datasource_cache/code_result/clvl4cad2001q01l1m522hxlu/f4c99616-dd7c-48b1-8a35-d3141d732c36.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241018T104617Z&X-Amz-SignedHeaders=host&X-Amz-Expires=600&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20241018%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=d21a8d939ab09547bc201754ba253ca6c0d1da5361752f2228237e3ff59be256",
              "group_id": "6b93c2b1-8908-4c2b-afb2-2a81f2d24739",
              "group_name": "Calculate the overall sales trend for the same channels but excluding the negative sales values. This involves setting negative values to zero or removing them and then summing up the sales across all days for each channel.",
              "stage": "Analyze"
            },
            {
              "type": "MESSAGE",
              "content": "- Merge the two datasets on the 'Channel' column to align sales data for comparison.\n- Calculate the difference in 'Total Sales' between the datasets for each channel.\n- Store the results, including channel name and calculated difference, in a new dataset.",
              "group_id": "3488f538-f7fc-4c0e-a265-b66e3a38d41e",
              "group_name": "Compare the sales trends with and without negative sales values to determine the impact of negative sales on the overall sales trend for the affected channels.",
              "stage": "Analyze"
            },
            {
              "type": "CODE",
              "content": "```python\n\nimport pandas as pd\n\ndef invoke(sales_trend_with_negatives: pd.DataFrame, sales_trend_without_negatives: pd.DataFrame) -> pd.DataFrame:\n    # Merge the two DataFrames on the 'Channel' column\n    merged_df = pd.merge(sales_trend_with_negatives, sales_trend_without_negatives, on='Channel', suffixes=('_with_negatives', '_without_negatives'))\n    \n    # Calculate the difference in 'Total Sales' between the two DataFrames\n    merged_df['Sales Difference'] = merged_df['Total Sales_without_negatives'] - merged_df['Total Sales_with_negatives']\n    \n    # Create a new DataFrame to store the results\n    output = merged_df[['Channel', 'Sales Difference']]\n    \n    return output\n\n```",
              "group_id": "3488f538-f7fc-4c0e-a265-b66e3a38d41e",
              "group_name": "Compare the sales trends with and without negative sales values to determine the impact of negative sales on the overall sales trend for the affected channels.",
              "stage": "Analyze"
            },
            {
              "type": "TABLE",
              "content": "https://s3.amazonaws.com/xxxtest/tmp_datasource_cache/code_result/clvl4cad2001q01l1m522hxlu/aaf4f2f7-e2db-4f2e-98ae-0bdd18f42333.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241018T104617Z&X-Amz-SignedHeaders=host&X-Amz-Expires=600&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20241018%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=19fcfe97c70bf40292b920ecbf0299c101e1de11e49b54fb8f62934b6e874f52",
              "group_id": "3488f538-f7fc-4c0e-a265-b66e3a38d41e",
              "group_name": "Compare the sales trends with and without negative sales values to determine the impact of negative sales on the overall sales trend for the affected channels.",
              "stage": "Analyze"
            },
            {
              "type": "MESSAGE",
              "content": "\n\n`Analyzing Conclusions` \n\n### The impact of negative sales values on overall sales trends\n\n#### Sales variance analysis\n\n",
              "group_id": "fd1a62e6-48cf-4ac1-8bac-025665444710",
              "group_name": "Conclusions",
              "stage": "Respond"
            },
            {
              "type": "TABLE",
              "content": "https://s3.amazonaws.com/xxxtest/tmp_datasource_cache/code_result/clvl4cad2001q01l1m522hxlu/aaf4f2f7-e2db-4f2e-98ae-0bdd18f42333.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241018T104617Z&X-Amz-SignedHeaders=host&X-Amz-Expires=600&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20241018%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=19fcfe97c70bf40292b920ecbf0299c101e1de11e49b54fb8f62934b6e874f52",
              "group_id": "fd1a62e6-48cf-4ac1-8bac-025665444710",
              "group_name": "Conclusions",
              "stage": "Respond"
            },
            {
              "type": "MESSAGE",
              "content": "\n\n- **Sales variance**：In all channels (including EC, JD, Tmall, WeChat, retail, corporate stores, outlets, and total), the sales difference is 0.0. This indicates that regardless of the presence of negative sales values, the sales trend has not changed.\n\n#### Conclusion and Insights\n- **The impact of negative sales values**：Based on the provided data, negative sales values have no impact on the overall sales trend of the affected channels, as the sales variance for all channels is 0.0.\n- **Data consistency**：The sales discrepancies across all channels are consistent, indicating that there are no anomalies or deviations caused by negative sales values during data processing or analysis.",
              "group_id": "fd1a62e6-48cf-4ac1-8bac-025665444710",
              "group_name": "Conclusions",
              "stage": "Respond"
            },
            {
              "type": "SOURCES",
              "content": [
                {
                  "source": "SalesByChannelByDay_Summary_Demo.xlsx",
                  "datasource_id": "cm2ej4wmo000001fcdkwbdrml",
                  "dataset_id": "cm2ej4vx900hp01l1o378zr9o",
                  "file_type": "xlsx",
                  "external_id": ""
                }
              ],
              "group_id": "",
              "group_name": "",
              "stage": "Respond"
            },
            {
              "type": "QUESTIONS",
              "content": [
                "Analyze the specific channels with negative sales values on different dates and discuss whether the sales strategies of these channels might lead to negative values.",
                "Study the long-term impact of negative sales values on overall sales trends and assess whether adjustments to data analysis methods are needed to more accurately reflect the actual situation.",
                "Investigate the source of negative sales values, whether they are related to returns, discounts, or other factors, and propose possible solutions to reduce the occurrence of negative values."
              ],
              "group_id": "-1",
              "stage": "Respond"
            }
          ]
        }
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||返回的任务记录的分页列表。|
|»» total_items|integer|true|none||返回的任务记录总数量。|
|»» page_number|integer|true|none||当前页面的页码。|
|»» page_size|integer|true|none||每页返回的记录数量。|
|»» records|[object]|true|none||当前页面返回的任务记录列表。|
|»»» question|object|true|none||您的提问（即提示词）。|
|»»»» blocks|[object]|true|none||构成整个问题的内容块列表。|
|»»»»» type|string|true|none||The content type of the question block. Possible values are:<br />- `MESSAGE`: The content is a piece of text.<br />- `CODE`: The content a code snippet in Markdown format.|
|»»»»» content|string|true|none||The block content. It is a piece of text when the `type` is `MESSAGE`, and a code snippet when the `type` is `CODE`.|
|»»» answer|object|true|none||MAXIR AI 的回答。|
|»»»» blocks|[[BlockDTO](#schemablockdto)]|true|none||MAXIR AI 的答案。|
|»»»»» type|string|true|none||答案块（Block）的内容类型。可能值为：<br /><br />- `MESSAGE`：表示内容是文本。<br />- `CODE`：表示内容是代码片段。<br />- `TABLE`：表示内容是表格。<br />- `IMAGE`：表示内容是图片。<br />- `SOURCE`：表示内容是答案块的参考来源。<br />- `QUESTIONS`：即 MAXIR AI 生成的建议问题，帮助引导您后续的数据探索和分析。|
|»»»»» content|string|true|none||答案块的内容，随 `type` 值而异：<br /><br />- 当 `type` 为 `MESSAGE` 时，内容为一段文本。<br />- 当 `type` 为 `CODE` 时，内容为 Markdown 格式表示的代码片段。<br />- 当 `type` 为 `TABLE` 时，内容为表格，包含如下构成参数：<br />    - `name`：`.csv` 文件的名称。<br />    - `url`：文件的 S3 Key 或 URL。<br />    - `expires_at`：`url` 的过期时间。如需保存表格方便后续使用，请确保在 URL 过期之前完成下载。<br />- 当 `type` 为 `IMAGE` 时，内容为一张图片，包含如下构成参数：<br />    - `name`：图片的名称。<br />    - `url`：图片的 S3 Key 或 URL。<br />    - `expires_at`：`url` 的过期时间。如需保存图片方便后续使用，请确保在 URL 过期之前完成下载。<br />- 当 `type` 为 `SOURCE` 时，内容为答案块的参考来源，包含如下构成参数：<br />    - `source`：数据源的文件名。<br />    - `datasource_id`：数据源 ID。<br />    - `dataset_id`：数据集 ID。<br />    - `file_type`：数据源的文件扩展名。<br />- 当 `type` 为 `QUESTIONS` 时，内容为 MAXIR AI 生成的建议问题，帮助您引导后续的数据探索与分析。|
|»»»»» group_id|string|true|none||答案块所在的分组 ID。|
|»»»»» group_name|string|true|none||答案块所在的分组名称。|
|»»»»» stage|string|true|none||MAXIR AI 生成答案的过程分为两个阶段：`Analyze` 和 `Respond`。  <br /><br />- `Analyze` 阶段的答案块并非最终答案的构成部分，为分析过程中的输出，旨在帮助您理解答案的生成方式。<br />- `Respond` 阶段的答案块是 MAXIR AI 基于您的问题生成的最终答复。|
|»»» job_id|string|true|none||任务 ID，即任务在当前会话中的唯一标识。|

#### 枚举值

|属性|值|
|---|---|
|type|MESSAGE|
|type|CODE|
|type|MESSAGE|
|type|CODE|
|type|TABLE|
|type|SOURCES|
|type|QUESTIONS|
|stage|Analyze|
|stage|Respond|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

# Dataset

## GET Get dataset overview

GET /v2/team/datasets/{id}/overview

获取数据集的基本信息，包括关键词、描述以及预生成的问题。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |目标数据集的 ID。|
|user_id|query|string| 是 |用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**id**: 目标数据集的 ID。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

> 返回示例

```json
{
  "code": {
    "code": 0
  },
  "data": {
    "id": "dset-cm5axptyyxxx298",
    "name": "sales_indicators_2024",
    "description": "A dataset comprising 373 travel bookings with 15 attributes, offering insights into booking patterns, pricing strategies, and more",
    "summary": "This dataset contains 373 travel bookings with 15 attributes, enabling analysis of booking trends, pricing strategies, and travel agency dynamics.",
    "exploration_questions": [
      "How does the booking price trend over time based on the BookingTimestamp?",
      "How does the average booking price change with respect to the TravelDate?",
      "Are there any significant outliers in the booking prices, and what might be causing them?",
      "How does the average price vary between one-way and round-trip bookings?"
    ],
    "keywords": [
      "Travel Bookings",
      "Booking Trends",
      "Travel Agencies"
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|[返回模型](#schema返回模型)|true|none||none|
|»» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||数据集对象。|
|»» id|string|true|none||数据集 ID，即数据集在项目中的唯一标识。|
|»» name|string|true|none||数据集名称。|
|»» description|string|true|none||数据集描述。|
|»» summary|string|true|none||数据集中数据源的概述。|
|»» exploration_questions|[string]|true|none||MAXIR AI 预生成的问题，可以帮助更好地探索数据集中的数据。|
|»» keywords|[string]|true|none||数据集关键词，可以帮助更好地理解数据集内容。|

## POST Create dataset

POST /v2/team/datasets

创建数据集。

数据集是相关数据源的集合。数据源可以是 Excel、CSV、PDF、Word、网页、Markdown、纯文本等格式。使用数据集可以更高效地访问和利用您的数据进行分析。您可以创建一个数据集，将所有用于特定分析的必要数据源存储其中。然后，在进行问答时，您只需将数据集与会话关联，即可访问数据集中的所有数据源。

> Body 请求参数

```json
{
  "name": "My dataset",
  "description": "my default dataset",
  "user_id": "tmm-dafasdfasdfasdf"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 |none|
|» name|body|string| 是 |数据集名称，至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|» description|body|string| 否 |数据集描述，至多可支持 5000 个字符。如果超过此限制，描述将被截断展示。|
|» user_id|body|string| 是 |用户 ID，即您在组织中的唯一身份标识。|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "dataset-adsdfasafdsfasdgasd"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||none|
|»» id|string|true|none||数据集 ID。<br /><br />如需 [上传](/api-reference/create-data-source) 数据源到该数据集或将其 [关联至任务](/api-reference/create-job) 进行数据分析和探索，请保存该数据集 ID。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET List datasets

GET /v2/team/datasets

返回数据集列表。

该接口仅会返回与您的 API 密钥所在同一项目中的数据集。

您可以指定搜索关键词，通过名称或描述进行数据集过滤。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|page_number|query|integer| 否 |分页返回的起始页码。如不指定，则使用默认值 `1`。|
|page_size|query|integer| 否 |每页返回的记录数量。如不指定，则使用默认值 `10`。|
|search|query|string| 否 |搜索关键词，最多支持 128 个字符。所有名称或描述中包含该关键词的数据集将被返回。|
|user_id|query|string| 是 |用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**search**: 搜索关键词，最多支持 128 个字符。所有名称或描述中包含该关键词的数据集将被返回。

如果省略此项，将列出项目中的所有数据集。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "page_number": 1,
    "page_size": 10,
    "total_items": 1,
    "records": [
      {
        "id": "dataset-dasfadsgadsgas",
        "name": "mysql",
        "description": "mysql databases"
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||返回的数据对象。|
|»» page_number|integer|true|none||当前页面的页码。|
|»» page_size|integer|true|none||每页返回的数据集数量。|
|»» total_items|integer|true|none||返回的数据集总数量。|
|»» records|[[DatasetDTO](#schemadatasetdto)]|true|none||当前页面返回的数据集列表。|
|»»» id|string|true|none||数据集 ID，即该数据集在项目中的唯一标识。|
|»»» name|string|true|none||数据集名称。|
|»»» description|string|true|none||数据集描述。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## DELETE Delete dataset

DELETE /v2/team/datasets/{id}

删除数据集。一旦删除，该数据集中的所有数据源也将被永久删除，且无法恢复。

> Body 请求参数

```json
{
  "user_id": "tmm-dafasdfasdfasdf"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |目标数据集 ID。您只能删除自己创建的数据集。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 |none|
|» user_id|body|string| 是 |用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**id**: 目标数据集 ID。您只能删除自己创建的数据集。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|false|none||操作成功则返回 null。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## POST Modify dataset

POST /v2/team/datasets/{id}

修改指定数据集的名称或描述。

> Body 请求参数

```json
{
  "name": "sales_data",
  "description": "sales data of all regions",
  "user_id": "tmm-dsadfdsafasdf"
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |目标数据集 ID。您只能修改自己创建的数据集。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 |none|
|» name|body|string| 否 |数据集的新名称，至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|» description|body|string| 否 |数据集的新描述，至多可支持 5000 个字符。如果超过此限制，描述将被截断展示。|
|» user_id|body|string| 是 |用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**id**: 目标数据集 ID。您只能修改自己创建的数据集。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**» name**: 数据集的新名称，至多可支持 128 个字符。如超过此限制，名称将被截断展示。

必须指定 `name` 或 `description` 中的至少一个。

**» description**: 数据集的新描述，至多可支持 5000 个字符。如果超过此限制，描述将被截断展示。

必须指定 `name` 或 `description` 中的至少一个。

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||操作成功则返回 null。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET Get status summary of data sources in dataset

GET /v2/team/datasets/{id}/status

此接口会计算并返回指定数据集中处于每个状态的数据源数量。您可以使用该接口来检查数据集中的所有数据源是否已完成同步并可用于数据分析任务。

只有当返回中的 `invalid_count` 和 `synching_count` 均为 `0`时，才表示该数据集中的所有数据源都能用于问答。否则，MAXIR AI 将无法使用未完成同步的数据源进行数据分析与探索。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|id|path|string| 是 |需要了解数据源状态的数据集 ID。|
|user_id|query|string| 是 |用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 |您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "synched_count": 5,
    "invalid_count": 0,
    "synching_count": 0
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||处于每个状态的数据源数量。<br /><br />请注意，只有当 `invalid_count` 和 `synching_count` 都为 `0` 时，使用 MAXIR AI 进行问答时才能使用数据集中的所有数据源。否则，MAXIR AI 将无法使用未完成同步的数据源进行数据分析与探索。|
|»» synched_count|integer|true|none||已同步的数据源数量。|
|»» invalid_count|integer|true|none||同步失败的数据源数量。|
|»» synching_count|integer|true|none||等待同步或正在同步的数据源数量。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

# Data source

## POST Create data source

POST /v2/team/datasets/{id}/datasources

在指定数据集中创建数据源。您只能在自己创建的数据集中创建数据源。

数据源可以为以下任意格式：**.csv**、**.tsv**、**.md**、**.mdx**、**.json**、**.txt**、**.pdf**、**.pptx**、**.ppt**、**.doc**、**.docx**、**.xls** 或 **.xlsx**。

> Body 请求参数

```json
{
  "name": "test.csv",
  "type": "FILE",
  "user_id": "tmm-dsfasdfasdfa",
  "url": "https://s3.amazonaws.com/xxxtest/user/clvl4cad2001q01l1m522hxlu/upload/f9773f1e-cd68-489a-8121-d566ca9218b1.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240924T143419Z&X-Amz-SignedHeaders=host&X-Amz-Expires=599&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20240924%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9ca0c58d508926a5811818041d557ffb53c64025dae94c0855280d457c7089a2"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|path|string| 是 ||目标数据集 ID。|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 ||none|
|» name|body|string| 是 ||数据源名称，需包含文件扩展名（例如 `example.csv`），至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|» type|body|string| 是 | FILE|数据源的类型。设置为 **FILE**。|
|» url|body|string| 否 ||文件 URL，用于公网访问该文件。|
|» file_object_key|body|string| 否 ||您本地上传文件的对象存储路径。|
|» user_id|body|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**id**: 目标数据集 ID。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**» url**: 文件 URL，用于公网访问该文件。

`url` 和 `file_object_key` 之间必须且只能指定其一。

仅支持以下扩展名的文件：.csv、.tsv、.md、.mdx、.json、.txt、.pdf、.pptx、.ppt、.doc、.docx、.xls 或 .xlsx。

**» file_object_key**: 您本地上传文件的对象存储路径。

`url` 和 `file_object_key` 之间必须且只能指定其一。

支持的文件扩展名包括：**.csv**、**.tsv**、**.md**、**.mdx**、**.json**、**.txt**、**.pdf**、**.pptx**、**.ppt**、**.doc**、**.docx**、**.xls** 或 **.xlsx**。

如何获取文件的 `file_object_key`：

当使用 [Upload file](/api-reference/upload-file) 接口完成文件上传后，会返回该文件的`file_object_key`。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "datasource-cadsgfsdagasgadsg",
    "dataset_id": "dataset-dagasdgasgasg",
    "name": "test.csv",
    "type": "FILE",
    "status": "synching"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||数据源对象。|
|»» id|string|true|none||数据源 ID，即该数据源在数据集中的唯一标识。|
|»» dataset_id|string|true|none||数据源所在的数据集 ID。|
|»» name|string|true|none||数据源名称。|
|»» type|string|true|none||数据源类型，固定为 **FILE**。|
|»» status|string|true|none||数据源的处理状态。可能值为：<br /><br />- `invalid`：等待处理中。<br />- `synching`：正在处理中。<br />- `synched`：已成功同步。|

#### 枚举值

|属性|值|
|---|---|
|type|FILE|
|status|synching|
|status|synched|
|status|invalid|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET List data sources

GET /v2/team/datasets/{id}/datasources

返回指定数据集中的数据源列表。使用此接口时，请注意：

- 确保指定数据集和您的 API Key 归属于同一项目。
- 如需查看您在该项目中有访问权限的数据集，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|path|string| 是 ||目标数据集 ID。|
|page_number|query|integer| 否 ||分页返回的起始页码。如不指定，则使用默认值 `1`。|
|page_size|query|integer| 否 ||每页返回的记录数量。如不指定，则使用默认值 `10`。|
|status|query|string| 否 ||数据源状态。指定该参数后，只有处于指定状态的数据源才会被返回。可选值包括：|
|user_id|query|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**id**: 目标数据集 ID。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**status**: 数据源状态。指定该参数后，只有处于指定状态的数据源才会被返回。可选值包括：

- `invalid`：等待处理中。
- `synching`：正在处理中。
- `synched`：已成功同步。

如果未指定，将返回所有数据源。

可以通过英文逗号分隔的列表指定多个状态，匹配任何状态的数据源将被返回。

#### 枚举值

|属性|值|
|---|---|
|status|synching|
|status|invalid|
|status|synched|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "total_items": 1,
    "page_size": 10,
    "page_number": 1,
    "records": [
      {
        "id": "datasource-cadsgfsdagasgadsg",
        "dataset_id": "dataset-dagasdgasgasg",
        "name": "test.csv",
        "type": "FILE",
        "status": "synching"
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||返回的数据源分页列表。|
|»» total_items|integer|true|none||返回的数据源总数量。|
|»» page_size|integer|true|none||每页返回的数据源数量。|
|»» page_number|integer|true|none||当前页面的页码。|
|»» records|[object]|true|none||当前页面返回的数据源列表。|
|»»» id|string|true|none||数据源 ID，即该数据源在数据集中的唯一标识。|
|»»» dataset_id|string|true|none||数据源所在的数据集 ID。|
|»»» name|string|true|none||数据源名称。|
|»»» type|string|true|none||数据源类型，固定为 **FILE**。|
|»»» status|string|true|none||数据源的处理状态。可能值为：<br /><br />- `invalid`：等待处理中。<br />- `synching`：正在处理中。<br />- `synched`：已成功同步。|

#### 枚举值

|属性|值|
|---|---|
|type|FILE|
|status|synching|
|status|synched|
|status|invalid|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## DELETE Delete data source

DELETE /v2/team/datasets/{dataset_id}/datasources/{datasource_id}

从指定的数据集中删除数据源。一旦删除，数据源将无法恢复。

您只能删除自己创建的数据集中的数据源。

> Body 请求参数

```json
{
  "user_id": "tmm-dafasdfasdfasdf"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|dataset_id|path|string| 是 ||目标数据集 ID。|
|datasource_id|path|string| 是 ||要删除的数据源 ID。|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 ||none|
|» user_id|body|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**dataset_id**: 目标数据集 ID。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**datasource_id**: 要删除的数据源 ID。

如需查询指定数据集中的数据源，请调用 [GET /v2/team/datasets/{id}/datasources](/api-reference/list-data-sources) 接口。

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object¦null|false|none||操作成功则返回 null。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## GET Get data source

GET /v2/team/datasets/{dataset_id}/datasources/{datasource_id}

获取指定数据源信息。

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|dataset_id|path|string| 是 ||目标数据源所在的数据集 ID。|
|datasource_id|path|string| 是 ||目标数据源 ID。|
|user_id|query|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

#### 详细说明

**dataset_id**: 目标数据源所在的数据集 ID。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**datasource_id**: 目标数据源 ID。

如需查询指定数据集中的数据源，请调用 [GET /v2/team/datasets/{id}/datasources](/api-reference/list-data-sources) 接口。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "datasource-cadsgfsdagasgadsg",
    "dataset_id": "dataset-dagasdgasgasg",
    "name": "test.csv",
    "type": "FILE",
    "status": "synching"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||数据源对象。|
|»» id|string|true|none||数据源 ID，即该数据源在数据集中的唯一标识。|
|»» dataset_id|string|true|none||数据源所在的数据集 ID。|
|»» name|string|true|none||数据源名称。|
|»» type|string|true|none||数据源类型，固定为 **FILE**。|
|»» status|string|true|none||数据源的处理状态。可能值为：<br /><br />- `invalid`：等待处理中。<br />- `synching`：正在处理中。<br />- `synched`：已成功同步。|

#### 枚举值

|属性|值|
|---|---|
|type|FILE|
|status|synching|
|status|synched|
|status|invalid|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## POST Create data source without specifying a dataset

POST /v2/team/datasources

该接口用于在不指定数据集的情况下，直接创建数据源。

调用此接口时，MAXIR AI 会自动为该数据源创建一个数据集。请保存返回中的数据集 ID，便于后续操作，如 [关联数据集至任务](/api-reference/create-job) 进行数据分析与探索。

> Body 请求参数

```json
{
  "name": "test.csv",
  "type": "FILE",
  "user_id": "tmm-dafasdfasdfasdf",
  "file_object_key": "/tmp/sdgsagdsgsadgasdg"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|[DataSourceConfig](#schemadatasourceconfig)| 否 ||none|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "datasource-cadsgfsdagasgadsg",
    "dataset_id": "dataset-dagasdgasgasg",
    "name": "test.csv",
    "type": "FILE",
    "status": "synching"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||数据源对象。|
|»» id|string|true|none||数据源 ID，即该数据源在数据集中的唯一标识。|
|»» dataset_id|string|true|none||数据源所在的数据集 ID。|
|»» name|string|true|none||数据源名称。|
|»» type|string|true|none||数据源类型，固定为 **FILE**。|
|»» status|string|true|none||数据源的处理状态。可能值为：<br /><br />- `invalid`：等待处理中。<br />- `synching`：正在处理中。<br />- `synched`：已成功同步。|

#### 枚举值

|属性|值|
|---|---|
|type|FILE|
|status|synching|
|status|synched|
|status|invalid|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

## POST Presign data source 

POST /v2/team/datasets/{dataset_id}/datasources/{datasource_id}/presign

该接口用于为指定数据源生成一个预签名 URL（Presigned URL），从而您可以通过该 URL 下载对应的数据源。

预签名 URL 具有有效期，请确保在 URL 过期之前完成数据源的下载。

> Body 请求参数

```json
{
  "expires_in": 600,
  "user_id": "tmm-dafasdfasdfasdf"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|dataset_id|path|string| 是 ||目标数据源所在的数据集 ID。|
|datasource_id|path|string| 是 ||目标数据源 ID。|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 ||none|
|» expires_in|body|integer| 否 ||预签名 URL 的过期时间，单位为秒（s）。最小值为 `60`，默认值为 `600`。|
|» user_id|body|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**dataset_id**: 目标数据源所在的数据集 ID。

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**datasource_id**: 目标数据源 ID。

如需查询指定数据集中的数据源，请调用 [GET /v2/team/datasets/{id}/datasources](/api-reference/list-data-sources) 接口。

> 返回示例

```json
{
  "code": 0,
  "data": {
    "presigned_url": "string",
    "expires_at": "2024-11-13T14:15:22.123Z"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||返回的数据对象。|
|»» presigned_url|string|true|none||预签名 URL，用于下载对应数据源。|
|»» expires_at|string(date-time)|true|none||预签名 URL 的过期日期和时间。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

# File

## POST Upload local file

POST /v2/team/file/upload-datasource

上传本地文件。支持的文件格式包括：**.csv**、**.tsv**、**.md**、**.mdx**、**.json**、**.txt**、**.pdf**、**.pptx**、**.ppt**、**.doc**、**.docx**、**.xls** 或 **.xlsx**。

您可以使用此接口上传本地文件，然后使用获得的 `file_object_key` 来创建数据源。详细操作指南，请参考 [如何上传本地文件](/developer-guides/upload-file)。

> Body 请求参数

```yaml
file: ""
user_id: ""

```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 ||none|
|» file|body|string(binary)| 是 ||要上传的文件。该字段必填，且应当包含文件数据。例如，`--form 'file=@"/Users/jiaoqi/Downloads/0f9a7ebd-7a2a-454a-8cd9-96accffa3107.csv"'`。|
|» user_id|body|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "file_object_key": "/tmp/sdgsagdsgsadgasdg.csv"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||返回的数据对象。|
|»» file_object_key|string|true|none||文件的对象存储路径。|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

# Job

## POST Create job

POST /v2/team/jobs

分析或探索您的数据。您可以通过此接口根据您的数据进行提问，立即获取洞察。

在 MAXIR AI 中，**任务（Job）** 即 MAXIR AI 根据您的请求（例如提示词或其他工作流）而生成并执行的问答过程。

> Body 请求参数

```json
{
  "session_id": "cxxdgegeegeg3433fff",
  "user_id": "tmm-dafasdfasdfasdf",
  "stream": true,
  "question": "Hello World",
  "dataset_id": "cm1gjmg8e0057r3x22v1fdu8m",
  "datasource_ids": [
    "cm1gjmmoo0001h0x24uk1xgu9"
  ],
  "output_language": "AUTO",
  "job_mode": "AUTO"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|x-pd-external-trace-id|header|string| 否 ||您本地系统中设置的 Trace ID，至多支持 128 个字符。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|
|body|body|object| 否 ||none|
|» session_id|body|string| 是 ||会话 ID。|
|» stream|body|boolean| 否 ||是否使用流式返回。如果设置为 `true`，MAXIR AI 将实时向客户端发送回答更新，持续传输实时可用的数据。如果设置为 `false`，则在整个回答完成后，一次性返回完整的响应。|
|» question|body|string| 是 ||您的问题（即提示词）。|
|» dataset_id|body|string| 否 ||任务关联的数据集 ID。 |
|» datasource_ids|body|[string]| 否 ||指定在任务中使用的数据源的 ID。最多可以指定 1,000 个数据源。|
|» output_language|body|string| 否 ||MAXIR AI 的回复语言。例如，当设置为 `ZH-CN` 时，则 MAXIR AI 以简体中文回复。可选值包括：|
|» job_mode|body|string| 否 ||任务类型。可选值包括：|
|» user_id|body|string| 是 ||用户 ID，即您在组织中的唯一身份标识。|

#### 详细说明

**» session_id**: 会话 ID。

如需查看项目中存在的会话，请调用 [GET /v2team/sessions](/api-reference/list-sessions) 接口。

**» stream**: 是否使用流式返回。如果设置为 `true`，MAXIR AI 将实时向客户端发送回答更新，持续传输实时可用的数据。如果设置为 `false`，则在整个回答完成后，一次性返回完整的响应。

如不指定，则使用默认值 `false`。

关于如何理解流式返回的内容，请参考 [流式返回中的内容说明](/api-reference/streaming#content-description)。

**» dataset_id**: 任务关联的数据集 ID。 

如需查询您有访问权限的数据集列表，请调用 [GET /v2/team/datasets](/api-reference/list-datasets) 接口。

**» output_language**: MAXIR AI 的回复语言。例如，当设置为 `ZH-CN` 时，则 MAXIR AI 以简体中文回复。可选值包括：

- `AUTO`：根据提示词自动识别
- `EN`：英语
- `ES`：西班牙语
- `AR`：阿拉伯语
- `PT`：葡萄牙语
- `ID`：印尼语
- `JA`：日语
- `RU`：俄语
- `HI`：印地语
- `FR`：法语
- `DE`：德语
- `VI`：越南语
- `TR`：土耳其语
- `PL`：波兰语
- `IT`：意大利语
- `KO`：韩语
- `ZH-CN`：简体中文
- `ZH-TW`：繁体中文

**» job_mode**: 任务类型。可选值包括：

- `AUTO`：MAXIR AI 根据你的提问进行意图判断，决定该任务为数据分析任务或信息检索任务。
- `DATA_ANALYTICS`：MAXIR AI 会根据你的输入进行数据分析。

如不指定，则使用会话的 `job_mode` 设置。

#### 枚举值

|属性|值|
|---|---|
|» output_language|AUTO|
|» output_language|EN|
|» output_language|ES|
|» output_language|AR|
|» output_language|PT|
|» output_language|ID|
|» output_language|JA|
|» output_language|RU|
|» output_language|HI|
|» output_language|FR|
|» output_language|DE|
|» output_language|VI|
|» output_language|TR|
|» output_language|PL|
|» output_language|IT|
|» output_language|KO|
|» output_language|ZH-CN|
|» output_language|ZH-TW|
|» job_mode|AUTO|
|» job_mode|DATA_ANALYTICS|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "job_id": "job-cm3ikdeuj02zk01l1yeuirt77",
    "blocks": [
      {
        "type": "CODE",
        "content": "```python\n\nimport pandas as pd\n\ndef invoke(input_0: pd.DataFrame) -> pd.DataFrame:\n    '''\n    input_0: pd.DataFrame  makeovermonday-a-century-of-global-deaths-from-disasters_decadal-deaths-disasters-type.csv\n    '''\n    # Group by 'Year' and sum the deaths for each type of disaster\n    aggregated_data = input_0.groupby('Year').sum().reset_index()\n    \n    # Select only the columns related to deaths\n    death_columns = [\n        'Deaths - Drought (decadal)', 'Deaths - Flood (decadal)', \n        'Deaths - Earthquake (decadal)', 'Deaths - Extreme weather (decadal)', \n        'Deaths - Extreme temperature (decadal)', 'Deaths - Volcanic activity (decadal)', \n        'Deaths - Wildfire (decadal)', 'Deaths - Glacial lake outburst flood (decadal)', \n        'Deaths - Dry mass movement (decadal)', 'Deaths - Wet mass movement (decadal)', \n        'Deaths - Fog (decadal)'\n    ]\n    \n    # Create a new DataFrame with the aggregated results\n    output = aggregated_data[['Year'] + death_columns]\n    \n    # Rename columns to be more descriptive\n    output.columns = ['Decade'] + [col.replace('Deaths - ', '').replace(' (decadal)', '') for col in death_columns]\n    \n    return output\n\n```",
        "group_id": "33063572-6e88-4912-8e2d-4166bcc8caee",
        "group_name": "Analyze the dataset to observe the trend of deaths caused by different types of natural disasters over the past century. This involves aggregating the data by decade and calculating the total number of deaths for each type of disaster to identify any changes in trends.",
        "stage": "Analyze"
      },
      {
        "type": "TABLE",
        "content": {
          "url": "https://static.xxx.ai/tmp_datasource_cache/code_result/cm37bchx106e301l1v9yf67yc/e24b6a5f-fdb8-48ca-ae35-dc91ac8e8ef7.csv",
          "name": "trend_data.csv",
          "expires_at": "2024-11-21T09:56:34.290544Z"
        },
        "group_id": "33063572-6e88-4912-8e2d-4166bcc8caee",
        "group_name": "Analyze the dataset to observe the trend of deaths caused by different types of natural disasters over the past century. This involves aggregating the data by decade and calculating the total number of deaths for each type of disaster to identify any changes in trends.",
        "stage": "Analyze"
      },
      {
        "type": "IMAGE",
        "content": {
          "url": "https://static.xxx.ai/tmp_datasource_cache/code_result/cm37bchx106e301l1v9yf67yc/81b75a33-a223-4954-9680-9f397872c8ad.png",
          "name": "Trend of Deaths from Natural Disasters Over the Century",
          "expires_at": "2024-11-21T09:56:34.290544Z"
        },
        "group_id": "7501680b-5879-441b-bd96-f58b1029ae17",
        "group_name": "Visualize the trend data to show how the number of deaths from different types of natural disasters has changed over the past century. Use line charts to represent the trends for each disaster type, which will help in understanding the impact of measures and technological advancements on reducing deaths.",
        "stage": "Analyze"
      },
      {
        "type": "MESSAGE",
        "content": "\n\n`Analyzing Conclusions` \n\n### Analysis of Trends in the Number of Deaths from Natural Disasters \n\n#### Data Analysis\n\n",
        "group_id": "b842aca7-6fd5-4190-85fa-97085e473877",
        "group_name": "Conclusions",
        "stage": "Respond"
      },
      {
        "type": "TABLE",
        "content": {
          "url": "https://static.xxx.ai/tmp_datasource_cache/code_result/cm37bchx106e301l1v9yf67yc/e24b6a5f-fdb8-48ca-ae35-dc91ac8e8ef7.csv",
          "name": "trend_data.csv",
          "expires_at": "2024-11-21T09:56:34.290544Z"
        },
        "group_id": "b842aca7-6fd5-4190-85fa-97085e473877",
        "group_name": "Conclusions",
        "stage": "Respond"
      },
      {
        "type": "MESSAGE",
        "content": "\n\n- **Droughts and Floods**: In the early 20th century, droughts and floods caused extremely high death tolls, particularly during the 1920s and 1930s.\n- **Earthquakes and Extreme Weather**: Earthquakes and extreme weather also led to significant death tolls throughout the century, especially in the 1970s and 1990s.\n- **Extreme Temperatures and Volcanic Activity**: These disasters had relatively lower death tolls, but in certain decades, such as the 2000s, deaths caused by extreme temperatures increased.\n\n#### Trend Visualization\n\n",
        "group_id": "b842aca7-6fd5-4190-85fa-97085e473877",
        "group_name": "Conclusions",
        "stage": "Respond"
      },
      {
        "type": "IMAGE",
        "content": {
          "url": "https://static.xxx.ai/tmp_datasource_cache/code_result/cm37bchx106e301l1v9yf67yc/81b75a33-a223-4954-9680-9f397872c8ad.png",
          "name": "Trend of Deaths from Natural Disasters Over the Century",
          "expires_at": "2024-11-21T09:56:34.290544Z"
        },
        "group_id": "b842aca7-6fd5-4190-85fa-97085e473877",
        "group_name": "Conclusions",
        "stage": "Respond"
      },
      {
        "type": "MESSAGE",
        "content": "\n\n- **Overall Trend**: The chart shows that although certain decades experienced spikes in death tolls caused by natural disasters, the overall trend is declining.\n- **Impact of Technology and Measures**: Over time, advancements in technology and the implementation of disaster prevention measures are likely key factors in reducing death tolls.\n\n#### Conclusions and Insights\n- **Technological Advancements**: Modern technological progress, such as improved early warning systems and better construction techniques, may have reduced the fatalities caused by earthquakes and extreme weather.\n- **Disaster Prevention Measures**: The enhancement of disaster prevention measures and emergency response capabilities on a global scale has likely contributed to the decreased fatality rates of natural disasters.",
        "group_id": "b842aca7-6fd5-4190-85fa-97085e473877",
        "group_name": "Conclusions",
        "stage": "Respond"
      },
      {
        "type": "SOURCES",
        "content": [
          {
            "source": "makeovermonday-a-century-of-global-deaths-from-disasters_decadal-deaths-disasters-type.csv",
            "datasource_id": "clxin6l9200oo01l1457bolx3",
            "dataset_id": "clxin6l8400ok01l1ff2m0s25",
            "file_type": "csv"
          }
        ],
        "group_id": "",
        "group_name": "",
        "stage": "Respond"
      },
      {
        "type": "QUESTIONS",
        "content": [
          "Analyze the trends in death tolls from different types of natural disasters over the past century and explore which disaster types have shown the most significant reduction in fatalities.",
          "Study the technological advancements and measures in responding to natural disasters across different regions globally, and analyze how these differences have influenced changes in death tolls in each region.",
          "Explore how future technological advancements and policy measures could further reduce fatalities caused by natural disasters, and assess their feasibility and potential impacts."
        ],
        "group_id": "-1",
        "stage": "Respond"
      }
    ]
  }
}
```

```json
{
  "code": 210021,
  "msg": "Job quota exceeded"
}
```

```json
{
  "code": 1003,
  "msg": "insufficient.authentication"
}
```

```json
{
  "code": 210020,
  "msg": "Something went wrong during job execution. Please try again."
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|none|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|
|» data|object|true|none||任务对象。|
|»» job_id|string|true|none||任务 ID，即会话中该任务的唯一标识。|
|»» blocks|[[BlockDTO](#schemablockdto)]|true|none||构成完整答案的答案块列表。|
|»»» type|string|true|none||答案块（Block）的内容类型。可能值为：<br /><br />- `MESSAGE`：表示内容是文本。<br />- `CODE`：表示内容是代码片段。<br />- `TABLE`：表示内容是表格。<br />- `IMAGE`：表示内容是图片。<br />- `SOURCE`：表示内容是答案块的参考来源。<br />- `QUESTIONS`：即 MAXIR AI 生成的建议问题，帮助引导您后续的数据探索和分析。|
|»»» content|string|true|none||答案块的内容，随 `type` 值而异：<br /><br />- 当 `type` 为 `MESSAGE` 时，内容为一段文本。<br />- 当 `type` 为 `CODE` 时，内容为 Markdown 格式表示的代码片段。<br />- 当 `type` 为 `TABLE` 时，内容为表格，包含如下构成参数：<br />    - `name`：`.csv` 文件的名称。<br />    - `url`：文件的 S3 Key 或 URL。<br />    - `expires_at`：`url` 的过期时间。如需保存表格方便后续使用，请确保在 URL 过期之前完成下载。<br />- 当 `type` 为 `IMAGE` 时，内容为一张图片，包含如下构成参数：<br />    - `name`：图片的名称。<br />    - `url`：图片的 S3 Key 或 URL。<br />    - `expires_at`：`url` 的过期时间。如需保存图片方便后续使用，请确保在 URL 过期之前完成下载。<br />- 当 `type` 为 `SOURCE` 时，内容为答案块的参考来源，包含如下构成参数：<br />    - `source`：数据源的文件名。<br />    - `datasource_id`：数据源 ID。<br />    - `dataset_id`：数据集 ID。<br />    - `file_type`：数据源的文件扩展名。<br />- 当 `type` 为 `QUESTIONS` 时，内容为 MAXIR AI 生成的建议问题，帮助您引导后续的数据探索与分析。|
|»»» group_id|string|true|none||答案块所在的分组 ID。|
|»»» group_name|string|true|none||答案块所在的分组名称。|
|»»» stage|string|true|none||MAXIR AI 生成答案的过程分为两个阶段：`Analyze` 和 `Respond`。  <br /><br />- `Analyze` 阶段的答案块并非最终答案的构成部分，为分析过程中的输出，旨在帮助您理解答案的生成方式。<br />- `Respond` 阶段的答案块是 MAXIR AI 基于您的问题生成的最终答复。|

#### 枚举值

|属性|值|
|---|---|
|type|MESSAGE|
|type|CODE|
|type|TABLE|
|type|SOURCES|
|type|QUESTIONS|
|stage|Analyze|
|stage|Respond|

### 返回头部 Header

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-pd-trace-id|string||MAXIR AI 返回的 Trace ID。当请求发生错误时，可以将此 ID 提供给 MAXIR AI 团队，协助进行故障排查。|

# 数据模型

<h2 id="tocS_CreateSessionRequest">CreateSessionRequest</h2>

<a id="schemacreatesessionrequest"></a>
<a id="schema_CreateSessionRequest"></a>
<a id="tocScreatesessionrequest"></a>
<a id="tocscreatesessionrequest"></a>

```json
{
  "name": "string",
  "output_language": "AUTO",
  "job_mode": "AUTO",
  "max_contextual_job_history": 0,
  "agent_id": "DATA_ANALYSIS_AGENT",
  "user_id": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|name|string|true|none||会话名称，至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|output_language|string|false|none||MAXIR AI 的回复语言。例如，当设置为 `EN` 时，则 MAXIR AI 使用英语进行回复。如不指定，将使用默认值 `AUTO`，即 MAXIR AI 会根据提示词自动选择合适的回复语言。可选值包括：<br /><br />- `AUTO`：根据提示词自动识别<br />- `EN`：英语<br />- `ES`：西班牙语<br />- `AR`：阿拉伯语<br />- `PT`：葡萄牙语<br />- `ID`：印尼语<br />- `JA`：日语<br />- `RU`：俄语<br />- `HI`：印地语<br />- `FR`：法语<br />- `DE`：德语<br />- `VI`：越南语<br />- `TR`：土耳其语<br />- `PL`：波兰语<br />- `IT`：意大利语<br />- `KO`：韩语<br />- `ZH-CN`：简体中文<br />- `ZH-TW`：繁体中文|
|job_mode|string|false|none||任务类型。可选值包括：<br /><br />- `AUTO`：MAXIR AI 根据你的提问进行意图判断，决定该任务为数据分析任务或信息检索任务。<br />- `DATA_ANALYTICS`：MAXIR AI 会根据你的输入进行数据分析。<br /><br />如不指定，则采用默认值 `AUTO`。如果您明确地想要进行数据分析，我们建议您将值设置为 **DATA_ANALYTICS**，从而 MAXIR AI 可以跳过意图识别步骤，加快问题处理速度。|
|max_contextual_job_history|integer|false|none||作为下一个任务上下文的历史任务数，取值范围为 `0` 到 `10`，默认值为 `10`。如设置为 `0`，则当前任务将不使用任何历史任务作为上下文信息。|
|agent_id|string|false|none||AI 智能体的 ID。该参数为保留参数，无需制定或设置为 **DATA_ANALYSIS_AGENT**。|
|user_id|string|true|none||用户 ID，即您在组织中的唯一身份标识。|

#### 枚举值

|属性|值|
|---|---|
|output_language|AUTO|
|output_language|EN|
|output_language|ES|
|output_language|AR|
|output_language|PT|
|output_language|ID|
|output_language|JA|
|output_language|RU|
|output_language|HI|
|output_language|FR|
|output_language|DE|
|output_language|VI|
|output_language|TR|
|output_language|PL|
|output_language|IT|
|output_language|KO|
|output_language|ZH-CN|
|output_language|ZH-TW|
|job_mode|AUTO|
|job_mode|DATA_ANALYTICS|
|agent_id|DATA_ANALYSIS_AGENT|

<h2 id="tocS_SessionDTO">SessionDTO</h2>

<a id="schemasessiondto"></a>
<a id="schema_SessionDTO"></a>
<a id="tocSsessiondto"></a>
<a id="tocssessiondto"></a>

```json
{
  "id": "string",
  "name": "string",
  "output_language": "AUTO",
  "job_mode": "AUTO",
  "max_contextual_job_history": 0,
  "agent_id": "DATA_ANALYSIS_AGENT"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||会话 ID，会话在当前项目中的唯一标识。|
|name|string|true|none||会话名称。如名称长度超过 128 个字符，将仅返回前 128 个字符。|
|output_language|string|false|none||MAXIR AI 的返回语言。可能值包括：<br /><br />- `AUTO`：根据提示词自动识别<br />- `EN`：英语<br />- `ES`：西班牙语<br />- `AR`：阿拉伯语<br />- `PT`：葡萄牙语<br />- `ID`：印尼语<br />- `JA`：日语<br />- `RU`：俄语<br />- `HI`：印地语<br />- `FR`：法语<br />- `DE`：德语<br />- `VI`：越南语<br />- `TR`：土耳其语<br />- `PL`：波兰语<br />- `IT`：意大利语<br />- `KO`：韩语<br />- `ZH-CN`：简体中文<br />- `ZH-TW`：繁体中文|
|job_mode|string|false|none||任务类型。可能值包括：<br /><br />- `AUTO`：MAXIR AI 根据您的提问进行意图判断，决定任务是数据分析任务还是信息检索任务。<br />- `DATA_ANALYTICS`：MAXIR AI 根据您的输入进行数据分析。|
|max_contextual_job_history|integer|false|none||在会话中保留作为下一个任务上下文的任务数量，取值范围为 `0` 到 `10`，默认值为 `10`。值为 `0` 时表示会话中的任务在执行时不会使用历史任务执行结果作为上下文信息。|
|agent_id|string|false|none||AI 智能体的 ID。该参数为保留参数，无实际意义，请忽略。|

#### 枚举值

|属性|值|
|---|---|
|output_language|AUTO|
|output_language|EN|
|output_language|ES|
|output_language|AR|
|output_language|PT|
|output_language|ID|
|output_language|JA|
|output_language|RU|
|output_language|HI|
|output_language|FR|
|output_language|DE|
|output_language|VI|
|output_language|TR|
|output_language|PL|
|output_language|IT|
|output_language|KO|
|output_language|ZH-CN|
|output_language|ZH-TW|
|job_mode|AUTO|
|job_mode|DATA_ANALYTICS|
|agent_id|DATA_ANALYSIS_AGENT|

<h2 id="tocS_DatasourceDTO">DatasourceDTO</h2>

<a id="schemadatasourcedto"></a>
<a id="schema_DatasourceDTO"></a>
<a id="tocSdatasourcedto"></a>
<a id="tocsdatasourcedto"></a>

```json
{
  "id": "string",
  "dataset_id": "string",
  "name": "string",
  "type": "FILE",
  "status": "synching"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||数据源 ID，即该数据源在数据集中的唯一标识。|
|dataset_id|string|true|none||数据源所在的数据集 ID。|
|name|string|true|none||数据源名称。|
|type|string|true|none||数据源类型，固定为 **FILE**。|
|status|string|true|none||数据源的处理状态。可能值为：<br /><br />- `invalid`：等待处理中。<br />- `synching`：正在处理中。<br />- `synched`：已成功同步。|

#### 枚举值

|属性|值|
|---|---|
|type|FILE|
|status|synching|
|status|synched|
|status|invalid|

<h2 id="tocS_DatasetDTO">DatasetDTO</h2>

<a id="schemadatasetdto"></a>
<a id="schema_DatasetDTO"></a>
<a id="tocSdatasetdto"></a>
<a id="tocsdatasetdto"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||数据集 ID，即该数据集在项目中的唯一标识。|
|name|string|true|none||数据集名称。|
|description|string|true|none||数据集描述。|

<h2 id="tocS_返回模型">返回模型</h2>

<a id="schema返回模型"></a>
<a id="schema_返回模型"></a>
<a id="tocS返回模型"></a>
<a id="tocs返回模型"></a>

```json
{
  "code": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer|true|none||状态码。**0** 表示操作成功。其它值则表示操作失败。如需进行错误排查，请参阅 [错误码](/introduction/error-codes)。|

<h2 id="tocS_BlockDTO">BlockDTO</h2>

<a id="schemablockdto"></a>
<a id="schema_BlockDTO"></a>
<a id="tocSblockdto"></a>
<a id="tocsblockdto"></a>

```json
{
  "type": "MESSAGE",
  "content": "string",
  "group_id": "string",
  "group_name": "string",
  "stage": "Analyze"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|type|string|true|none||答案块（Block）的内容类型。可能值为：<br /><br />- `MESSAGE`：表示内容是文本。<br />- `CODE`：表示内容是代码片段。<br />- `TABLE`：表示内容是表格。<br />- `IMAGE`：表示内容是图片。<br />- `SOURCE`：表示内容是答案块的参考来源。<br />- `QUESTIONS`：即 MAXIR AI 生成的建议问题，帮助引导您后续的数据探索和分析。|
|content|string|true|none||答案块的内容，随 `type` 值而异：<br /><br />- 当 `type` 为 `MESSAGE` 时，内容为一段文本。<br />- 当 `type` 为 `CODE` 时，内容为 Markdown 格式表示的代码片段。<br />- 当 `type` 为 `TABLE` 时，内容为表格，包含如下构成参数：<br />    - `name`：`.csv` 文件的名称。<br />    - `url`：文件的 S3 Key 或 URL。<br />    - `expires_at`：`url` 的过期时间。如需保存表格方便后续使用，请确保在 URL 过期之前完成下载。<br />- 当 `type` 为 `IMAGE` 时，内容为一张图片，包含如下构成参数：<br />    - `name`：图片的名称。<br />    - `url`：图片的 S3 Key 或 URL。<br />    - `expires_at`：`url` 的过期时间。如需保存图片方便后续使用，请确保在 URL 过期之前完成下载。<br />- 当 `type` 为 `SOURCE` 时，内容为答案块的参考来源，包含如下构成参数：<br />    - `source`：数据源的文件名。<br />    - `datasource_id`：数据源 ID。<br />    - `dataset_id`：数据集 ID。<br />    - `file_type`：数据源的文件扩展名。<br />- 当 `type` 为 `QUESTIONS` 时，内容为 MAXIR AI 生成的建议问题，帮助您引导后续的数据探索与分析。|
|group_id|string|true|none||答案块所在的分组 ID。|
|group_name|string|true|none||答案块所在的分组名称。|
|stage|string|true|none||MAXIR AI 生成答案的过程分为两个阶段：`Analyze` 和 `Respond`。  <br /><br />- `Analyze` 阶段的答案块并非最终答案的构成部分，为分析过程中的输出，旨在帮助您理解答案的生成方式。<br />- `Respond` 阶段的答案块是 MAXIR AI 基于您的问题生成的最终答复。|

#### 枚举值

|属性|值|
|---|---|
|type|MESSAGE|
|type|CODE|
|type|TABLE|
|type|SOURCES|
|type|QUESTIONS|
|stage|Analyze|
|stage|Respond|

<h2 id="tocS_DataSourceConfig">DataSourceConfig</h2>

<a id="schemadatasourceconfig"></a>
<a id="schema_DataSourceConfig"></a>
<a id="tocSdatasourceconfig"></a>
<a id="tocsdatasourceconfig"></a>

```json
{
  "name": "string",
  "type": "string",
  "url": "string",
  "file_object_key": "string",
  "user_id": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|name|string|true|none||数据源名称，需包含文件扩展名（例如 `example.csv`），至多可支持 128 个字符。如超过此限制，名称将被截断展示。|
|type|string|true|none|FILE|数据源的类型。设置为 **FILE**。|
|url|string|false|none||文件 URL，用于公网访问该文件。<br /><br />`url` 和 `file_object_key` 之间必须且只能指定其一。<br /><br />仅支持以下扩展名的文件：.csv、.tsv、.md、.mdx、.json、.txt、.pdf、.pptx、.ppt、.doc、.docx、.xls 或 .xlsx。|
|file_object_key|string|false|none||您本地上传文件的对象存储路径。<br /><br />`url` 和 `file_object_key` 之间必须且只能指定其一。<br /><br />支持的文件扩展名包括：**.csv**、**.tsv**、**.md**、**.mdx**、**.json**、**.txt**、**.pdf**、**.pptx**、**.ppt**、**.doc**、**.docx**、**.xls** 或 **.xlsx**。<br /><br />如何获取文件的 `file_object_key`：<br /><br />当使用 [Upload file](/api-reference/upload-file) 接口完成文件上传后，会返回该文件的`file_object_key`。|
|user_id|string|true|none||用户 ID，即您在组织中的唯一身份标识。|

