# 配置中心

配置中心提供一组可自定义的系统参数，支持按组织级别进行灵活配置。当前包含三类配置项：**自然语言生成 SQL、知识库配置、应用层配置**。

自然语言生成 SQL配置：

- **Maximum connections**：最大连接数量，取值范围为 1～1000，默认 `100`。
    
- **Theme color**：界面的主题色，默认值为 `#1890ff`。
    
- **language**：界面语言，目前支持`中文`和 `English`。 
    
- **Float config**：取值范围为 0～10，默认值为 `8.8`。
    

知识库配置：

- **Message Returned For Empty Response**：答复内容为空的时候返回的消息。
    
- **System Prompt**：系统提示词。

应用层配置：

- **Insufficient Permission Error Message**：操作权限不足时的提示信息。