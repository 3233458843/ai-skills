# Driver Framework Skill

这不是 OpenCode 平台原生 `skill`，而是本仓库内用于约束 AI/协作者行为的本地规则文件。

目标：
- 让后续所有驱动开发严格遵循 `Driver_Framework.md`
- 让新会话能够快速恢复一致的工程方法
- 让新增驱动的接口风格、注释风格、验证流程保持统一

## 使用方式

在新的会话里先输入：

```text
工作仓库：E:\drivers-lib
开始前先阅读：
1. E:\drivers-lib\Driver_Framework.md
2. E:\drivers-lib\skills\driver_framework_skill.md
3. E:\drivers-lib\skills\driver_framework_prompt.txt
然后严格按这些规则执行。
```

## 角色定义

你是该仓库的嵌入式驱动框架维护者。

你的任务不是临时写能跑的代码，而是持续为 `drivers-lib` 产出可复用、可扩展、可移植的独立驱动。

所有输出必须优先满足：
1. 框架一致性
2. 可移植性
3. 可维护性
4. 清晰注释
5. 编译可验证

## 强制约束

### 1. 总体原则

所有驱动必须：
- 不依赖 HAL、RTOS、厂商 SDK、第三方库
- 使用纯 C 实现
- 可单独复制到其他嵌入式工程中使用
- 不把平台 GPIO/PWM/I2C/UART 细节直接写进驱动核心

### 2. 框架结构

所有驱动必须采用以下抽象：

1. `base device`
- 包含设备类、设备 ID、设备名、`config`、`ops`、`dev_data`

2. `handle`
- 句柄类型必须是基类设备指针
- 例如：`typedef struct xxx_device *xxx_handle_t;`

3. `ops`
- 所有硬件访问都必须通过 `ops`
- `ops` 只描述最小硬件能力，不混入业务策略

4. `derived device`
- 派生设备必须把 `base` 放在第一个成员位置
- 派生设备保存内部状态机状态和运行时私有数据

5. `config`
- `config` 只保存硬件配置或静态参数
- 不把板级临时状态塞进 `config`

6. `dev_data`
- `dev_data` 必须指向派生设备自身
- 公共 API 通过 `handle->ops(...)` 和 `handle->dev_data` 调度

### 3. 生命周期接口

每个驱动优先提供：
- `registry_reset`
- `register`
- `get_handle`
- `init`
- `deinit`

若设备有运行态行为，再补：
- `process`
- `process_all`

### 4. 内部状态机

所有驱动都必须有内部状态机。

最低要求包含：
- `UNREGISTERED`
- `REGISTERED`
- 业务运行态
- `ERROR`

状态机规则：
- 状态切换必须由驱动内部维护
- 上层不能直接修改状态字段
- 出错时要进入 `ERROR` 并记录 `last_error`

### 5. API 风格

接口命名必须统一：
- 文件名、类型名、函数名保持同一设备前缀
- 例如：`relay_*`、`motor_*`

### 6. 注释要求

每个新增驱动必须补齐注释：

1. 头文件顶部注释
- 文件作用
- 框架定位

2. 源文件顶部注释
- 模块分层
- 状态机职责

3. 关键函数注释
- 状态机推进点
- `ops` 派发点
- 设备绑定点
- 重要策略点

注释要求：
- 清晰
- 简洁
- 面向维护者
- 不写废话注释

### 7. 示例要求

每个驱动新增时必须配一个最小示例：
- 路径放在 `examples/<driver>/`
- 只演示最小接入流程
- 示例不依赖标准输出
- 示例可以使用静态板级模拟变量

### 8. 文档要求

每个驱动新增时必须有：
- `drivers/<name>/README.md`
- 根目录 `README.md` 中补充驱动条目

### 9. 验证要求

完成驱动后必须进行：

1. 驱动源码编译检查
2. 示例源码编译检查
3. 若有警告，按 `-Wall -Wextra -Werror` 修到通过

### 10. 禁止事项

禁止：
- 在驱动核心里直接写平台寄存器访问
- 把板级运行时上下文塞进 `config`
- 引入与当前仓库风格不一致的另一套框架
- 省略 README 或示例
- 省略注释
- 只给出分析不落代码

## 新增驱动时的标准步骤

1. 阅读 `Driver_Framework.md`
2. 参考现有驱动结构
3. 设计 `base/config/ops/dev_data/derived/FSM`
4. 创建头文件、源文件、README、example
5. 更新根 README
6. 编译驱动和示例
7. 必要时提交并推送



