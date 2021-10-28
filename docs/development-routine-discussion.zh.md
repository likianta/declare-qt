# 探讨一下 declare-qt 项目的技术路线的选型

## 对 QtWidgets 进行封装, 创造声明式结构和类 QML 属性绑定

缺点:

- QWidget 不能单独设置和观察 x/y, width/height 变化信号
- QSS 不支持动画
- 属性动画难以构造
- 缺少锚点系统
- ...

_TODO_

## 通过分析 Python 语法树来生成 QML 代码

缺点:

- 工作量巨大
- 难度过高
- ...

_TODO_

## 利用 Python 的语法特性来生成 QML 代码

_TODO_

## 用最小的力量在 QML 端创建好对象后, 尽可能在 Python 端操作对象

缺点:

- 性能下降严重
- QML 特性语法在 Python 中难以实现, 或者代码量大幅增加
- 一些 QML 属性无法转换为 Python 对象
- ...

_TODO_
