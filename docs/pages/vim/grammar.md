# 语法

## vim 语法

- 操作（ operation ） + 动词（范围）

## 操作

- 删除 :point_right: `d`
- 删除并且进⼊ insert 模式 :point_right: `c`
- 复制 :point_right: `y`

## 基于单词/字串的移动

- 移动到单词的结尾 :point_right: `e`
- 移动到字串的结尾 :point_right: `E`
- 移动到上⼀个单词的开头 :point_right: `b`
- 移动到上⼀个字串的开头 :point_right: `B`
- 移动到单词的开头 :point_right: `w`
- 移动到的字串开头 :point_right: `W`
- 移动到上⼀个单词的结尾 :point_right: `ge`

## 常用组合

> tips:可以自行根据语法进行自行组合

- 删除当前单词 :point_right: `cw`
- 在当前单词结尾处添加 :point_right: `ea`

## 更有效率的处理单字符

- 删除光标所在的字符 :point_right: `x`
- 删除光标前的字符 :point_right: `X`
- 删除当前光标的字符并进⼊ insert 模 式 :point_right: `s`
- 删除当前光标缩在⾏并进⼊ insert 模 式 :point_right: `S`
- 替换⼀个字符 :point_right: `r`
- 替换多个字符 :point_right: `R`

## undo/redo
> 可撤销块,进⼊插⼊模式开始，直到返回普通模式为⽌，在此
期间输⼊或删除的任何内容都被当成⼀次修改

- undo :point_right: `u`
- redo :point_right: `Ctrl + r`

## 配置

<!-- 需求迁移到后期的 vscode 模块 -->

```javascript
  // vscode
  "vim.operatorPendingModeKeyBindingsNonRecursive": [
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
