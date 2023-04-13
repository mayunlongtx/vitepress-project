# 认识 vim

## 安装

- vscode 下载 Vim 插件

## 模式

- 正常模式 (Normal-mode)
- 插入模式 (Insert-mode)

## 基础的移动

-  `k` :arrow_up:
-  `j` :arrow_down:
-  `h` :arrow_left:
- `l` :arrow_right:

## 插入文字

- `a` :point_right: (append) 在光标后输入
- `i` :point_right: (insert) 在光标前输入

## 退出 insert 模式

- 使用 `Esc` 或者  `Ctrl + [` 
- 推荐 `Ctrl + [` 

## 终端中 使用 vim / 如何退出

- `:wq` :point_right: 保存且退出，需要在 `Normal` 模式下
- `:q!` :point_right: 强制退出，不保存内容

## Ctrl 和 caps 调换位置

 - [Window](https://docs.microsoft.com/zh-cn/windows/powertoys/keyboard-manager)

 - [Mac](https://support.apple.com/zh-cn/guide/mac-help/mchlp1011/mac)

## Esc 改建

```javascript
	// vscode 配置项文件  settings.json 
	"vim.insertModeKeyBindings": 
		{
			{
				"before": ["xxx"],
				"after": ["<Esc>"]
			},
		}
		
```

## 如何快速移动

 - [配置](https://github.com/VSCodeVim/Vim#mac)

 ```yaml
 	#需要在终端将下边命令逐个输入
	$ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false              # For VS Code
	$ defaults write com.microsoft.VSCodeInsiders ApplePressAndHoldEnabled -bool false      # For VS Code Insider
	$ defaults write com.visualstudio.code.oss ApplePressAndHoldEnabled -bool false         # For VS Codium
	$ defaults write com.microsoft.VSCodeExploration ApplePressAndHoldEnabled -bool false   # For VS Codium Exploration users
	$ defaults delete -g ApplePressAndHoldEnabled                                           # If necessary, reset global default
 ```

## Tips

 - 习惯 `insert` 完 就⽴⻢回到 `normal` 模式

