# 功能
- 可选择每页显示多少条
- 可控制显示页数范围大小
- 可控制当前页是否可点击
- 可填写某一页跳转

# 依赖
- bootstrap@^4.1.3

# 使用
```html
<!-- 示例 -->
<h-pagination
  :total="total"
  :current="page"
  @jump="changePage" @changeSize="changeSize"
></h-pagination>
```
## Select Attributes
参数|说明|类型|可选值|默认值
-----------|-|-|-|-
rangNum    |控制显示页数范围大小|Number|-|1
sizesArr   |控制每页显示条数可选值|Array|-|[5, 10, 20, 30, 50]
defaultSize|每页显示条数默认值|Number|-|10
total      |总条数|Number|-|0
current    |当前页|Number|-|1
refresh    |当前页是否可点击|Boolean|-|false

## Select Events
事件名称|说明|回调参数
----------|----------------|-
changeSize|点击页数         |将跳转的页数
jump      |点击上一页或下一页|将跳转的页数