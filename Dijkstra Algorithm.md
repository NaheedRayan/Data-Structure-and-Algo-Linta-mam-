# Dijkstra Algorithm

This is a cpp code

```cpp
Read the book for theory
below a sample code is given


#include <iostream>
#include <bits/stdc++.h>
#define PII pair<int , int> 

using namespace std ;

vector<PII>adj[10005] ;
bool vis[10005] ;
int dis[10005]  , n , m ;


void dijkstra(int x)
{
    //for min heap .It will take the smallest weight first
    priority_queue <PII ,vector <PII> ,greater<PII>> q ;


    //here INT_MAX can also be set
    //for this the minimum value will begiven priority
    for(int i = 0 ; i <= n ;i++)dis[i]=200001;  


    dis[x] = 0;       //setting the initial distance to zero
    q.push({0,x});    //saving the weight in the first position because of the priority_queue
    while (!q.empty()) 
    {
        int a = q.top().second; 
        q.pop();

        if (vis[a]) continue;
            vis[a] = true;
        for (auto u : adj[a]) 
        {
            int b = u.second, w = u.first;
            
            if (dis[a] + w < dis[b]) 
            {
            	dis[b] = dis[a] + w ;
            	q.push({dis[b],b});
            }
        }
    }
}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    cin >> n >> m ;			// n = nodes , m = edges
    for(int i = 0 ; i < m ; i++)
    {
        int u , v, w ;
        cin >> u >> v >> w ;
        adj[u].push_back({w , v}) ;     //pushing the weight at the left inorder to be sorted
        adj[v].push_back({w , u}) ;

    }
    dijkstra(1) ;			//distance from source node ie. 1
        
    if(dis[n]==200001)cout << "Impossible" << endl; //if the node is not visited or connected
    else cout << dis[n] << endl;
    return 0 ;
}
```

<br>
Below is an example of java code:

```java
// Java implementation of Dijkstra's Algorithm 
// using Priority Queue 
import java.util.*; 
public class DPQ { 
	private int dist[]; 
	private Set<Integer> settled; 
	private PriorityQueue<Node> pq; 
	private int V; // Number of vertices 

	List<List<Node> > adj; 

	public DPQ(int V) 
	{ 
		this.V = V; 
		dist = new int[V]; 
		settled = new HashSet<Integer>(); 
		pq = new PriorityQueue<Node>(V, new Node()); 
	} 

	// Function for Dijkstra's Algorithm 
	public void dijkstra(List<List<Node> > adj, int src) 
	{ 
		this.adj = adj; 

		for (int i = 0; i < V; i++) 
			dist[i] = Integer.MAX_VALUE; 

		// Add source node to the priority queue 
		pq.add(new Node(src, 0)); 

		// Distance to the source is 0 
		dist[src] = 0; 
		while (settled.size() != V) { 

			// remove the minimum distance node 
			// from the priority queue 
			int u = pq.remove().node; 

			// adding the node whose distance is 
			// finalized 
			settled.add(u); 

			e_Neighbours(u); 
		} 
	} 

	// Function to process all the neighbours 
	// of the passed node 
	private void e_Neighbours(int u) 
	{ 
		int edgeDistance = -1; 
		int newDistance = -1; 

		// All the neighbors of v 
		for (int i = 0; i < adj.get(u).size(); i++) { 
			Node v = adj.get(u).get(i); 

			// If current node hasn't already been processed 
			if (!settled.contains(v.node)) { 
				edgeDistance = v.cost; 
				newDistance = dist[u] + edgeDistance; 

				// If new distance is cheaper in cost 
				if (newDistance < dist[v.node]) 
					dist[v.node] = newDistance; 

				// Add the current node to the queue 
				pq.add(new Node(v.node, dist[v.node])); 
			} 
		} 
	} 

	// Driver code 
	public static void main(String arg[]) 
	{ 
		int V = 5; 
		int source = 0; 

		// Adjacency list representation of the 
		// connected edges 
		List<List<Node> > adj = new ArrayList<List<Node> >(); 

		// Initialize list for every node 
		for (int i = 0; i < V; i++) { 
			List<Node> item = new ArrayList<Node>(); 
			adj.add(item); 
		} 

		// Inputs for the DPQ graph 
		adj.get(0).add(new Node(1, 9)); 
		adj.get(0).add(new Node(2, 6)); 
		adj.get(0).add(new Node(3, 5)); 
		adj.get(0).add(new Node(4, 3)); 

		adj.get(2).add(new Node(1, 2)); 
		adj.get(2).add(new Node(3, 4)); 

		// Calculate the single source shortest path 
		DPQ dpq = new DPQ(V); 
		dpq.dijkstra(adj, source); 

		// Print the shortest path to all the nodes 
		// from the source node 
		System.out.println("The shorted path from node :"); 
		for (int i = 0; i < dpq.dist.length; i++) 
			System.out.println(source + " to " + i + " is "
							+ dpq.dist[i]); 
	} 
} 

// Class to represent a node in the graph 
class Node implements Comparator<Node> { 
	public int node; 
	public int cost; 

	public Node() 
	{ 
	} 

	public Node(int node, int cost) 
	{ 
		this.node = node; 
		this.cost = cost; 
	} 

	@Override
	public int compare(Node node1, Node node2) 
	{ 
		if (node1.cost < node2.cost) 
			return -1; 
		if (node1.cost > node2.cost) 
			return 1; 
		return 0; 
	} 
} 
```

>Time Complexity of Dijkstra's Algorithm is O ( V 2 ) but with min-priority queue it drops down to O ( V + E l o g V )
