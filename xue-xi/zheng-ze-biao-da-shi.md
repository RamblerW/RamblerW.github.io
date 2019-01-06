> ### 正则表达式

1. 匹配汉字：```[\u4e00-\u9fa5]```
2. 前匹配：```(?<=preContent)targetContent```
3. 后匹配：```targetContent(?=lastContent)```
4. 匹配￥：`[\u00A5]`



> ### Xpath 表达式

1. 去空格：给 xpath 表达式外层增加 `normalize-space()`。==注：使用该方法后只能获取到一个元素==
2. 获取当前元素的下一个兄弟元素：`following-sibling::`。例：`//span[contains(text(),'出品方')]/following-sibling::text())`
3. 包含某个class：`div[contains(@class, "p-name")]`

