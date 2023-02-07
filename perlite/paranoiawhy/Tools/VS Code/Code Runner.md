# `ts` 文件 (`typescript`)

## 安装依赖

须全局安装以下依赖:

```bash
npm i typescript -g
npm i ts-node -g
npm i @types/node -g
```

## `setting.json` 配置

> [!配置]
> ```json
> "code-runner.clearPreviousOutput": true,
> "code-runner.saveFileBeforeRun": true,
> "code-runner.runInTerminal": true,
> "code-runner.executorMap": {
> 	// "javascript": "node",
> 	"typescript": "ts-node",
> }
> ```

> [!tip]
> - 可用 `Code Runner` 插件直接运行 `ts` 文件
> - 可在终端下运行 `tsc index.ts` 将其转换为 `index.js`
> - 可在终端下运行 `ts-node index.ts` 运行 `ts` 文件

```json
        "build": "tsc obsidian.d.ts && rollup obsidian.js -f iife -o ./dist/obsidian.iife.js"
```