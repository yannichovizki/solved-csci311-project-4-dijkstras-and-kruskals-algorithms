Download Link: https://assignmentchef.com/product/solved-csci311-project-4-dijkstras-and-kruskals-algorithms
<br>



In this project you will implement the Dijkstra’s algorithm and the Kruskal’s algorithm.

Download Project5.tar and untar it: tar -xvf Project5.tar

Use code for Project 4 and for Project 3. You will need to use classes <em>Item, TimeStamp</em>, <em>Ugraph, </em>and <em>PriorityQueue.</em>

<strong>Step 1. </strong>Update code for <strong><em>PriorityQueue</em></strong> class:

<ol>

 <li>In function <strong><em>pop()</em></strong>, before removing min-Priority Item, set it’s keys[aheap[0].key] = -1. In this case if keys[v] is -1, then we will know that vertex v is not in the priority queue anymore.</li>

 <li>Write the member function <strong><em>bool isKey(int v) </em></strong>that returns <em>true</em> if v is in the priority queue (i.e. if keys[v] is not -1), and returns <em>false</em></li>

</ol>




<strong>Step 2.</strong> Update struct <strong><em>edge</em>: </strong>




<table width="0">

 <tbody>

  <tr>

   <td width="568">struct edge{int source;//edge is from this node to neighbor      int neighbor; // adjacent node    int w; //keeps auxiliary informationedge(){               source = 0;          neighbor = 0;                w = 0;};edge(int i, int j){                source = 0;//dummy valueneighbor = i;                w = j;};edge(int from, int to, int aweight){             source = from;//edge is from this node          neighbor = to;//edge is to this nodew = aweight;//weight of this edge};//overloaded *less than* operator will allow to compare edges         bool operator&lt;(edge y){ return (this-&gt;w &lt; y.w) ? true : false; }; }; </td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<strong>                 </strong>

<strong>Step 3. </strong>Update code for <strong><em>Ugraph</em></strong> class:







<ol>

 <li>Write overloaded member function <strong><em>void addEdge(int u, int v, int aweight)</em></strong> that takes three parameters, integers u, v and weight, and adds an edge (u, v) in Adj[u] whose weight <strong><em>w </em></strong>is set to the third parameter <em>aweight; </em>and adds an edge (v, u) in Adj[v] with <strong><em>w </em></strong>set to</li>

 <li>Write a new member function <strong><em>void dijkstra(int s)</em></strong> that takes an integer <em>s </em>as a parameter and finds all shortest paths from <em>s </em>to all vertices (nodes) of the graph.

  <ol>

   <li>Use the vectors <em>parents </em>and <em>distance </em>to store the results (these vectors already exist in <em>Ugraph</em>). Inside this function, first, for all vertices v, initialize parent[v] to v and distance[v] to INT_MAX.</li>

   <li>Then set distance of <em>s </em>to 0.</li>

   <li>Then instantiate an object of PriorityQueue class using the constructor that takes a pointer to an array of Items and it’s length. You need to create an array in the Heap (using <strong><em>new</em></strong>) of Items, such that each Item has each vertex v as it’s key and has distance[v] as it’s priority. The size of this array is equal to the total number of vertices in the graph (use <strong><em>size </em></strong>of Ugraph). Simply scan array <em>distance </em>from left to right and for each i, initialize array at i to Item(i, distance[i]). Then you will pass this array to the constructor of PriorityQueue.</li>

   <li>Then continue writing the code of the Dijkstra’s algorithm. To check if a vertex v is in the priority queue, use the member function <strong><em>isKey(v) </em></strong>of PriorityQueue.</li>

   <li>When updating priority of a node v with smaller distance, update distance[v] too.</li>

  </ol></li>

 <li>Write a new member function <strong><em>void printDistance() </em></strong>that prints distance of each node v, and put a space after each node and <em>endl </em>at the end.</li>

 <li>Write a new member function <strong><em>void printParents() </em></strong>that prints parent of each node v, and put a space after each node and <em>endl </em>at the end.</li>

 <li>Write a new recursive member function <strong><em>void printPath(int u, int v) </em></strong>that prints path by backtracking <em>parents </em>array starting with the second parameter <em>v </em>until the first parameter <em>u </em>is found on the path. Path is printed in the format: &lt;vertex&gt;&lt;space&gt;…&lt;vertex&gt;&lt;space&gt;. The first vertex on the path is <em>u </em>and the last is (Note: there is NO <em>endl</em> at the end of output).</li>

 <li>Write a new member function <strong><em>int</em></strong> <strong>lenghtShortestW(int u, int v) </strong>that finds the shortest path from <em>u </em>to <em>v </em>using the Dijkstra’s algorithm, then prints this path and returns the length of the path:

  <ol>

   <li>Inside this function, call <em>dikstra(u) </em>that will find the shortest paths from u to all vertices;</li>

   <li>Then call <em>printPath(u, v) </em>that will print path from u to v using <em>parents </em>vector; since <em>printPath </em>does not print <em>endl, </em>print <strong><em>endl </em></strong>after calling</li>

   <li>Finally, return the length of the shortest path stored at <em>distance[v]. </em></li>

  </ol></li>

 <li>Add a new private data member to <em>Ugraph </em>that holds the minimum spanning tree of the graph. Add <strong><em>vector&lt;vector&lt; edge &gt; &gt; mst. </em></strong>Inside the constructor, resize <strong><em>mst </em></strong>to</li>

 <li>Write a new member function <strong><em>void kruskal()</em></strong> that will calculate the minimum spanning tree for the graph (and will store it in the data member <strong><em>mst</em></strong>).

  <ol>

   <li>Use <strong><em>parents</em></strong> vector to store parents (representatives of connected components) of the vertices and use <strong><em>distance </em></strong>vector to store ranks of the vertices.</li>

   <li>Check if <strong><em>mst </em></strong>is not empty (size is greater than 0), clear it and resize to 0: mst.clear(), and mst.resize(0).</li>

   <li>Write a new recursive member function <strong><em>int findSet(int v) </em></strong>that returns the representative of <em>v</em>’s connected component and sets parents of all the vertices on the path from v to the root (representative) of the connected component to the root.</li>

   <li>Write a new member function <strong><em>void combine(int x, int y) </em></strong>that uses rank-by-union heuristic to combine two connected components whose representatives are x and y.</li>

   <li>First, inside <strong><em>kruskal()</em></strong>, initialize parents[v] = v and distance[v] = 0 (rank of each node is zero).</li>

   <li>Run <strong><em>while</em></strong> (or <strong><em>for</em></strong>) loop until (size – 1) edges have been added to MST. Continue implementing the Kruskal’s algorithm according to pseudocode in lecture slides. When adding an edge (u, v, w) (from u to v with weight w) to the minimum spanning tree, you need to add this edge to mst[u] and mst[v] (since mst is an undirected graph, an edge appears in the adjacency lists of mst twice).</li>

   <li><strong><em>To sort edges</em></strong>:

    <ol>

     <li>Comment out “bool operator&gt;….” line in struct “edge”.</li>

    </ol></li>

  </ol></li>

</ol>

<em> </em>

<ol>

 <li>Put this function (not a member function) into ugraph.cpp</li>

</ol>

bool lessThan(const edge &amp;x, const edge &amp;y){ return (x.w &lt; y.w) ? true : false; }

<em> </em>

<em> </em>

<ul>

 <li>Put all the edges into a temporary vector (declared inside <em>kruskal </em>function) of edges, vector&lt;edge&gt; <strong><em>edgesAll</em></strong>. You will need to scan <em>Adj</em> to do this. <strong>Note</strong> that each edge (u, v) occurs in <em>Adj </em>twice: once in Adj[u] and the other time in Adj[v]; so when you consider an edge (u, v), check if u &lt; v, then put this edge into <em>edgesAll, </em>and do not put edge if u &gt; v; in this case you will put the same edge only once. Use the edge’s constructor that takes three parameters: edge(u, v, weight).</li>

</ul>

<em> </em>

<ol>

 <li>After this, you may use <strong><em>sort </em></strong>of the standard library (include &lt;algorithm&gt;):</li>

</ol>

<em>sort(edgesAll.begin(), edgesAll.end(), <strong>lessThan</strong>); </em>

<em> </em>

<ol start="9">

 <li>Write a new member function <strong><em>void printMST() </em></strong>that scans <strong><em>mst </em></strong>and prints out all vertices in mst[0], then all vertices in mst[1], and so on. Format of output: print a space after each vertex and print <strong><em>endl </em></strong>after each adjacency list of mst (e.g. print <em>endl</em> after all vertices of mst[0] have been printed, and so on).</li>

</ol>

<em> </em>

<strong><em>Example: </em></strong><em>mst of the given graph in Figure to the left is shown in blue, and this mst will be printed like this:</em>

<strong>4 </strong>

3

3

1 4 2

<strong>Explanation: </strong>each line corresponds to adjacency list of mst[i]. The

last line corresponds to vertices at mst[3] (4 comes before 2, because edge (3,4) has less weight than edge (2, 3), so it will be pushed back to mst[3] before the edge (2, 3) ).

<em> </em>

<em> </em>

<ol start="10">

 <li>Write a new member function <strong><em>int weightMST() </em></strong>that scans <strong><em>mst </em></strong>and returns total weight of all the edges in the minimum spanning tree. Please note that each edge is repeated twice in MST, so to return the correct number, you may add up all the weights, and then divide the sum by 2.</li>

</ol>


