# live-ppt-publisher

将已经定稿的银行螺丝钉直播 PPT 成品发布到飞书与腾讯文档的 Codex Skill。

这个 Skill **不制作、不修改 Keynote/PPT**。它只处理从 Keynote 导出的最终文件：`.key`、PDF 和逐页图片。

## 能做什么

1. 从电脑下载文件夹识别同一期的 `.key`、PDF 和逐页图片。
2. 按历史命名规则在飞书共享文件夹中新建本期子文件夹并上传成品。
3. 在腾讯文档中创建普通在线文档，将图片按页码逐张插入。
4. 将腾讯文档设置为“所有人可查看”。
5. 通过飞书私聊回传飞书文件夹和腾讯文档两个链接。
6. 修改某一页时更新原腾讯文档，尽量保留原链接。

## 安装

克隆仓库后，将 Skill 文件夹复制到 Codex 的个人 Skills 目录：

```bash
git clone https://github.com/fanlili321/live-ppt-publisher.git
cp -R live-ppt-publisher/skill/live-ppt-publisher ~/.codex/skills/
```

重新开启一个 Codex 任务后即可使用。

## 使用前准备

- 在 `~/Downloads` 中准备同一期的 `.key`、PDF 和逐页图片，或在请求中指定其他目录。
- 图片文件名应带连续三位页码，例如 `.001.jpeg`、`.002.jpeg`。
- 登录飞书和腾讯文档，并确保有目标共享文件夹的编辑权限。
- 在 Codex 中安装或启用飞书云盘、飞书联系人、飞书消息与浏览器控制能力。
- 准备好飞书共享父文件夹链接；不要把某一期的子文件夹误当成父目录。

## 快速开始

可以直接对 Codex 说：

```text
使用 $live-ppt-publisher 发布第473期直播PPT。
成品在下载文件夹，飞书共享父文件夹是：https://example.feishu.cn/drive/folder/xxxxx
```

如果文件名已经包含期数和标题，也可以简化为：

```text
使用 $live-ppt-publisher，把下载文件夹里刚定稿的直播PPT发布到飞书和腾讯文档，并把两个链接私聊发给我。
```

执行过程中，Skill 会在权限修改、覆盖文件、删除冲突版本和发送飞书消息前按工具规则请求确认。

## 标准输出

- 飞书本期共享文件夹：包含 `.key`、PDF 和逐页图片子文件夹。
- 腾讯在线文档：标题为 `第{期数}期螺丝钉专属直播课-{PPT标题}`，正文包含全部 PPT 图片。
- 腾讯文档权限：所有人可查看。
- 飞书私聊：包含飞书共享文件夹链接和腾讯文档链接。

## 重要说明

- 腾讯文档必须逐张上传图片，等待当前图片插入后再上传下一张。一次多选可能导致页序错乱。
- PDF 页数与图片数量不一致时应停止发布，先修正导出文件。
- 更新单页时应修改原腾讯文档，以保留原链接。
- 本 Skill 面向特定业务工作流；其他团队可在 `SKILL.md` 中替换命名规则、飞书目录和消息模板。

## 仓库结构

```text
live-ppt-publisher/
├── README.md
└── skill/
    └── live-ppt-publisher/
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```
