# Tintide Roadmap

Language: **English (en-US)** | [简体中文 (zh-CN)](#简体中文-zh-cn)

This roadmap is intentionally incremental. Each stage should leave the
project runnable and understandable before the next layer is added.

## Status

- [x] Project concept and architecture documented
- [ ] M0: initialize the implementation and define the core model
- [ ] v0.1: first dynamic theme and CLI MVP
- [ ] v0.2: user-authored themes
- [ ] v0.3: GUI color studio
- [ ] v0.4: application adapters
- [ ] v0.5: background daemon
- [ ] v1.0: stable ecosystem and desktop integration

## M0: Foundation

Goal: establish a small, testable core before adding astronomy or GUI code.

Deliverables:

- choose the implementation language and dependency policy;
- define semantic palette types and serialization;
- add the built-in base palette as data, not scattered constants;
- implement `tintide palette` with text and JSON output;
- add unit tests for parsing, serialization, and palette completeness;
- document the local build, format, lint, and test commands.

Exit criteria: a new contributor can clone the project, run the CLI, inspect the
palette, and understand the core types.

## v0.1: CLI MVP

Goal: one complete, hand-designed theme that changes continuously through the
year and the day.

Deliverables:

- OKLab/OKLCH conversion through a maintained color library;
- interpolation with hue wrapping and low-chroma handling;
- 24 solar-term annual keyframes;
- sunrise, solar noon, sunset, and solar-midnight daily keyframes;
- time zone and explicit latitude/longitude configuration;
- deterministic `tintide show --at <instant>` output;
- gamut mapping and WCAG contrast checks;
- JSON output containing both final colors and useful metadata;
- sampled full-year tests for continuity, contrast, gamut, and invalid values.

The MVP does not include a GUI, automatic geolocation, desktop theme updates,
or a second built-in theme.

Exit criteria:

- all 24 solar terms work as keyframes;
- annual and daily cycles have no visible boundary jump;
- the CLI can show the base palette and a requested instant;
- generated colors pass configured gamut and contrast constraints;
- a full-year preview is usable as a daily theme.

## v0.2: User-authored themes

Goal: let users define and validate their own seed palette and keyframes.

Deliverables:

- versioned TOML or JSON theme format;
- base colors in OKLCH with semantic role names;
- annual and daily modifier keyframes;
- locked roles that do not drift with time;
- `tintide validate <theme>` and preview commands;
- import of compatible static themes where practical;
- migration rules for future format changes.

## v0.3: Tintide Studio

Goal: make theme design accessible without editing numbers by hand.

Deliverables:

- sliders for lightness, chroma, temperature, contrast, and cycle strength;
- per-role color editing and lock controls;
- draggable day and year timelines;
- previews for terminal, editor, and generic UI;
- visible gamut, contrast, and color-distance warnings;
- import/export of the versioned theme format.

The GUI must call the same core engine as the CLI; it must not implement a
second color algorithm.

## v0.4: Application adapters

Start with formats that have strong existing conventions:

- Base16/Base24;
- Kitty or Alacritty;
- Neovim;
- Waybar, Rofi, and Dunst.

Each adapter should be tested independently and should consume semantic colors
from the core rather than reaching into interpolation internals.

## v0.5: Background updates

Goal: update supported applications when the perceptual change is meaningful.

Deliverables:

- a daemon or scheduled mode;
- debounced updates based on perceptual color distance;
- explicit manual pause and override;
- logs and a dry-run mode;
- robust behavior during sleep, resume, clock changes, and polar day/night.

## v1.0: Stable platform

Before calling the project stable:

- freeze and document the theme format;
- publish the core API and adapter interface;
- provide reproducible previews and regression fixtures;
- document accessibility and contrast assumptions;
- package for at least one target platform;
- choose and publish an open-source license;
- add contribution, release, and security guidance.

---

## 简体中文 (zh-CN)

这份路线图刻意采用渐进式设计。每个阶段都应该让项目保持可运行、可理解，再进入下一层。

## 状态

- [x] 已记录项目概念和架构
- [ ] M0：初始化实现并定义核心模型
- [ ] v0.1：第一个动态主题和 CLI MVP
- [ ] v0.2：用户自定义主题
- [ ] v0.3：GUI 配色工作台
- [ ] v0.4：应用适配器
- [ ] v0.5：后台 daemon
- [ ] v1.0：稳定的生态和桌面集成

## M0：基础设施

目标：在加入天文计算和 GUI 之前，先建立小而可测试的核心。

产物：确定实现语言和依赖策略；定义语义 Palette 类型及其序列化；把内置基础 Palette 作为数据保存；
实现支持文本和 JSON 的 `tintide palette`；为解析、序列化和 Palette 完整性添加单元测试；记录本地构建、格式化、
静态检查和测试命令。

完成标准：新贡献者可以克隆项目、运行 CLI、查看 Palette，并理解核心类型。

## v0.1：CLI MVP

目标：完成一套由作者设计的主题，使它在全年和一天中连续变化。

产物：通过维护中的颜色库完成 OKLab/OKLCH 转换；处理色相绕回和低色度颜色的插值；二十四节气年度关键帧；
日出、正午、日落和午夜日内关键帧；时区和显式经纬度配置；确定性的 `tintide show --at <instant>`；
色域映射和 WCAG 对比度检查；包含最终颜色和元数据的 JSON；全年采样测试，检查连续性、对比度、色域和无效值。

MVP 不包含 GUI、自动定位、桌面主题更新或第二套内置主题。

完成标准：24 个节气都能作为关键帧；年度和日内周期没有明显边界跳变；CLI 能查看基础 Palette 和指定时刻；
颜色通过配置的色域及对比度约束；全年预览可以作为日常主题使用。

## v0.2：用户自定义主题

目标：允许用户定义并校验自己的种子 Palette 和关键帧。

产物：带版本的 TOML 或 JSON 主题格式；使用 OKLCH 和语义角色名保存基础颜色；年度和日内修饰关键帧；
不随时间漂移的锁定角色；`tintide validate <theme>` 和预览命令；在可行时导入静态主题；未来格式变更的迁移规则。

## v0.3：Tintide Studio

目标：不手动编辑数字也能设计主题。

产物：明度、色度、冷暖、对比度和周期强度滑条；单个角色编辑和锁定；可拖动的一日及年度时间轴；
终端、编辑器和普通 UI 预览；色域、对比度和颜色距离警告；主题格式的导入导出。

GUI 必须调用与 CLI 相同的核心引擎，不能实现第二套颜色算法。

## v0.4：应用适配器

优先支持已有约定成熟的格式：Base16/Base24、Kitty 或 Alacritty、Neovim、Waybar/Rofi/Dunst。

每个适配器都应独立测试，只消费核心输出的语义颜色，不直接访问插值内部实现。

## v0.5：后台更新

目标：只有感知上的变化足够明显时才更新支持的应用。

产物：daemon 或定时运行模式；基于感知色差的防抖更新；手动暂停和覆盖；日志及 dry-run；
正确处理睡眠唤醒、时钟变更以及极昼极夜。

## v1.0：稳定平台

稳定发布前需要冻结并记录主题格式；发布核心 API 和适配器接口；提供可复现预览及回归样例；
记录可访问性和对比度假设；至少为一个目标平台打包；选择并发布开源许可证；补充贡献、发布和安全指南。
