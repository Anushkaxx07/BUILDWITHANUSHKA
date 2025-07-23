📚 **Reference:** [Kruskal's Algorithm Explained – YouTube](https://www.youtube.com/watch?v=KxLtIrCyXwE)

---

### 🗓️ July 20, 2025

* ✅ Today, I studied **Kruskal’s Algorithm** for finding the Minimum Spanning Tree (MST) using **Disjoint Set Union (DSU)** with both **union by rank** and **union by size** optimizations.

---

#### 🔹 What is Kruskal’s Algorithm?

* A greedy algorithm used to find the **Minimum Spanning Tree** of a graph.
* Selects the smallest weighted edges and ensures **no cycles** are formed.

---

#### 🔹 Key Steps

1. **Sort** all edges in ascending order based on weight.
2. Initialize **DSU** (Disjoint Set Union) structure.
3. Loop through the sorted edges:

   * Let `u = edge[0]`, `v = edge[1]`, and `wt = edge[2]`.
   * Find the **ultimate parent** of `u` and `v` using the `find()` function.
   * If they belong to **different components**, include the edge in MST and perform `union()`.

---

#### 🔹 Union by Rank

* Maintains a `rank[]` array to attach the shorter tree under the taller one.
* If ranks are equal, attach one under the other and **increment the parent’s rank**.

```cpp
void unionByRank(int u, int v) {
    int pu = find(u);
    int pv = find(v);
    if (pu == pv) return;

    if (rank[pu] < rank[pv]) {
        parent[pu] = pv;
    } else if (rank[pu] > rank[pv]) {
        parent[pv] = pu;
    } else {
        parent[pv] = pu;
        rank[pu]++;
    }
}
```

---

#### 🔹 Union by Size

* Maintains a `size[]` array and always connects the **smaller set to the larger set**.
* If sizes are equal, attach one and **add sizes accordingly**.

```cpp
void unionBySize(int u, int v) {
    int pu = find(u);
    int pv = find(v);
    if (pu == pv) return;

    if (size[pu] < size[pv]) {
        parent[pu] = pv;
        size[pv] += size[pu];
    } else {
        parent[pv] = pu;
        size[pu] += size[pv];
    }
}
```

---

#### 🔹 Final Notes

* If `u` and `v` have **different parents**, they belong to different components → add edge.
* If they have **same parent**, adding the edge would form a **cycle** → **skip** it.
* The main goal of Kruskal’s: **connect all nodes with minimum weight and no cycles** ✅



---

### 🗓️ July 21, 2025

📚  **Reference:** [Tarjan's Algorithm Explained – YouTube](https://www.youtube.com/watch?v=CiDPT1xMKI0&t=908s)
                    [Question solved on - Coding Ninja](https://www.naukri.com/code360/problems/bridges-in-graph_893026?leftPanelTab=0&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar).
                    [Leetcode Que Solved which beat 94.32% in runtime](https://leetcode.com/problems/critical-connections-in-a-network/submissions/1705773875/)


* ✅ Today, I studied **Bridges in Graph** using **Tarjan’s Algorithm** via **Depth-First Search (DFS)** to identify all **critical connections** in an undirected graph.

---

#### 🔹 What is a Bridge?

* A **bridge** is an edge in a graph whose removal increases the number of connected components.
* In simple terms, a bridge **does not lie on any cycle** – it is a **critical edge**.

---

#### 🔹 Key Steps

1. Performed DFS traversal and maintained:
   - `disc[]`: Discovery time of the node
   - `low[]`: Lowest discovery time reachable from that node (even via back edges)
   - `parent[]`: To track the parent during DFS
   - `vis[]`: To mark nodes as visited
   - A global `timer`: Used to assign unique discovery times

2. For each neighbor of a node:
   - If it's the parent → skip
   - If it's already visited → it’s a back edge → update:
     ```cpp
     low[node] = min(low[node], disc[neighbour]);
     ```
   - If not visited → DFS on it, then backtrack and check:
     ```cpp
     if (low[neighbour] > disc[node]) → it's a bridge
     ```
     Then update:
     ```cpp
     low[node] = min(low[node], low[neighbour]);
     ```

---

#### 🔹 Code Snippet

```cpp
void dfs(int node, vector<vector<int>> &adj) {
    vis[node] = true;
    disc[node] = low[node] = timer++;

    for (int neighbour : adj[node]) {
        if (neighbour == parent[node]) continue;

        if (!vis[neighbour]) {
            parent[neighbour] = node;
            dfs(neighbour, adj);

            if (low[neighbour] > disc[node]) {
                // (node, neighbour) is a bridge
            }

            low[node] = min(low[node], low[neighbour]);
        } else {
            low[node] = min(low[node], disc[neighbour]); // back edge
        }
    }
}

---
### 🗓️ July 22, 2025

📚  **Reference:** [Articulation Poitn Explained – YouTube](https://www.youtube.com/watch?v=fqkqx6OBRDE&list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA&index=15)
                    [Question solved on - GFG](https://www.geeksforgeeks.org/problems/articulation-point-1/1).
                  
---

### ✅ **What I Learned Today:**

🧠 **Definition:**
An **Articulation Point** (or Cut Vertex) is a vertex in a graph such that **removing it increases the number of connected components** — in simple terms, it disconnects the graph.

🛠️ **Approach Used: Tarjan's Algorithm**

We use the following data structures:
- `disc[]`: Discovery time of each node
- `low[]`: Lowest discovery time reachable from the node
- `parent[]`: To keep track of the DFS parent
- `visited[]`: To mark visited nodes
- `set<int> ap`: To store articulation points (avoids duplicates)
- `adjacency list`: To represent the graph

We maintain a global `timer` to assign discovery times.

---

### 🔁 **DFS Steps Breakdown:**

1. Initialize:  
   - `disc[node] = low[node] = timer++`  
   - `children = 0`

2. For each adjacent node:
   - **Case 1: If already visited**
     - If it's the **parent**, skip.
     - Else, it's a **back edge** → update:
       ```cpp
       low[node] = min(low[node], disc[neighbour]);
       ```

   - **Case 2: If not visited**
     - `children++`
     - `parent[neighbour] = node`
     - `visited[neighbour] = true`
     - DFS call: `dfs(neighbour, ...)`
     - After DFS:
       ```cpp
       low[node] = min(low[node], low[neighbour]);
       ```

     - Check articulation condition (non-root):
       ```cpp
       if (parent[node] != -1 && low[neighbour] >= disc[node])
           ap.insert(node);
       ```

3. After loop (for root nodes):
   ```cpp
   if (parent[node] == -1 && children >= 2)
       ap.insert(node);
   ```

---

### 🧾 Final Step:
Convert the set to vector and return:
```cpp
vector<int> ans(ap.begin(), ap.end());
return ans;
```

---

### 📌 Summary:

> Tarjan’s algorithm efficiently finds articulation points using DFS and `low` / `disc` arrays. Root nodes have a separate condition, and a `set` ensures unique articulation points.

---

### 💡 Concept Mastered:
- Articulation Point Detection ✅  
- Back Edges in DFS ✅  
- Tarjan’s Algo Implementation ✅  

---


📚 **Reference:** [Kosaraju's Algorithm Explained – YouTube](https://www.youtube.com/watch?v=ndfjV_yHpgQ&t=169s)
                    [Question solved on - Coding Ninja which eats 99.8% in tc](https://www.naukri.com/code360/problems/count-strongly-connected-components-kosaraju-s-algorithm_1171151?leftPanelTab=0&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar&leftPanelTabValue=SUBMISSION).

---

### 🗓️ July 23, 2025

## 🔁 Kosaraju's Algorithm - Strongly Connected Components (SCC)

Today, I learned and implemented **Kosaraju’s Algorithm** to find the **Strongly Connected Components (SCCs)** in a directed graph.

### 🧠 Concept

A **Strongly Connected Component** (SCC) in a directed graph is a **maximal subset of vertices** such that **every vertex is reachable from every other vertex in the same subset**, and vice versa.

In simpler terms:
> From any node in an SCC, we can reach every other node in that SCC, and also return back to the original node.

---

### 🚀 Approach using Kosaraju's Algorithm

Kosaraju’s algorithm uses **2 DFS traversals** and works in **3 main steps**:

1. **Topological Ordering using DFS + Stack**
   - Perform a DFS traversal of the original graph and push each node into a stack **after its DFS call finishes**.
   - This stack stores nodes in **order of finishing time** (i.e., reverse topological order).

2. **Transpose the Graph**
   - Reverse the direction of all edges in the graph. This is called the **transpose** of the graph.

3. **DFS on Transposed Graph (in Stack Order)**
   - Pop nodes one by one from the stack.
   - For every unvisited node, perform DFS on the transposed graph.
   - Each such DFS call will give us **one strongly connected component**.

---

### 💡 Key Insight

> The number of DFS calls on the transposed graph (after popping from the stack) gives us the **total number of SCCs**.

---

### ✅ Time & Space Complexity

- **Time Complexity:** `O(V + E)`  
- **Space Complexity:** `O(V + E)`

Where `V` is the number of vertices and `E` is the number of edges.

---

### 📌 Summary

Kosaraju's Algorithm is a powerful and efficient method to identify SCCs in any directed graph. Its logic builds upon DFS, stack (for finish time), and graph transposition.

---

### 📂 Personal Reflection

I found the idea of **reversing the graph** and using **finish times from DFS** very intuitive once I visualized it. Implementing this helped me deeply understand how reachability works in directed graphs.

> 📚 Learning Outcome:  
> *From any node A, if I can go to B and then return from B to A — this symmetry of reachability defines a strongly connected component.*
