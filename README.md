
    import java.util.*;
    import java.lang.*;
    import java.io.*;

    class Graph
    {

        class Edge {
            int source, sink, cost;
            Edge() {
                source = sink = cost = 0;
            }
        };

        int V, E;
        Edge edge[];


        Graph(int v, int e)
        {
            V = v;
            E = e;
            edge = new Edge[e];
            for (int i=0; i<e; ++i)
                edge[i] = new Edge();
        }


        void BellmanFord(Graph graph,int source)
        {
            int V = graph.V, E = graph.E;
            int dist[] = new int[V];

            // Step 1: Initialize distances from source to all other
            // vertices as INFINITE
            for (int i=0; i<V; ++i)
                dist[i] = Integer.MAX_VALUE;
            dist[source] = 0;

            // Step 2: Relax all edges |V| - 1 times. A simple
            // shortest path from source to any other vertex can
            // have at-most |V| - 1 edges
            for (int i=1; i<V; ++i)
            {
                for (int j=0; j<E; ++j)
                {
                    int u = graph.edge[j].source;
                    int v = graph.edge[j].sink;
                    int cost = graph.edge[j].cost;
                    if (dist[u]!=Integer.MAX_VALUE &&
                        dist[u]+cost<dist[v])
                        dist[v]=dist[u]+cost;
                }
            }


            for (int j=0; j<E; ++j)
            {
                int u = graph.edge[j].source;
                int v = graph.edge[j].sink;
                int cost = graph.edge[j].cost;
                if (dist[u]!=Integer.MAX_VALUE &&
                    dist[u]+cost<dist[v])
                  System.out.println("Graph contains negative cost cycle");
            }
            printArr(dist, V);
        }


        void printArr(int dist[], int V)
        {
            System.out.println("Vertex   Distance from Source");
            for (int i=0; i<V; ++i)
                System.out.println(i+"  "+dist[i]);
        }


        public static void main(String[] args)
        {
            int V=4;  // Number of vertices in graph
            int E=8;  // Number of edges in graph

            Graph graph = new Graph(V, E);


            graph.edge[0].source = 0;
            graph.edge[0].sink = 3;
            graph.edge[0].cost = 8;


            graph.edge[1].source = 0;
            graph.edge[1].sink = 1;
            graph.edge[1].cost = 4;


            graph.edge[2].source = 1;
            graph.edge[2].sink = 2;
            graph.edge[2].cost = 5;


            graph.edge[3].source = 0;
            graph.edge[3].sink = 2;
            graph.edge[3].cost = -3;

            graph.edge[4].source = 2;
            graph.edge[4].sink = 4;
            graph.edge[4].cost = 4;


            graph.edge[5].source = 3;
            graph.edge[5].sink = 4;
            graph.edge[5].cost = 2;

            graph.edge[6].source = 4;
            graph.edge[6].sink = 3;
            graph.edge[6].cost = 1;

            graph.edge[7].source = 4;
            graph.edge[7].sink = 1;
            graph.edge[7].cost = -3;

            graph.BellmanFord(graph, 0);
        }
    }
