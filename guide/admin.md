# 管理员指南
在成功开通 MAXIR AI 后，企业管理员可以通过统一的管理平台，轻松对组织内的各项资源进行全面管理，包括：

+ 用户管理
+ 项目管理
+ MAXIR AI 资源管理（如订阅套餐中的座席、任务配额、工作空间容量等）
+ 支付设置

## 用户管理
MAXIR AI 提供两种用户类型，支持管理员根据每个独立用户所需的权限进行选择创建，实现精细化的用户权限管理。

### 用户类型
MAXIR AI 提供两种用户类型，支持管理员根据每个独立用户所需的权限进行选择创建，实现精细化的用户权限管理。

+ **团队成员**：团队成员拥有控制台的全部功能权限，可与其他成员协作，管理并操作所在项目中的数据，支持的操作包括：
    - 创建、管理数据集与数据源
    - 基于数据集运行数据任务
    - 与其他团队成员协作

<font style="background-color:rgb(240,244,255);">团队成员仅需在控制台上完成操作，无需 Open API 权限。</font>

+ **系统用户**：系统用户可通过 MAXIR AI 提供的 Open API 大批量运行数据任务，支持的操作包括：
    - 通过 API 调用 MAXIR AI 的 AI 驱动数据分析能力
    - 高效、大批量执行数据分析任务
    - 利用 Open API 开发定制化的 AI 解决方案，为自己的最终用户提供服务

### 创建用户
**创建单个用户：**

1. 在顶部导航栏中，点击“用户管理”。
2. 点击“创建用户”，选择用户类型，填写用户信息，并点击页面左下角的“创建”按钮。

创建团队成员，需填写如下信息： 

| **参数** | **是否必须** | **说明** |
| --- | --- | --- |
| 用户名 | 是 | 团队成员的用户名，在团队中唯一标识该用户。 |
| 密码 | 是 | 该团队成员的密码，支持随机生成。 |
| 分配座席 | 否 | 是否给该团队成员分配座席。非必选，可在需要时再为团队成员分配座席。<br/><font style="background-color:rgb(240,244,255);">团队成员只有在分配了座席后，才能执行数据任务。</font> |
| 加入项目 | 否 | 将该团队成员添加至选择的项目中。<br/><font style="background-color:rgb(240,244,255);">团队成员可以并且只能在加入了的项目中创建、管理数据集和数据源。</font> |

创建系统用户，需填写如下信息：

| **参数** | **是否必须** | **说明** |
| --- | --- | --- |
| 展示名 | 是 | 系统用户的展示名，仅作展示用。 |
| 密码 | 是 | 该团队成员的密码，支持随机生成。 |
| 分配座席 | 否 | 是否给该团队成员分配座席。非必选，可在需要时再为团队成员分配座席。<br/><font style="background-color:rgb(240,244,255);">团队成员只有在分配了座席后，才能执行数据任务。</font> |
| 加入项目 | 否 | 将该团队成员添加至选择的项目中。<br/><font style="background-color:rgb(240,244,255);">团队成员可以并且只能在加入了的项目中创建、管理数据集和数据源。</font> |


**批量创建用户：**

批量创建功能仅支持用于创建团队成员。系统成员只支持单个添加。

1. 在顶部导航栏中，点击“用户管理”。
2. 点击“批量创建”。
3. 在弹出的对话框中，点击“下载模板”，完成模板内容填写，点击“上传”。

### 查看用户信息
进入“用户管理”页面后，默认展示组织内的所有用户信息列表。

![](/images/1740118953363-0.png)

如上图所示，在该列表中，你可以查看每一个用户的如下信息：

| **字段名** | **说明** |
| --- | --- |
| 用户ID | 用户 ID（以 `tmm` 为前缀）和用户名 / 展示名。<br/><font style="background-color:rgb(240,244,255);">团队成员提供</font>**<font style="background-color:rgb(240,244,255);">用户名</font>**<font style="background-color:rgb(240,244,255);">，系统成员提供</font>**<font style="background-color:rgb(240,244,255);">展示名</font>**<font style="background-color:rgb(240,244,255);">。</font> |
| 用户类型 | 用户类型。MAXIR AI 支持两种用户类型：“团队成员”和“系统用户”。 |
| 所属项目 | 用户加入的项目。 |
| 是否分配座席 | 用户是否分配座席。只有分配了座席的用户才能在组织中执行数据任务。 |


你也可以通过用户列表上方的过滤器对用户进行筛选，支持的过滤器包括：

+ **用户类型**：只展示“团队成员”或“系统用户”。
+ **所属项目**：只展示加入到指定项目中的用户。
+ **是否分配座席**：只展示有分配座席或者未分配座席的用户。

### 管理用户所属项目
MAXIR AI 支持将指定用户添加至项目，或从项目中移除。

<font style="background-color:rgb(255,245,235);">未加入任何项目的用户在使用 MAXIR AI 时将受到以下限制：</font>

+ <font style="background-color:rgb(255,245,235);">上传数据源或创建数据集</font>
+ <font style="background-color:rgb(255,245,235);">执行数据任务时，无法指定数据集进行问答</font>

<font style="background-color:rgb(255,245,235);">因此，建议将用户加入到相应项目中，以便更充分地利用 MAXIR AI 的数据分析功能。</font>

