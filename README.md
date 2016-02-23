# Ruyi.Ai Helpdesk

* [接口说明](#接口说明)
  * [意图识别接口（GET /message）](#意图识别接口-get-message)
  	* [意图识别结果（Intent）](#意图识别结果-intent)
	* [示例：识别两个数字的加减法](#示例-识别两个数字的加减法)
* [更新说明](#更新说明)
* [注意事项](#注意事项)

## 接口说明

API (v1.0.0) 服务的域名URL
````
http://api.ruyi.ai/v1
````

### 意图识别接口 （GET /message）
从中文自然语言文本提取实体和意图，并利用知识图谱为用户提供信息增值服务。

服务地址
<pre>
http://api.ruyi.ai/v1/message
</pre>

#### 输入参数

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



#### 意图识别结果 (Intent)
Intent 指自然语言文本中提取的一个用户意图，对应原文中的一段文字。它对应到知识图谱中的一个节点，例如命名实体，用户命令等。

基本属性
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

#### 示例：识别两个数字的加减法

调用意图接口
<pre>
http://api.ruyi.ai/v1/message?q=1-1等于几&app_key=304abf8a-2172-42e0-8e1f-c185c990bf5e&user_id=123456
</pre>

返回结果说明
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


## 更新说明
2016-02-23 v1.0.0 新框架上线
 * 支持开发者自定义后台编辑意图

## 注意事项
 * 文中使用的app-key仅供测试使用，如有开发需求，请联系：<code>x@ruyi.ai</code>
 * 目前我们使用 **github** 自带的issue track系统进行bug追踪。
 * 文档中链接不建议直接点击，可能会出错。请直接拷贝复制该整个链接到浏览器。
 * RESTFUL API 调用参数中会包含标点符号，中文等非ASCII字符，因此调用服务需要注意 <a href="http://baike.baidu.com/view/1197115.htm">URL Encode</a> 参数值。
