<!-- # Vim 命令 -->

# 行相关命令

## 移动

- 行首

  - `0`
  - `^` 到本行第一个不是 [`blank`](# "空格，tab，换⾏，回⻋等") 字符的位置

- 行尾
  - `$`
  - `g\_` 到本行最后一个不是 [`blank`](# "空格，tab，换⾏，回⻋等") 字符的位置
- 为了方便使用，对 `^` 以及 `g\_` 改键
  ```javascript
  // vscode 
  "vim.normalModeKeyBindings": [
  	{
  		"before": [
  			"H"
  		],
  			"after": [
  				"^"
  		]
  	},
  	{
  		"before": [
  			"L"
  		],
  		"after": [
  			"g",
  			"_"
  		]
  	},
  ]
  ```

## 插入

- 行首 :point_right: `I`
- 行尾 :point_right: `A`
- 行前 :point_right: `O`
- 行后 :point_right: `o`

## 删除、复制、粘贴当前行

- 删除 :point_right: `yy`
- 复制 :point_right: `dd`
- 粘贴 :point_right: `p`
