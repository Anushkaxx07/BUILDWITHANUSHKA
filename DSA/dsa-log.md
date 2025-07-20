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


