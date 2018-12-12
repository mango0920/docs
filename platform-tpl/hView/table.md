# 使用文档
## Select Attributes
参数|说明|类型|可选值|默认值
--------------|-|-|-|-
tree          |是否树形展开表格|Boolean|-|false
data          |表格数据|Array|-|[]
column        |表格渲染配置项，下面会详述|Array|-|[]
trClickToCheck|点击行是否模拟点击复选框|Boolean|-|false
missMsg       |没有数据时的提示|String|-|没有找到匹配的记录
refresh       |当前页是否可点击|Boolean|-|false

## column
>重要说明：`func, key, format`需且仅需配置其中一个;如果配置了`format`, 则必需配置`name`

参数|说明|类型|可选值|默认值
--------------|-|-|-|-
func          |功能性表格|String|index(序号)；check(复选)；其他字符串（用作列名）
key           |用来取值的键名|String
format        |转化显示值的方法，Function参数为对应行的数据<必需name>|Function
name          |列名|String
icons         |字体图标<必需func作为列名>|Array
order         |可排序的key<必需key>|String|key的值
class         |该列表头表体类名|String
classHead     |该列表头类名，Function参数为对应行的数据|String/Function
classBody     |该列表体类名，Function参数为对应行的数据|String/Function
fn            |点击回调,Function参数为对应行的数据<必需key或format>|Function
textLimit     |文字超过时添加title属性<必需key或format>|Number


## icons[]说明
参数|说明|类型|可选值|默认值
-|-|-|-|-
iconFont|font-family|String
iconClass|icon类名|String/Function，Function参数是对应行的数据


## Methods
方法名|说明|参数
---------|-|-
checkData|获取选中数据，只有在prop: tree为false时才有效|-

## Select Events
事件名称|说明|回调参数
-----------|-|-
checkChange|点击复选框，只有在prop: tree为 true时才有效|当前行对应的一条数据
