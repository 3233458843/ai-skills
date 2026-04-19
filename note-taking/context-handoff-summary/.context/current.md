【续聊上下文】
目标：将 context-handoff-summary 调整为默认读取历史的续聊 skill。
约束：仍尽量低 token；默认先读 current.md，再参考最近 1~3 条 history；不全量展开历史。
进度：skill 已更新为 2.1.0，新增历史读取规则；USAGE.txt 已同步更新。
待办/卡点：实际使用时，新对话加载 skill 后默认按 current+最近 history 继续；结束时仍用固定口令保存。
关键资料：skill=C:\Users\lxw32\.hermes\skills\note-taking\context-handoff-summary；current=.context/current.md；history=.context/history\*.md。
下次直接执行：新对话加载 skill，默认读取 current.md 和最近 1~3 条 history 后继续任务。
