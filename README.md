#Ruyi.Ai Helpdesk

### API (v1.0.0) 服务的域名URL
````
http://api.ruyi.ai/v1
````

### 注意事项
 - 文档中链接不建议直接点击，可能会出错。请直接拷贝复制该整个链接到浏览器。
 - RESTFUL API 调用参数中会包含标点符号，中文等非ASCII字符，因此调用服务需要注意 <a href="http://baike.baidu.com/view/1197115.htm">URL Encode</a> 参数值。


# Ruyi API 接口

## GET /message
### 功能介绍
从中文自然语言文本提取实体和意图，并利用知识图谱为用户提供信息增值服务。

### 服务地址
<pre>
http://api.ruyi.ai/v1/message
</pre>

### 输入参数

 * 注意，所有字符串参数需要 URL-encoded.

<table  class="table-responsive">
  <thead>
    <tr>
      <th>参数</th>
      <th>参数类型</th>
      <th>是否必须</th>
      <th>含义</th>
    </tr>
  </thead>
  <tbody>
   <tr>
    <td>q</td>
    <td>String</td>
    <td>是</td>
    <td>输入中文自然语言文本，例如“1-1等于几”</td>
   </tr>
    <tr>
    <td>app_key</td>
    <td>String</td>
    <td>是</td>
    <td>应用的开发者密钥</td>
   </tr>
   <tr>
    <td>user_id</td>
    <td>String</td>
    <td>是</td>
    <td>用户唯一标识，便于支持个性化语义解析。建议开发者使用UUID字符串</td>
   </tr>
  </tbody>
</table>


### 服务示例
<pre>
http://api.ruyi.ai/v1/message?q=1-1等于几&app_key=304abf8a-2172-42e0-8e1f-c185c990bf5e&user_id=123456
</pre>
<!--
## POST /speech
### 功能介绍
从音频文件中识别中文文本，并中文自然语言文本提取实体和意图，并利用知识图谱为用户提供信息增值服务。

### 服务地址
<pre>
http://api.ruyi.ai/v1/speech
</pre>

### 输入参数

<table  class="table-responsive border">
  <thead>
    <tr>
      <th>参数</th>
      <th>参数类型</th>
      <th>是否必须</th>
      <th>含义</th>
    </tr>
  </thead>
  <tbody>
   <tr>
    <td>speech</td>
    <td>File</td>
    <td>是</td>
    <td>输入的语音文件</td>
   </tr>
   <tr>
    <td>bits</td>
    <td>Int</td>
    <td>是</td>
    <td>采样位数</td>
   </tr>
   <tr>
    <td>rate</td>
    <td>Int</td>
    <td>是</td>
    <td>采样频率</td>
   </tr>
    <tr>
    <td>app_key</td>
    <td>String</td>
    <td>是</td>
    <td>应用的开发者密钥</td>
   </tr>
   <tr>
    <td>user_id</td>
    <td>String</td>
    <td>否</td>
    <td>用户唯一标识，便于支持个性化语义解析。建议开发者使用加密后的用户ID</td>
   </tr>
   <tr>
    <td>msg_id</td>
    <td>String</td>
    <td>否</td>
    <td>请求的唯一标识,便于回查追踪，例如“aeaa40ad-3546-421e-9129-0622dd46ee4c”</td>
   </tr>
   <tr>
    <td>context</td>
    <td>String</td>
    <td>否</td>
    <td>用户当前上下文信息。Context 的一个实例，JSON字符串格式, 例如 “{"name":"张三"}”</td>
   </tr>

  </tbody>
</table>

### 服务示例
$ curl -i -F "bits=your_file_bits" -F "rate=your_file_rate" -F "app_key=YOURAPPKEY" -F "speech=@your_speech_file" -F "user_id=lab-user-api.ruyi.ai" http://api.ruyi.ai/v1/speech

### 返回结果
````
同Get /message接口返回结果
````

## POST /feedback
### 功能介绍
提交用户反馈,指出那条解析结果有何种错误。

### 服务地址
<pre>
http://api.ruyi.ai/v1/feedback
</pre>

### 输入参数
<table  class="table-responsive">
  <thead>
    <tr>
      <th>参数</th>
      <th>参数类型</th>
      <th>是否必须</th>
      <th>含义</th>
    </tr>
  </thead>
  <tbody>
   <tr>
    <td>content</td>
    <td>String</td>
    <td>是</td>
    <td>开发者／用户的反馈意见。例如:”地点识别错误“</td>
   </tr>
    <tr>
    <td>ref_msg_id</td>
    <td>String</td>
    <td>是</td>
    <td>被反馈的解析结果</td>
   </tr>
   <tr>
    <td>app_key</td>
    <td>String</td>
    <td>是</td>
    <td>开发者密钥</td>
   </tr>
   <tr>
    <td>user_id</td>
    <td>String</td>
    <td>否</td>
    <td>用户唯一标识</td>
   </tr>
  </tbody>
</table>

### 服务示例
$ curl -XPOST 'http://api.ruyi.ai/v1/feedback'  -d "content=ok&app_key=YOURAPPKEY&user_id=lab-user-api.ruyi.ai&ref_msg_id=8dc03d3e-bd3a-4d5f-9d47-5d030d5bb980"

-->

# Ruyi API 返回数据结构

## Intent （意图）
Intent 指自然语言文本中提取的一个用户意图，对应原文中的一段文字。它对应到知识图谱中的一个节点，例如命名实体，用户命令等。


### 基本属性
<table  class="table-responsive">
  <thead>
    <tr>
      <th>参数</th>
      <th>参数类型</th>
      <th>是否必须</th>
      <th>含义</th>
    </tr>
  </thead>
  <tbody>

  <tr>
   <td>intent_name</td>
   <td>String</td>
   <td>是</td>
   <td>意图的名称，自定义意图的名称可以在开发者后台编辑</td>
  </tr>
   <tr>
    <td>action</td>
    <td>String</td>
    <td>否</td>
    <td>动作的名称，自定义动作的名称可以在开发者后台编辑</td>
   </tr>
   <tr>
    <td>parameters</td>
    <td>JSON Object</td>
    <td>否</td>
    <td>意图参数列表</td>
   </tr>
   <tr>
    <td>result</td>
    <td>JSON Object</td>
    <td>否</td>
    <td>意图执行结果</td>
   </tr>
  </tbody>
</table>

示例：

    {
		"code": 0,
		"msg": "ok",
		"result": {
			"msg_id": "32c70057-c492-4745-9984-710d23e7c64e",
			"_text": "1-1等于几",
			"intents": [{
				"parameters": {
					"num2": "1",
					"num1": "1",
					"operator": "-"
				},
				"action": "TWO_VALUE_CAL",
				"result": {
					"text": "0",
					"type": "dialog"
				},
				"intent_name": "two_value_cal"
			}],
			"meta_process_milliseconds": 43
		}
    }

# Ruyi API 接口问题反馈

目前我们使用 **github** 自带的issue track系统进行bug追踪。

# 更新说明



### v1.0.0 新框架上线
<ol>
  <li>支持开发者自定义后台编辑意图</li>
</ol>


## 注意事项

<ul>
<li>文中使用的app-key仅供测试使用，如有开发需求，请联系：<code>x@ruyi.ai</code></li>
</ul>
