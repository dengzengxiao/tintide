# Tintide

> A time-aware color scheme generator for calm, adaptive computing.

This project is at the design and scaffolding stage. The repository currently
contains documentation only; the CLI and color engine are not implemented yet.

Language: **English (en-US)** | [简体中文 (zh-CN)](#简体中文-zh-cn)

## Vision

Tintide generates a low-stimulation color scheme that changes smoothly with
the time of day and the annual cycle. The visual direction is inspired by
Everforest: soft contrast, restrained chroma, and colors that remain useful
for long sessions.

The long-term goal is a desktop environment whose applications adapt to the
same time-aware scheme. The first goal is deliberately smaller: a deterministic
CLI and a reusable color engine.

## MVP

The first milestone contains one hand-designed built-in theme and supports:

- a semantic base palette;
- the 24 solar terms as annual keyframes;
- sunrise, solar noon, sunset, and solar midnight as daily keyframes;
- smooth interpolation between keyframes;
- color gamut and contrast validation;
- CLI output for the base palette and any requested instant;
- human-readable terminal output and JSON output.

Planned examples (not implemented yet):

```text
tintide palette
tintide show --at 2026-10-23T18:30:00+08:00
tintide show --format json
```

## Color model

OKLCH is the user-facing configuration space. OKLab or OKLCH may be used for
interpolation, with explicit handling for hue wrapping and low-chroma colors.
The final colors are converted to sRGB, mapped into gamut, and checked for
contrast before export.

The internal palette is semantic rather than tied to one application format:

```text
background  surface  foreground  muted  border  selection
red  orange  yellow  green  aqua  blue  purple
```

Application formats such as Base16, terminal colors, editor themes, and GTK or
KDE themes belong to a later adapter layer.

## Proposed architecture

```text
tintide-core    time model, color math, interpolation, validation
tintide-cli     commands, configuration, terminal and JSON output
tintide-studio  future GUI editor and timeline preview
tintide-daemon  future background updater for desktop applications
```

The core should remain deterministic and free of I/O. Given the same theme,
location, time zone, and instant, it must produce the same result.

## Development

Read [AGENTS.md](AGENTS.md) before changing the project. The staged plan is in
[ROADMAP.md](ROADMAP.md). The next implementation task is to create the
smallest vertical slice: a hard-coded semantic palette and `tintide palette`.

During early development, prefer small changes that compile, have focused
tests, and can be inspected with `git diff`. Do not add GUI, desktop daemons,
automatic location lookup, or broad application integrations before the MVP is
usable.

## License

No license has been selected yet.

---

## 简体中文 (zh-CN)

> 一个让配色随时间平滑变化、并尽量保持舒适的 color scheme 生成器。

项目目前处于设计和脚手架阶段。仓库现在只有文档，CLI 和颜色引擎尚未实现。

## 愿景

Tintide 根据一天中的时间和一年中的季节周期，生成平滑变化的配色方案。视觉方向参考
Everforest：柔和的对比度、克制的色度，以及适合长时间使用的颜色。

长期目标是让桌面环境中的应用共享同一套随时间变化的配色。第一阶段会保持小而完整：
先实现确定性的 CLI 和可复用的颜色引擎。

## MVP

第一个里程碑包含一套由项目作者设计的内置主题，并支持：

- 语义化基础 Palette；
- 二十四节气作为年度关键帧；
- 日出、正午、日落和午夜作为日内关键帧；
- 关键帧之间的平滑插值；
- 色域和对比度校验；
- CLI 查看基础 Palette 和任意指定时刻的配色；
- 人类可读的终端输出以及 JSON 输出。

计划中的命令示例（当前尚未实现）：

```text
tintide palette
tintide show --at 2026-10-23T18:30:00+08:00
tintide show --format json
```

## 颜色模型

OKLCH 是面向用户的配置空间。插值可以使用 OKLab 或 OKLCH，但必须明确处理色相绕回和低色度颜色。
最终颜色转换到 sRGB，执行色域映射，并在导出前进行对比度检查。

内部 Palette 使用语义角色，不绑定某一种应用格式：

```text
background  surface  foreground  muted  border  selection
red  orange  yellow  green  aqua  blue  purple
```

Base16、终端颜色、编辑器主题以及 GTK/KDE 主题等应用格式属于后续适配层。

## 计划中的架构

```text
tintide-core    时间模型、颜色计算、插值、校验
tintide-cli     命令、配置、终端和 JSON 输出
tintide-studio  未来的 GUI 编辑器和时间轴预览
tintide-daemon  未来用于更新桌面应用的后台服务
```

核心库应保持确定性并且不负责 I/O。相同的主题、位置、时区和时刻必须产生相同结果。

## 开发

修改项目之前请先阅读 [AGENTS.md](AGENTS.md)，阶段计划见 [ROADMAP.md](ROADMAP.md)。下一项开发任务是完成最小纵向切片：
一套硬编码的语义 Palette，以及 `tintide palette` 命令。

早期开发优先选择能编译、带有针对性测试、并且可以通过 `git diff` 检查的小改动。在 MVP 可用前，
不要加入 GUI、桌面 daemon、自动定位或大规模应用适配。

## 许可证

项目尚未选择许可证。
