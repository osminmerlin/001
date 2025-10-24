# Quit Smoking Tracker / 吸烟助手

This is a lightweight, privacy-first single-page app (static HTML + JavaScript + CSS) for tracking smoking-related "punch" events (打卡). It runs entirely in the browser and stores all data locally using localStorage. No backend or account is required.

本项目是一个轻量级、注重隐私的单页应用（静态 HTML + JavaScript + CSS），用于记录与吸烟相关的“打卡”事件。所有数据仅保存在浏览器的 localStorage 中，无需后端或账号。

---

## Features / 功能

- Quick "punch" (打卡) to record the current time when a smoking event occurs.
- Daily summary: count, earliest/latest times, average interval between punches.
- Predicts how the average interval would change if you punch now.
- Recent history list (shows up to 5 most recent punches for today).
- Analysis section comparing today to yesterday and the same day last week.
- Encouragement area with a simple "quit progress" visual (progress bar).
- Reports modal with charts:
  - Daily hourly distribution chart (Chart.js)
  - Monthly & yearly placeholders (chart canvases included)
- Simple settings modal to customize:
  - App title
  - Today card title
  - Punch behavior name (e.g., "吸烟")
- All UI is responsive and designed for mobile devices.

- 快速「打卡」记录当前时间
- 每日报表：次数、最早/最晚时间、平均间隔
- 预测当前打卡后平均间隔会如何变化
- 最近打卡记录列表（显示今日最近最多 5 条）
- 数据分析：与昨日及上周同日对比
- 鼓励模块，包含简单的「戒烟进度」进度条
- 报告弹窗（含 Chart.js 图表）
- 设置弹窗：自定义应用标题、今日卡片标题、打卡行为名称
- 响应式设计，适配移动端

---

## How to use / 使用方法

1. Open index.html in a browser (desktop or mobile) or host the folder on a static server.
   - You can simply double-click the file or run a static server (e.g., `npx http-server`).
2. Tap the main punch button to record a smoking event.
3. Click the "📊" reports button to open the reports modal and view charts by day/month/year.
4. Click the "⚙️" settings button to change titles or the punch name.
5. All data is stored locally. Clearing the browser storage will remove saved punches and settings.

1. 在浏览器中打开 index.html（桌面或移动端），或将目录放到静态服务器上托管。
   - 可以直接双击打开文件，或运行静态服务器（如 `npx http-server`）。
2. 点击页面上的打卡按钮记录一次事件。
3. 点击“📊”按钮打开报告弹窗，查看日/月/年图表。
4. 点击“⚙️”按钮进入设置，修改应用标题、今日标题或打卡名称。
5. 所有数据保存在本地，清除浏览器存储将删除打卡记录与设置。

---

## Data & Storage / 数据与存储

- localStorage keys used:
  - `punches` — JSON array of punch objects
  - `settings` — JSON object containing the app settings

Punch object structure:
- id: timestamp-based unique id (Number)
- timestamp: epoch milliseconds (Number)
- date: YYYY-MM-DD string (local date)
- time: localized time string used for display (e.g., "14:30")

示例：
- localStorage 键：
  - `punches` — 打卡对象数组（JSON）
  - `settings` — 设置对象（JSON）

打卡对象结构：
- id：基于时间戳的唯一 ID（Number）
- timestamp：毫秒级时间戳（Number）
- date：本地日期字符串（YYYY-MM-DD）
- time：用于展示的本地时间字符串（例如 "14:30"）

Note: All data is local to the browser. There is no sync or cloud backup.

注意：所有数据仅保存在浏览器本地，不会同步或备份到云端。

---

## Dependencies / 依赖

- Chart.js (loaded via CDN)
  - <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

Charts are created dynamically when the reports modal is opened or when the selected date changes.

图表通过 CDN 加载的 Chart.js 渲染（在 index.html 中引入）。

---

## File overview / 文件概览

- index.html — The whole app (HTML, CSS, and JavaScript bundled in one file)
  - Contains UI components: header, punch card, history, daily report, settings modal, reports modal, notification component.
  - All app logic lives in inline <script> in index.html.
- icon-192.png, icon-512.png — App icons referenced in the head (if present)

