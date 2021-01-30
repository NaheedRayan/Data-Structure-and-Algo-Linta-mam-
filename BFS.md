# BFS - Breadth First Search


This is a cpp code 

```cpp
#include <bits/stdc++.h>

using namespace std ;

vector <int> v[10] ;   //Vector for maintaining adjacency list explained above
int level[10];         //To determine the level of each node
bool vis[10];          //Mark the node if visited 

void bfs(int s) 
{
    queue <int> q;
    q.push(s);
    
	level[ s ] = 0 ;  //Setting the level of the source node as 0
    vis[ s ] = true;
    while(!q.empty())
    {
        int p = q.front();
        q.pop();

        for(int i = 0 ; i < v[p].size() ; i++)
        {
            if(vis[ v[p][i] ] == false)
            {
                //incrementing the level
                level[ v[p][i] ] = level[ p ]+1;                 
                q.push(v[p][i]);
                vis[ v[p][i] ] = true;
    		}
        }
    }
}

```

Now an implementation in java is given
Source GFG : https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/


```java
// Java program to print BFS traversal from a given source vertex.
// BFS(int s) traverses vertices reachable from s.
import java.io.*;
import java.util.*;

// This class represents a directed graph using adjacency list
// representation
class Graph
{
	private int V; // No. of vertices
	private LinkedList<Integer> adj[]; //Adjacency Lists

	// Constructor
	Graph(int v)
	{
		V = v;
		adj = new LinkedList[v];
		for (int i=0; i<v; ++i)
			adj[i] = new LinkedList();
	}

	// Function to add an edge into the graph
	void addEdge(int v,int w)
	{
		adj[v].add(w);
	}

	// prints BFS traversal from a given source s
	void BFS(int s)
	{
		// Mark all the vertices as not visited(By default
		// set as false)
		boolean visited[] = new boolean[V];

		// Create a queue for BFS
		LinkedList<Integer> queue = new LinkedList<Integer>();

		// Mark the current node as visited and enqueue it
		visited[s]=true;
		queue.add(s);

		while (queue.size() != 0)
		{
			// Dequeue a vertex from queue and print it
			s = queue.poll();
			System.out.print(s+" ");

			// Get all adjacent vertices of the dequeued vertex s
			// If a adjacent has not been visited, then mark it
			// visited and enqueue it
			Iterator<Integer> i = adj[s].listIterator();
			while (i.hasNext())
			{
				int n = i.next();
				if (!visited[n])
				{
					visited[n] = true;
					queue.add(n);
				}
			}
		}
	}

	// Driver method to
	public static void main(String args[])
	{
		Graph g = new Graph(4);

		g.addEdge(0, 1);
		g.addEdge(0, 2);
		g.addEdge(1, 2);
		g.addEdge(2, 0);
		g.addEdge(2, 3);
		g.addEdge(3, 3);

		System.out.println("Following is Breadth First Traversal "+
						"(starting from vertex 2)");

		g.BFS(2);
	}
}
// This code is contributed by Aakash Hasija

```

Output:
```cmd
Following is Breadth First Traversal (starting from vertex 2)
2 0 3 1
```


# <center>The end</center>
