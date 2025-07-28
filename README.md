# MazeMaster-AI-Report

## 1. PEAS Framework – MazeMaster AI

The PEAS framework helps define the characteristics of an intelligent agent. Here's how it applies to our MazeMaster AI:

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Performance** | Successfully reach the goal from the start point using the **shortest path**. |
| **Environment** | A **static 10x10 maze**, represented as a 2D grid with walls and open paths.  |
| **Actuators**   | The agent can **move** in four directions: **up, down, left, right**.         |
| **Sensors**     | The agent senses its **current position** and the **state of adjacent cells** (walkable or blocked). |

## 2. Maze Modeling – Environment Representation

The maze is modeled as a 10x10 grid using a 2D Python list. Each cell contains:

- `'#'` → Wall
- `'.'` → Walkable Path
- `'S'` → Start Point
- `'G'` → Goal Point

Example snippet of the maze:

```python
maze = [
    ['#', 'G', '#', '#', '#', '#', '#', '#', '#', '#'],
    ...
    ['.', '.', '.', '.', '#', '#', '#', '#', 'S', '#']
]
```


---

## 3. Search Strategy – Breadth-First Search (BFS)

Breadth-First Search (BFS) is an uninformed search algorithm that explores all neighboring nodes before moving to the next level. It guarantees the **shortest path** in unweighted grids like our maze.

### Why BFS?
- All movements have equal cost.
- Maze is static and unweighted.
- BFS ensures optimality (shortest path).

### Implementation Summary:
- Uses a **queue** to store current position and the path so far.
- Maintains a **visited set** to avoid revisits.
- Explores 4 directions (up, down, left, right) from each step.
- Returns the full path once the goal is reached.

### Example Output:
```python
[(9, 8), (9, 7), (9, 6), ..., (0, 1)]
```

---

## 4. Visualizing the Path – Plotting the Agent’s Journey

To better understand and demonstrate how the AI agent navigates the maze, we created a visual representation of the path found using BFS.

### Key Features:
- **Yellow** → Walkable paths
- **Black** → Walls
- **Blue** → Start point
- **Green** → Goal point
- **Red Line** → Agent's shortest path

### Implementation:
We used `matplotlib` and `ListedColormap` to color-code the maze. The path was plotted using `plt.plot()` with red lines and circular markers to indicate steps in the route.

This visualization gives insight into how the agent performs and helps in debugging or comparing other algorithms.

## 5. Search Strategy Comparison – BFS vs DFS

To explore different approaches to maze-solving, we implemented and compared two classic search strategies: **Breadth-First Search (BFS)** and **Depth-First Search (DFS)**.

### ✅ Observations Based on Our Maze:

| Feature            | BFS                                | DFS                             |
|--------------------|-------------------------------------|----------------------------------|
| Path Optimality     | ✅ Shortest path guaranteed          | ❌ May take longer/indirect path |
| Search Behavior     | Explores level-by-level             | Goes deep in one direction first |
| Memory Usage        | Higher (queue stores more paths)    | Lower (uses stack, fewer nodes)  |
| Final Path Length   | *Shorter*                           | *Usually longer*                 |
| Visualization Color | 🔴 Red Path                         | 🟪 Purple Path                    |

### 💡 Visual Insight:
Both BFS and DFS reached the goal, but BFS found the shortest route. DFS explored deeper paths first, which sometimes led to dead ends or loops.

The visual overlay shows how BFS moves more uniformly, while DFS sometimes curves or detours.

### 👩‍💻 Implementation Status:
- BFS and DFS functions implemented in Python
- Paths visualized over the maze using `matplotlib`
- Color-coded overlays helped compare agent behavior directly

  ## 6. Animated Agent Movement – BFS & DFS

To enhance the clarity and impact of our maze-solving AI, we implemented **animated visualizations** of both the BFS and DFS algorithms. Rather than static path plots, these animations show the agent moving through the maze **step by step**, providing deeper insight into how each algorithm operates in real time.

### ✨ Key Features:
- **Trail Effect**: As the agent moves, it leaves a visual trail behind, highlighting its exploration path dynamically.
- **Real-Time Progress**: Each movement is shown with a slight delay, simulating how an agent would explore a physical maze.
- **Color-Coded Agents**:
  - 🔴 **BFS Agent**: Red trail + dot (shows shortest-path behavior)
  - 🟪 **DFS Agent**: Purple trail + dot (shows depth-first behavior)