- index.html — 含全部应用代码（HTML、CSS、JavaScript）
  - 包含主界面、打卡卡片、历史、日报表、设置弹窗、报告弹窗、通知组件
  - 应用逻辑直接写在 index.html 的内联 <script> 中
- icon-192.png, icon-512.png — 页面中引用的图标（若存在）

---

## Customization / 自定义

- App look & feel: edit CSS variables in the <style> :root at the top of index.html
  - --primary-color, --gradient, --background-color, border radius, etc.
- Change default settings (initial values) by editing the state.settings object in the script.
- Chart appearance: adjust Chart.js dataset options in generateDailyChart / generateMonthlyChart / generateYearlyChart.

- 样式与配色：编辑 index.html 顶部 :root 中的 CSS 变量
  - 如 --primary-color、--gradient、--background-color、圆角等
- 默认设置：在脚本中修改 state.settings 的初始值
- 图表样式：修改 generateDailyChart / generateMonthlyChart / generateYearlyChart 中的数据集选项

---

## Developer notes / 开发者说明

Key JavaScript functions and state:
- state — holds:
  - punches: array
  - settings: { appTitle, todayCardTitle, punchName }
  - charts: { daily, monthly, yearly } (Chart.js instances)
- initApp() — initializes elements, loads data, attaches listeners.
- loadData() / saveData() — read/write localStorage.
- handlePunch() — create a punch entry for current time and save.
- renderUI() — update counts, average interval, history list, daily report, analysis, encouragement.
- generateDailyChart(date) — builds hourly bar chart for a given date.
- generateMonthlyChart(), generateYearlyChart() — placeholders included (can be implemented to aggregate by month/year).
- generateAnalysisReport() — compares today with yesterday and last week and gives a simple trend message.
- generateEncouragement() — shows friendly messages and a crude progress-based progress bar.

重要函数与状态说明：
- state：
  - punches：打卡数组
  - settings：{ appTitle, todayCardTitle, punchName }
  - charts：{ daily, monthly, yearly }（Chart.js 实例）
- initApp()：初始化元素、加载数据并绑定事件
- loadData() / saveData()：读写 localStorage
- handlePunch()：记录当前时间的打卡并保存
- renderUI()：更新界面数据、每日报表、分析与鼓励模块
- generateDailyChart(date)：为指定日期生成按小时统计的柱状图
- generateMonthlyChart(), generateYearlyChart()：月/年图表占位，可实现月/年聚合
- generateAnalysisReport()：与昨日/上周对比并给出趋势分析
- generateEncouragement()：展示鼓励信息和简单进度条

---

## Known limitations / 已知限制

- Data is stored only in localStorage — if the user clears browser data, punches will be lost.
- No import/export functionality for backup.
- Monthly/yearly charts are scaffolded but may need additional aggregation logic depending on desired behavior.
- Timezone/localization uses the browser locale; tests needed for cross-timezone usage if you open the page in different locales.

- 数据仅保存在 localStorage，清除浏览器数据将丢失记录
- 暂无导入/导出功能来备份数据
- 月/年图表需要根据实际需求扩展聚合逻辑
- 时间使用浏览器本地设置，跨时区使用需额外测试

---

## Suggestions / 建议

- Add an export/import CSV or JSON feature for backup and analysis.
- Provide an option to choose between 24-hour / 12-hour format.
- Add a confirmation for accidental multi-taps (debounce punch button).
- Implement monthly/yearly aggregation and summary charts.
- Add optional passcode or browser-based encryption for increased privacy.
- 增加导出/导入 CSV 或 JSON 的功能用于备份与分析
- 提供 24 小时 / 12 小时格式切换
- 防止重复快速点击（防抖/节流）
- 完善月/年聚合统计并增加图表展示
- 可选的本地加密/密码保护以增强隐私

---

## License / 许可

You can add a license file as needed (e.g., MIT). The project currently has no license file included.

可根据需要添加许可证（例如 MIT）。当前仓库中未包含许可证文件。

---

If you'd like, I can:
- generate a README file in the repository,
- add export/import functionality,
- implement monthly/yearly aggregation and examples,
- or translate in a different tone (shorter/longer).

如果你需要，我可以：
- 直接在仓库中生成 README 文件，
- 添加导出/导入功能，
- 完成月/年聚合并实现相应图表，
- 或者用不同风格（更短或更详细）重写 README。
