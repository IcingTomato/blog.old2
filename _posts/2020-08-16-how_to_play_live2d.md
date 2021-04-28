---
layout: post
title: "How to Play Live2D?"
description: "Live2D Module"
comments: false
keywords: "Live2D"
---

# Live2d的moc3配置说明

live2d的moc和moc3的配置是差不多的，主要是说明一下moc3格式的配置。

可以先阅读一下[官方文档](https://docs.live2d.com/cubism-editor-manual/top/)。

# 官方配置

以官方模型Hiyori为例。

文件说明:

> moc3 是模型文件
>
> model3.json 是模型配置文件
>
> pose3.json 预设姿势文件
>
> userdata3.json 用户数据和事件
>
> physics3.json 物理演算配置文件
>
> Hiyori.2048 文件夹存放模型图片
>    - texture_00.png
>    - texture_001png
> motions 文件夹存放模型动作文件
>
> Hiyori_m01.motion3.json //动作文件后缀为motion3.json

## model3.json

live2d只需配置好.model3.json就行了。

简单配置如下：

```shell
{
  "Version": 3,
  "FileReferences": {
    "Moc": "Hiyori.moc3", //.moc3文件相对路径
    "Textures": [
      "Hiyori.2048/texture_00.png", //图片相对路径
      "Hiyori.2048/texture_01.png"
    ]
  }
}
```

详细配置:

```shell
{
	"Version": 3,
	"FileReferences": {
		"Moc": "Hiyori.moc3", //.moc3文件相对路径
		"Textures": [
			"Hiyori.2048/texture_00.png", //图片相对路径
			"Hiyori.2048/texture_01.png"
		],
		"Physics": "Hiyori.physics3.json", //物理演算文件相对路径
		"Pose": "Hiyori.pose3.json", //姿势文件相对路径
		"UserData": "Hiyori.userdata3.json",
		"Motions": {   //动作配置
			"Idle": [  //待机
				{
					"File": "motions/Hiyori_m01.motion3.json",  文件相对路径
					"FadeInTime": 0.5,  //淡入时间，可省略
					"FadeOutTime": 0.5  //淡出时间，可省略
					"sound"："voice/voice.ogg" //声音文件文件相对路径
				},
				{
					"File": "motions/Hiyori_m02.motion3.json",
					"FadeInTime": 0.5,
					"FadeOutTime": 0.5
				}
			],
			"TapBody": [  //触摸位置触发动作
				{
					"File": "motions/Hiyori_m04.motion3.json",
					"FadeInTime": 0.5,
					"FadeOutTime": 0.5
				}
			]
		}
	},
	"Groups": [  //参数组
		{
			"Target": "Parameter",
			"Name": "LipSync",
			"Ids": [
				"ParamMouthOpenY"
			]
		},
		{
			"Target": "Parameter",
			"Name": "EyeBlink",
			"Ids": [
				"ParamEyeLOpen",
				"ParamEyeROpen"
			]
		}
	],
	"HitAreas": [ //触摸区域
		{
			"Id": "HitArea",
			"Name": "Body"
		}
	]
}
```

.physics3.json .pose3.json 等文件一般用Live2d Cubism Editor生成，可有可不有。没有.physic3.json物理演算可以用动作文件ide.motion3.json代替，idle是待机的动作。

.moc3文件用记事本打开开头是MOC3代表是moc3格式模型。

# Live2DViewerEX配置

推荐使用Live2DViewerEX配置.model3.json文件，有软件辅助易上手，高级的配置很不难。也可以参考Live2DViewerEX的官方文档写的参数。

注意的是每个软件的配置不一定通用的，存在加载不了模型是正常。但最基本的配置是通用的，比如下面的基本配置：

```shell
{
	"Version": 3,
	"FileReferences": {
		"Moc": "Hiyori.moc3", //.moc3文件相对路径
		"Textures": [
			"Hiyori.2048/texture_00.png", //图片相对路径
			"Hiyori.2048/texture_01.png"
		],
		"Physics": "Hiyori.physics3.json", //物理演算文件相对路径
		"Pose": "Hiyori.pose3.json", //姿势文件相对路径
		"Motions": {   //动作配置
			"Idle": [  //待机
				{
					"File": "motions/Hiyori_m01.motion3.json",  文件相对路径
					"FadeInTime": 0.5,  //淡入时间，可省略
					"FadeOutTime": 0.5  //淡出时间，可省略
					"sound"："voice/voice.ogg" //声音文件文件相对路径
				}		
			]
		}
	}
}
```

# 链接

转载自[live2d配置-Eikan](https://blog.tsundere.best/post/live2d%E9%85%8D%E7%BD%AE/)
