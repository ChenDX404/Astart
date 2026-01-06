
# A* & Weighted A* Maze Pathfinding (with Visualization + EXE)

> Course Project — Classic AI Search in a Real(ish) Navigation Scenario  
> 本项目实现并对比 **A\*** 与 **Weighted A\***（加权启发式搜索），在二维网格迷宫路径规划任务上完成：  
> ✅ 算法实现 ✅ 批量实验 ✅ 指标统计 ✅ 可视化演示（动画/GUI）✅ 可打包 EXE 展示

---

## ✨ Project Highlights（亮点）
- **标准 A\***：在可采纳启发式下可保证最优路径（最短路）
- **Weighted A\***：通过 `f = g + w·h` 提供可调节的“速度—质量”折中
- **实验对比**：自动输出 `results.csv` + 关键曲线图（扩展节点数 / 时间 / 路径代价）
- **可视化演示 App（app.py）**：动态展示搜索扩展过程与最终路径，适合答辩演示加分
- **工程化交付**：目录清晰、可复现实验、可一键打包 Windows EXE

---

## 📌 Background / Motivation（背景）
路径规划是机器人导航、室内定位、仓储AGV、游戏AI寻路等任务的核心能力。  
本项目将迷宫路径规划建模为经典的**状态空间搜索问题**，使用启发式信息（Manhattan distance）提升搜索效率，并通过加权策略分析启发式强弱对性能与最优性的影响。

---

## 🧠 Algorithms（算法简介）
### A*
评价函数：
\[
f(n)=g(n)+h(n)
\]
- `g(n)`：从起点到当前节点的真实代价
- `h(n)`：到目标的启发式估计（本项目使用 Manhattan distance）
- 在 `h(n)` 可采纳时，A* 可得到**最优路径**

### Weighted A*
评价函数：
\[
f(n)=g(n)+w\cdot h(n), \; w\ge 1
\]
- `w=1` 等价于标准 A*
- `w>1` 更“贪心”，通常**扩展更少、速度更快**，但可能**牺牲最优性**

---

## 📂 Repository Structure（目录结构）


```

.
├── app.py                      # 可视化演示程序（GUI/App，支持动态展示路径与扩展过程）
├── astar_weighted.py            # A* / Weighted A* 核心实现
├── maze_gen.py                  # 迷宫生成与读写（0通行 / 1障碍）
├── run_experiments.py           # 批量实验：输出 results.csv + 曲线图
├── make_gif.py                  # 生成演示 GIF（不同 w 的路径对比）
├── requirements.txt             # 依赖
└── results/                     # 运行后生成：csv、png 图、gif 等

````

---

## ✅ Quick Start（快速开始）
### 1) Environment（环境）
- Python 3.9+（建议 3.10/3.11）
- Windows / macOS / Linux 均可运行

### 2) Install dependencies（安装依赖）
```bash
pip install -r requirements.txt
````

如果你没用 requirements.txt，也可以：

```bash
pip install numpy pandas matplotlib imageio
```

---

## 🧪 Run Experiments（运行批量实验：生成 CSV + 曲线图）

```bash
python run_experiments.py
```

运行后将在 `results/` 生成：

* `results.csv`
* `expansions_vs_weight.png`
* `time_s_vs_weight.png`
* `path_cost_vs_weight.png`

---

## 🎬 Generate GIF Demo（生成 GIF 动画，可选加分）

```bash
python make_gif.py
```

运行后生成：

* `results/weighted_astar_demo.gif`

---

## 🖥️ Run Visualization App（运行可视化演示程序：app.py）



```bash
python app.py
```

你可以在界面里：

* 生成新迷宫
* 选择权重 `w`（1.0 / 1.2 / 1.5 / 2.0）
* 观察 **w 增大时搜索更快但路径可能更绕** 的效果

---

## 🧰 Build Windows EXE（可选：打包 EXE）

> 如果你想交“可执行程序”或演示更像产品，可打包成 exe

### 1) Install PyInstaller

```bash
pip install pyinstaller
```

### 2) Build

```bash
pyinstaller -F -w app.py
```

生成的可执行文件在：

```
dist/app.exe
```

---

## 📊 Metrics（实验指标）

* **expansions**：扩展节点数（越少通常越快）
* **time_s**：运行时间
* **path_cost**：路径总代价（越小越接近最优）

项目核心结论：

> 随着 `w` 增大，通常可以显著减少 expansions/时间，但 path_cost 可能上升（不再保证最优）。

---

## 📌 Notes（说明）

* 迷宫使用随机生成并保证连通（起点到终点必有路）
* 默认使用四邻接移动（上下左右），如需可扩展为八邻接 + Octile heuristic

---

## License

```
