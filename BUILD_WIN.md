# Windows 构建指南

## 构建命令

```bash
npm run dist:win
```

## 产物

- **路径**: `out\win-unpacked\AionUi.exe`
- **类型**: 便携版，直接双击运行，无需安装

## 注意事项

1. **构建前先关闭 AionUi** — 如果 `out\win-unpacked\AionUi.exe` 正在运行，构建会报 `EBUSY` 错误
2. **不要用** `npm run package` — 这个命令只跑 electron-forge，不会重建 native 模块（better-sqlite3），打出来的包会报错
3. `out\AionUi-win32-x64` 是中间产物，不可用；`out\win-unpacked` 才是最终可用的产物

## 构建流程

```
npm run dist:win
  → electron-forge package (webpack 编译 TypeScript)
  → electron-builder (afterPack.js 重建 better-sqlite3 native 模块)
  → 输出到 out\win-unpacked\
```

## 配置说明

- `electron-builder.yml` 中 win target 设为 `dir`，只生成目录，不压缩 zip
- 如需生成 zip 或 NSIS 安装包，修改 `electron-builder.yml` 的 `win.target`
