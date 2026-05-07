【续聊上下文】
目标：XST_Demo 掌静脉驱动已具备完整事件驱动框架，后续聚焦应用层命令交互、DMA 优化、多模组支持。
约束：xst_drv.c 零 HAL 依赖；平台代码在 porting 层 #if 条件编译；静态内存池无 malloc；单线程；严格遵循 driver_Framework skill。
进度：v2.1 完成 — ①事件系统(REPLY/NOTE/DATA/ERROR+回调) ②7状态帧解析机+XOR校验+超时 ③UART中断链路(ISR→lwrb→解析→回调) ④PDF协议常量对齐(MCU_NID_AUTHORIZATION 5→8, MR_FAILED4_AUTHORIZATION 18→14, MID_QUIT 0xFE→0xFF) ⑤event_t改为指针省16KB RAM ⑥parsed_data 4096适配4000B批量帧 ⑦linker加shellCommand段 ⑧新文档XST_DRIVER.md(11章含5平台实例) ⑨去goto+校验函数化xst_calc_checksum ⑩xst_porting.c多平台骨架。
待办/卡点：应用层send命令API未实现；DMA接收未适配；TX状态机缺失。
关键资料：bsp/xst_driver/xst_drv.h, xst_drv.c, xst_pack_t.h, porting/xst_porting.h/.c, XST_DRIVER.md; Core/Src/main.c; STM32F411XX_FLASH.ld(已加shellCommand段); PDF协议 E:\Desktop\毕业\掌静脉资料\。
下次直接执行：先读 current.md；继续在现有框架上增量开发，不改核心引擎架构；porting 层扩展新平台时在 #elif 分支加 4 个 ops 函数。
