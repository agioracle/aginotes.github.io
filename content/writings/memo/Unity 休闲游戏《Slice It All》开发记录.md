---
title: Unity 休闲游戏《Slice It All》开发记录
date: 2025-04-09
draft: false
tags:
  - writing
  - memo
  - Unity
  - 休闲游戏
---
>  游戏设计文档： https://docs.google.com/document/d/1KbZ4fvnAftWMiYaKH5r-OTNOCx4kxWKNUU8M07QzFFY/edit?tab=t.0


### 2025-04-21
1. 尝试解决刀下降速度过快，没有“飘逸感”问题: 在添加向上的拉力的基础上，增加声音，体验改善不明显❌。

### 2025-04-18
1. 让主相机根据刀移动：尝试把主相机作为 Player 的子gameobject，相机除了跟随移动，还会跟随旋转（跟随旋转不是我们想要的效果）。使用相机控制脚本，控制主相机跟随 Player 的 position，但不跟随 rotation，效果较好✅。
2. 尝试解决刀下降速度过快，没有“飘逸感”问题：在降落过程中添加向上的拉力，有一定改善，但效果和参考游戏还是有较大差距❌。

### 2025-04-14
1. 尝试解决刀碰到 Block 后应该垂直往下切的问题：原来的主要问题在于 刀 和 HalfBlock 会发生碰撞，取消碰撞后，刀不会乱跳了，但刀还是在往前走。修改代码把 add forward force 和 add upward force 分开，只有当刀在旋转时才 add forward force。并且是在 FixedUpdate（固定时间间隔执行，和帧率无关，这样刀往前走的速度相对稳定） 函数中判断刀是否旋转，是的话才 add forward force。这样最终效果才相对较好✅。
2. 尝试解决 刀 旋转没有自动回到初始角度问题：通过在旋转过程中实时判断和初始 rotation 的角度偏差，当和初始角度偏差小于某个范围时，停止旋转。最终效果还不错，偶现旋转跳变问题，待后续优化✅。

### 2025-04-11
1. 尝试解决 Block 切开的效果不丝滑问题：发现主要的问题点在于 刀 和 HalkBlock 存在 collision， 因此默认把 halfblock 的 collider 为不生效状态，当 halfblock 初始化时启动一个协程去延迟 0.1s。最终实现效果和参考游戏比较接近✅。

### 2025-04-10
1. 尝试解决 Block 切开的效果不丝滑问题：通过在代码中控制让 刀 和 HalfBlock 的物理碰撞效果失效，最终实现效果不好，感觉上代码控制没有生效❌。

### 2025-04-08
1. 目前还需要优化的点：
	- [ ] 控制刀只有刀刃能够插入 Plane；
	- [ ] 刀下降过程速度较快，没有参考游戏中的“飘逸”感；
	- [x] 相机根据刀移动；
	- [x] 刀旋转能够自动纠正刀和初始旋转角度相差不大的位置；
	- [x] 刀在碰到 Block 后应该垂直往下切，而不是还往前走；
	- [x] Block 切开后的效果不丝滑，和参考游戏有差距；

### 2025-04-07
1. windsurf + unity-mcp 操作 Unity Editor
	- 安装 windsurf package：https://github.com/Asuta/com.unity.ide.windsurf.git
	- 安装 unity-mcp：https://github.com/justinpbarnett/unity-mcp。注意严格按照步骤安装。
	- 安装完成后，切换 Unity  代码编辑器为 Windsurf：Unity -> settings -> External Tools -> External Script Editor
2. 实现纯基于物理特性碰撞实现 刀切开方块， 效果不好，没有丝滑的切开效果
3. 控制刀每次旋转都是 360 度，如果刀落在 Plane 上的角度和初始旋转角度不一样，后续就会以这个新的旋转角度每次旋转 360 度，没有达成每次落在 Plane 上的角度和初始旋转角度相差不大的需求。
### 2025-04-03
 1. Unity 中 导入 FBX 模型文件后，发现模型 是灰色的，没有自动绑定 Texture。
    - 如果 Textures 是内含在模型文件中的，需要在导入后模型的 Inspector -> Materials -> Textures 中点击 Extracted Textures，这样一般就可以正常显示纹理了。
    - 如果 Textures 是独立的 png 文件，则也需要把 png 同时导入到 Unity 中，然后再绑定纹理。
    - 建议：导入的模型一般放在 Models 文件夹，纹理一般放在 Textures 文件夹。



