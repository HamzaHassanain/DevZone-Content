# Introduction to Graphs

- [What is a Graph?](#what-is-a-graph)
- [Graph Representation](#graph-representation)
- [Graph Traversal](#graph-traversal)
  - [Depth First Search (DFS)](#depth-first-search-dfs)
  - [Breadth First Search (BFS)](#breadth-first-search-bfs)
- [Unweighted Shortest Path](#unweighted-shortest-path)
- [Topological Sort](#topological-sort)
- [Exercises](#exercises)

## What is a Graph?

A graph is a data structure that consists of a set of vertices and a set of edges that connect the vertices. A graph can be directed or undirected. In a directed graph, the edges have a direction, while in an undirected graph, the edges do not have a direction.

- **Vertex (Node)**: A vertex is a point in the graph.
- **Edge**: An edge is a line connecting two vertices.
- **Directed Graph**: A graph in which the edges have a direction.
- **Undirected Graph**: A graph in which the edges do not have a direction.
- **Weighted Graph**: A graph in which the edges have weights.
- **Unweighted Graph**: A graph in which the edges do not have weights.
- **Cycle**: A cycle is a path in the graph that starts and ends at the same vertex.
- **Connected Graph**: A graph in which there is a path between every pair of vertices.
- **Disconnected Graph**: A graph in which there is no path between some pairs of vertices.
- **Tree**: A connected acyclic graph.
- **Forest**: A collection of trees.
- **Degree**: The degree of a vertex is the number of edges incident to the vertex.
- **In-degree**: The in-degree of a vertex is the number of edges coming into the vertex.
- **Out-degree**: The out-degree of a vertex is the number of edges going out of the vertex.
- **Path**: A path is a sequence of vertices in which each vertex is connected to the next vertex by an edge.
- **Shortest Path**: The shortest path between two vertices is the path with the minimum number of edges.
- **Connected Component**: A connected component is a subgraph in which there is a path between every pair of vertices.
- **Strongly Connected Component**: A strongly connected component is a subgraph in which there is a path between every pair of vertices in both directions.
- **Topological Sort**: A topological sort of a directed acyclic graph is a linear ordering of its vertices such that for every directed edge `u -> v`, vertex `u` comes before vertex `v` in the ordering.
- **DAG**: A directed acyclic graph is a directed graph with no cycles.

## Graph Representation

There are two common ways to represent a graph: adjacency matrix and adjacency list.

### Adjacency Matrix

An adjacency matrix is a 2D array of size `V x V` where `V` is the number of vertices in the graph. If the value of `adj[i][j]` is 1, then there is an edge from vertex `i` to vertex `j`, otherwise there is no edge.

```cpp

int V, E;

cin >> V >> E;

vector<vector<int>> adj(V, vector<int>(V, 0));

for (int i = 0; i < E; i++)
{
    int u, v;
    cin >> u >> v;
    adj[u][v] = 1;
    adj[v][u] = 1; // Uncomment this line for undirected graph
}

```

### Adjacency List

An adjacency list is a collection of linked lists.Each list represents a vertex in the graph.The list contains the neighbors of the vertex.

```cpp

int V, E;

cin >> V >> E;

vector<vector<int>> adj(V);

for (int i = 0; i < E; i++)
{
    int u, v;
    cin >> u >> v;
    adj[u].push_back(v);
    adj[v].push_back(u); // Uncomment this line for undirected graph
}

```

## Graph Traversal

Graph traversal is the process of visiting all the vertices in a graph.There are two common graph traversal algorithms : Depth First Search(DFS) and Breadth First Search(BFS).

### Depth First Search(DFS)

Depth First Search(DFS)
is a graph traversal algorithm that explores as far as possible along each branch before backtracking.

```cpp

void dfs(int u, vector<vector<int>> &adj, vector<bool> &visited)
{
    visited[u] = true;
    cout << u << " ";
    for (int v : adj[u])
    {
        if (!visited[v])
        {
            dfs(v, adj, visited);
        }
    }
}

int main()
{

    int V, E;

    cin >> V >> E;

    vector<vector<int>> adj(V);

    for (int i = 0; i < E; i++)
    {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u); // Uncomment this line for undirected graph
    }

    vector<bool> visited(V, false);

    dfs(0, adj, visited);
}

```

### Breadth First Search(BFS)

Breadth First Search(BFS)
is a graph traversal algorithm that explores the neighbor vertices before moving to the next level of neighbors.

```cpp

void bfs(int u, vector<vector<int>> &adj, vector<bool> &visited)
{
    queue<int> q;
    q.push(u);
    visited[u] = true;
    while (!q.empty())
    {
        int v = q.front();
        q.pop();
        cout << v << " ";
        for (int w : adj[v])
        {
            if (!visited[w])
            {
                q.push(w);
                visited[w] = true;
            }
        }
    }
}

int main()
{

    int V, E;

    cin >> V >> E;

    vector<vector<int>> adj(V);

    for (int i = 0; i < E; i++)
    {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u); // Uncomment this line for undirected graph
    }

    vector<bool> visited(V, false);

    bfs(0, adj, visited);
}
```

## Unweighted Shortest Path

Unweighted Shortest Path is the shortest path between two vertices in a graph with unweighted edges.Breadth First
Search(BFS)

can be used to find the shortest path in an unweighted graph.

```cpp

int  bfs(int u, int v, vector<vector<int>> &adj)
{
    queue<pair<int, int>> q;
    q.push({u, 0});
    vector<bool> visited(adj.size(), false);
    visited[u] = true;
    while (!q.empty())
    {
        int node = q.front().first;
        int dist = q.front().second;
        q.pop();
        if (node == v)
        {
            return dist;
        }
        for (int neighbor : adj[node])
        {
            if (!visited[neighbor])
            {
                q.push({neighbor, dist + 1});
                visited[neighbor] = true;
            }
        }
    }
    return -1;
}

int main()
{

    int V, E;

    cin >> V >> E;

    vector<vector<int>> adj(V);

    for (int i = 0; i < E; i++)
    {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u); // Uncomment this line for undirected graph
    }

    int u, v;
    cin >> u >> v;

    cout << bfs(u, v, adj);
}
```

## Topological Sort

Topological Sort is a linear ordering of the vertices of a directed acyclic
graph(DAG) such that for every directed edge `u -> v`, vertex `u` comes before vertex `v` in the ordering. Topological Sort can be done using Depth First Search (DFS).

```cpp

void dfs(int u, vector<vector<int>>& adj, vector<bool>& visited, stack<int>& s)
{
    visited[u] = true;
    for (int v : adj[u])
    {
        if (!visited[v])
        {
            dfs(v, adj, visited, s);
        }
    }
    s.push(u);
}

void topological_sort(vector<vector<int>> &adj)
{
    int V = adj.size();
    vector<bool> visited(V, false);
    stack<int> s;
    for (int i = 0; i < V; i++)
    {
        if (!visited[i])
        {
            dfs(i, adj, visited, s);
        }
    }
    while (!s.empty())
    {
        cout << s.top() << " ";
        s.pop();
    }
}
```

## Problems

- [Flood Fill](https://leetcode.com/problems/flood-fill/description/)
- [Number of Islands](https://leetcode.com/problems/number-of-islands/description/)
- [Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/)
- [Find the Town Judge](https://leetcode.com/problems/find-the-town-judge/)
- [Course Schedule](https://leetcode.com/problems/course-schedule/)
