# Scientific Figure Shapes

## 个人介绍

**momo科研版** · 分享科研技巧

小红书 [momo科研版](https://xhslink.com/m/3aXzBrRpJ5G)（小红书号 `2798706502`）

| 小红书 · 扫码访问主页 | 微信 · 扫码添加好友 |
| :---: | :---: |
| <img src="assets/contact/xiaohongshu-momo.png" alt="momo科研版的小红书二维码" width="240"> | <img src="assets/contact/wechat-momo.jpg" alt="momo 的微信二维码" width="260"> |

`scientific-figure-shapes` 是一个用于 Codex 的科研图像重建 skill，可以把科研机制图、流程图、截图、学术示意图快速还原为可编辑的 PowerPoint VBA Shapes。

它的目标不是机械地做像素级描摹，而是优先保证“可编辑”和“够快”：标题、标签、箭头、框线、图例、简单图标、坐标轴和版式结构会尽量重建为 Office 原生形状；复杂的生物结构、纹理插画、显微图、照片或高细节区域，则可以作为局部图片裁剪保留。

## 能做什么

- 将上传的科研图片转换为面向 PowerPoint 的可运行 VBA 模块。
- 把文字、标注、连接线、箭头、图例、表格、简单图标和整体布局重建为可编辑 Shapes。
- 对复杂插画或高细节区域生成可追溯的局部裁剪，避免耗时重画造成失真。
- 输出 `.bas` 宏文件、局部素材、结构清单、运行记录，以及可选的 `.pptx` 兜底文件。
- 默认走快速重建流程；如果需要，也可以要求更严格的保真检查和修正轮次。

## 典型用法

可以这样向 Codex 提问：

```text
用 scientific-figure-shapes，把这张科研机制图快速还原成可编辑 PowerPoint VBA Shapes。
```

也可以指定更高保真：

```text
用 scientific-figure-shapes 高保真还原这张图，尽量保持布局、颜色和箭头位置一致。
```

## 安装方式

最简单的方式：直接把这个 GitHub 链接发给 Codex，并告诉它“帮我安装这个 skill”：

```text
https://github.com/summer-ai-lab/scientific-figure-shapes
```

Codex 会把它安装到本地 skills 目录。安装后重启 Codex，或在支持的环境中重新加载 skills。

也可以手动把仓库克隆到本地 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/summer-ai-lab/scientific-figure-shapes.git ~/.codex/skills/scientific-figure-shapes
```

如果使用 SSH：

```bash
mkdir -p ~/.codex/skills
git clone git@github.com:summer-ai-lab/scientific-figure-shapes.git ~/.codex/skills/scientific-figure-shapes
```

手动安装后同样需要重启 Codex，或在支持的环境中重新加载 skills。

## 目录结构

```text
scientific-figure-shapes/
├── SKILL.md
├── agents/
│   └── scientific-figure-shapes.yaml
├── references/
│   ├── delivery-note-format.md
│   ├── fidelity-review-gates.md
│   └── office-shape-recipes.md
└── scripts/
    ├── canvas_point_mapper.py
    ├── macro_smoke_lint.py
    ├── office_runtime_probe.py
    ├── ppt_macos_macro_launcher.py
    ├── ppt_windows_macro_runner.ps1
    ├── preserve_cropper.py
    └── render_delta_probe.py
```

## 常见输出

一次正常运行通常会生成：

- `*.bas`：包含 `BuildFinal` 的可运行 VBA 模块。
- `assets/*.png`：复杂视觉区域的局部保留素材。
- `manifest.md`：说明哪些区域是可编辑对象，哪些区域是保留裁剪。
- `*.pptx`：在 Office 自动化不可用时生成的可编辑兜底文件。
- `preview.png`：用于检查整体视觉效果的预览图。
- `run_report.md`：运行、校验和自动化状态说明。

## 设计取向

这个 skill 是面向实际科研制图修改场景的独立重写版，重点是快速得到可编辑结果。它适合组会图、机制图、论文示意图、汇报图和需要二次修改的学术图片。

如果目标是投稿级、像素级、逐元素复刻，请在提示中明确要求“高保真”“逐元素检查”或“多轮修正”。

## 基础要求

- 支持本地 skills 的 Codex 环境。
- Python 3，用于运行辅助脚本。
- Microsoft PowerPoint 或 WPS Presentation，用于可用时直接执行宏。

即使本机没有可自动化的 Office 环境，skill 仍然可以生成 VBA、局部素材和说明文件。
