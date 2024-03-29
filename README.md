# proj274-Low-overhead-memory-expansion
# 题目：
面向轻量级虚拟机的低开销内存扩展技术

# 项目描述：

## 轻量级虚拟机/安全容器：
在服务器无感知计算中，应用或服务被分解为细粒度的、可独立部署的函数。当一个函数被调用时，服务器无感知平台会为该函数创建一个容器沙箱来执行用户代码以处理用户的请求。然而基于共享内核的容器沙箱技术无法提供足够的隔离以确保多租户场景下的安全性。因此，服务器无感知计算平台会将容器沙箱运行在可以提供强隔离的安全执行环境的轻量级虚拟机中，如AWS Firecracker。这种利用轻量级虚拟机来运行容器沙箱的方式，可以在保证安全性的同时，完全兼容容器的软件生态。

## 自动资源缩放
服务器无感知计算平台可以根据负载请求的变化自动调整分配给函数的资源，从而兼顾应用的性能和资源利用率。现有的服务器无感知计算平台通常采用水平缩放的方式来调整函数的资源。即当请求增加时，它会创建更多的轻量级虚拟机来承载函数的容器沙箱，从而提高函数的处理能力；当请求减少时，它会销毁多余的轻量级虚拟机，从而降低资源的消耗。然而，这种水平缩放的方式会严重地增加函数的冷启动延迟，从而降低函数的性能。此外，每个容器独占一个轻量级虚拟机的方式会导致严重的内存浪费，从而降低资源的利用率。

## 虚拟机内存垂直缩放：
对于服务器无感知计算，垂直缩放是更有潜力的资源缩放策略。当请求增加时，该策略会增大现有轻量级虚拟机的资源，以容纳更多的容器沙箱；当请求减少时，它会释放轻量级虚拟机的多余的资源。这种垂直缩放的方式可以避免冷启动延迟，从而提高函数的性能。此外，该策略允许同一个轻量级虚拟机运行多个容器沙箱，从而提高资源的利用率。

然而现有的基于轻量级虚拟的垂直扩展技术并不成熟，尤其是对于内存资源而言。首先，他需要运行在虚拟机中的应用能够随时感知到底层资源的变换从而进行相应的调整。其次，强制回收虚拟内存容易触发内核的保护机制，导致OOM，最终导致应用崩溃。最后，缩放虚拟机内存的时间开销通常为几百毫秒至几秒，这对于执行时间通常不超过1秒的函数而言是不可接受的。因此，我们需要一种新的轻量级虚拟机内存垂直缩放技术，以支持服务器无感知计算平台的内存资源的垂直缩放。

# 目标：
本赛题拟基于轻量级虚拟机的内存垂直缩放技术，实现亚毫秒级的内存垂直缩放，以支持服务器无感知计算平台的内存资源的垂直缩放。

# 所属赛道：
2024全国大学生操作系统比赛的“OS功能设计”赛道

# 参赛要求：
以小组为单位参赛，最多三人一个小组，且小组成员是来自同一所高校的本科生或研究生（2024年春季学期或之后毕业的学生）。如学生参加了多个项目，参赛学生选择一个自己参加的项目参与评奖，并遵循“2024全国大学生操作系统比赛”的章程和技术方案要求

# 难度：
高等

# 预期目标：
目标一：实现函数感知的轻量级虚拟机内存垂直缩放技术，避免对非函数应用的影响
目标二: 将内存垂直缩放的时间开销降低到亚毫秒级
目标三：将轻量级虚拟机内存垂直缩放技术应用到服务器无感知计算平台中，以实现高弹性的资源分配

# 赛题分类
2.3.1 虚拟化

# License
GPL-3.0 License

# 项目导师
- 姓名：吴松
- 单位：华中科技大学
- email: wusong@hust.edu.cn