1. 在“用户管理”页面，找到目标用户所在位置，点击“所属项目”列中的下拉列表。
2. 在弹出的对话框中，勾选项目将用户添加至选定项目中，或者去勾选项目将用户从对应项目中移除，点击“确定”。

  同一用户可以加入到多个项目中。如无合适的项目，你也可以点击左下角的“创建新项目”进行项目创建，然后勾选新创建的项目，完成用户添加。

![](/images/1740118953363-1.png)

### 修改用户信息
MAXIR AI 支持修改团队成员的用户名及密码，支持修改系统用户的展示名。

1. 在“用户管理”页面，找到目标用户所在位置，点击“操作”列中的修改按钮。
2. 在弹出来的对话框中，输入修改后的信息，点击“确认”。

  如需修改团队成员的密码，点击“密码”字段右侧的“修改”按钮。在弹出的“修改密码”对话框中，输入并确认新密码，点击“修改”即可。

### 删除用户
MAXIR AI 支持将不再需要的用户账号从组织中移除。用户删除后，分配给该用户的座席（如有）也将立即被释放。

<font style="background-color:rgb(255,245,235);">用户移除后，与该用户相关的数据都将被删除，该操作一旦开始则无法撤销，请谨慎操作。</font>

1. 在“用户管理”页面，找到目标用户所在位置，点击“操作”列中的删除按钮。
2. 在弹出来的确认对话框中，点击“删除”。

## 项目管理
项目是组织内基于特定目标创建的群组。MAXIR AI 支持根据需求灵活创建多个项目。

虽然所有项目共享同一工作区的容量资源，但各项目间数据相互隔离。也就是说，一个项目中创建的数据集无法被其他项目访问，从而实现精细化管理数据安全，确保项目之间的边界清晰明确。

### 创建项目
组织创建完成后，系统会自动为该组织创建一个默认项目。你也可以按需创建项目。

1. 在管理控制台的顶部导航栏中，点击“项目管理”。
2. 在出现的项目列表中，点击“创建项目”。

![](/images/1740118953363-2.png)

3. 在弹出的对话框中，设置项目名称，点击“创建项目”。

项目创建完成后，会自动进入项目详情页面，在该页面上可以完成项目成员管理以及项目 API Key 管理。详情请参考章节[管理项目成员](/maxirai/guide/admin?id=管理项目成员)和[管理项目 API Key](/maxirai/guide/admin?id=管理项目-api-key) 。

### 管理项目成员
组织管理员可以管理项目内的用户，包括添加和移除项目内用户。

#### 添加项目成员
1. 在“项目管理”页面，点击目标项目卡片进入项目详情页。
2. 在“用户”页签，点击“添加用户”按钮。

![](/images/1740118953363-3.png)

3. 在弹出的对话框中，选择需要添加的用户，点击“添加”。

#### 移除项目成员
从项目中移除的用户将无法再使用项目中的数据进行数据分析。

1. 在“项目管理”页面，点击目标项目卡片进入项目详情页。
2. 在“用户”页签，找到目标用户，点击“操作”列中的删除按钮。

  如需一次移除多个，可以勾选对应用户 ID 前的复选框，点击用户列表右上角的“删除”按钮，完成批量删除。

![](/images/1740118953363-4.png)

### 管理项目 API Key
当**系统用户**需要通过调用 MAXIR AI Open API 在指定项目内进行操作时，需要使用项目 API Key 进行鉴权。

> <font style="background-color:rgb(255,245,235);">项目 API Key 是访问和操作项目资源的身份凭证，若泄露或未经授权使用，可能导致项目数据泄露和数据安全风险。</font>**<font style="background-color:rgb(255,245,235);">请务必妥善保管，以确保项目安全。</font>**


#### 创建项目 API Key
从项目中移除的用户将无法再使用项目中的数据进行数据分析。

1. 在“项目管理”页面，点击目标项目卡片进入项目详情页。
2. 点击“项目 API Key”页签，点击 API Access Key 列表右上角的“+ API Access Key”按钮。

![](/images/1740118953363-5.png)

3. 在弹出的对话框中，设置 API Access Key 的名称，点击“创建”。
4. 拷贝并保存好生成的 Secret Key，确认保存后点击“我已经保存好该 Secret Key”。

![](/images/1740118953363-6.png)

<font style="background-color:rgb(240,244,255);">生成的 </font>**<font style="background-color:rgb(240,244,255);">Secret Key 仅在创建时展示一次</font>**<font style="background-color:rgb(240,244,255);">，请务必复制并妥善保存。离开此页面后，将只能在 API Key 列表中查看该 Secret Key 的后四位。</font>

#### 删除项目 API Key
出于安全考虑，MAXIR AI 建议定期清理不再使用的 API Key。已删除的 API Key 将无法再用于访问对应项目中的资源。

1. 在“项目管理”页面，点击目标项目卡片进入项目详情页。
2. 点击“项目 API Key”页签，找到不再需要的 API Key，点击“操作”列中的删除按钮。
3. 在弹出的确认框中，点击“删除”。

## 用量监控
MAXIR AI 管理员控制台提供用量监控功能，您可以查看工作空间容量以及数据任务配额使用情况。

1. 在管理员控制台的顶部导航栏中，点击“用量”。
2. 在“用量”页面，查看具体资源的使用情况。

![](/images/1740118953363-7.png)