### 🧠 Insights Gained:
- BFS's animation reveals a systematic, level-wise exploration towards the shortest path.
- DFS shows deeper probes into the maze, often exploring subpaths before backtracking.

These animations help both technically and visually:
- **Technical learners** can observe the algorithm’s behavior
- **Non-technical viewers** can visually understand how pathfinding works

### 📽️ Tools Used:
- Python’s `matplotlib` for grid and animation
- `time.sleep()` + `clear_output()` for real-time simulation
- Custom trail color mapping for aesthetic clarity

### 📌 Implementation Status:
- Both BFS and DFS animations are integrated into the notebook.
- Optional: These can be exported as GIFs for use in presentations, reports, or GitHub README.

  ## 7. Evaluation & Metrics

To evaluate the effectiveness of our pathfinding agents, we compared the three algorithms—**BFS, DFS, and A\***—on the same 10x10 maze.

### 📊 7.1 Performance Metrics

| Algorithm | Path Found | Path Length | Optimality | Search Strategy        |
|-----------|------------|-------------|------------|------------------------|
| BFS       | ✅          | 21 steps     | ✅ Optimal  | Level-wise (Breadth)  |
| DFS       | ✅          | 29 steps     | ❌ Sub-optimal | Deep-first (can backtrack) |
| A*        | ✅          | 21 steps     | ✅ Optimal  | Smart + Heuristic-based |

> *Note: Path lengths may vary based on maze structure.*

---

### ⏱️ 7.2 Time & Efficiency

- All three algorithms completed within milliseconds on a 10x10 maze.
- **DFS** can take longer and use more memory due to unnecessary exploration.
- **BFS** is consistent but explores more nodes than needed.
- **A\*** reaches the goal efficiently by prioritizing promising paths using a heuristic (Manhattan distance).

---

### 🎯 7.3 Path Quality

- **BFS and A\*** always return the shortest path (if it exists).
- **DFS** may return a valid but longer path and doesn't guarantee optimality.

---

### 💡 7.4 Takeaway

In unweighted grids like ours:
- **BFS and A\*** perform similarly in terms of path length.
- But **A\*** has an advantage when mazes become larger or weighted.
- **DFS** helps visualize deep exploration but isn't reliable for optimal pathfinding.

## 8. A* Search Algorithm

The **A\*** algorithm (pronounced “A-star”) is one of the most powerful and widely used pathfinding techniques in artificial intelligence. It combines the strengths of both **Dijkstra's Algorithm** (which considers actual cost) and **Greedy Best-First Search** (which uses a heuristic) to find the shortest possible path in an efficient manner.

---

### 🔍 8.1 How It Works ###

A\* evaluates each possible path using the formula:

> **f(n) = g(n) + h(n)**

- **g(n)** → Actual cost from start node to current node  
- **h(n)** → Estimated cost from current node to goal node (heuristic)

In our project, we used **Manhattan Distance** as the heuristic:

```python
abs(current_x - goal_x) + abs(current_y - goal_y)
```
This heuristic is admissible (never overestimates), ensuring A* finds the shortest path when one exists.

### 🧪 8.2 Implementation Details ###
A priority queue (min-heap) is used to always select the node with the lowest f(n).

Each step considers 4 directions (up, down, left, right).

We track visited nodes to avoid cycles or redundant exploration.

Each valid move in our grid has an equal cost (g(n) += 1).

### 🛠️ 8.3 Performance in Our Maze ### 
A* found the same optimal path as BFS (21 steps).

This behavior is expected in unweighted grids where all movements have equal cost.

Despite the same result, A* uses heuristic-driven decisions, making it more scalable and efficient in larger or complex environments.

### 🎬 8.4 Animated Visualization ### 
We animated the A* agent as a bright blue dot navigating through the maze, leaving a glowing blue trail behind it. This visual clearly shows:

The intelligent, directed movement of the agent

The shortest path from start to goal

The algorithm's optimal behavior in real-time

### 💡 8.5 Why A* Matters ### 
A* is widely used in:

🕹️ Game AI (enemy movement, path planning)

🗺️ GPS Navigation systems

🤖 Robotics and real-time decision-making

It offers the perfect balance of accuracy and efficiency, especially when:

Environments are large or complex

Terrain costs (weights) vary

Optimal pathfinding is essential

In our project, A* validates its reliability and intelligence by consistently delivering the shortest path — backed by mathematical guarantees and practical speed.






