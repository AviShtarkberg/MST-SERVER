
# Concurrent MST Computation Server

A multithreaded network server application that allows clients to compute Minimum Spanning Trees (MST) using Kruskal's or Prim's algorithms. The server supports multiple clients simultaneously and provides various graph operations.

## Overview

The Concurrent MST Computation Server is designed to handle multiple client connections simultaneously. Clients can choose between Kruskal's or Prim's algorithm for MST computation and perform various graph operations such as adding or removing edges, computing the MST weight, finding the longest distance between two vertices, and more.

## Features

- **Concurrent Client Handling**: Supports multiple clients simultaneously using a thread pool.
- **Active Object Pattern**: Implements the Active Object design pattern for asynchronous method execution.
- **Singleton Graph Instance**: Manages the graph using a thread-safe singleton pattern.
- **MST Computation**: Allows clients to compute MSTs using Kruskal's or Prim's algorithms.
- **Graph Operations**: Supports adding/removing edges, creating new graphs, and querying graph properties.
- **Signal Handling**: Graceful shutdown on `SIGINT` or `SIGTERM`.

## Usage

### Running the Server

By default, the server listens on port `9034`. You can run the server using:

```bash
./server
```

### Client Interaction

Clients can connect to the server using `telnet`:

```bash
telnet localhost 9034
```

#### Client Commands

1. **Select MST Algorithm**: Upon connection, the server prompts:

    ```
    Do you prefer to use Kruskal or Prim for MST computation?
    ```

    - **Input**: `Kruskal` or `Prim`

2. **Create a New Graph**:

    - **Prompt**:

        ```
        Please write the amount of vertices and edges that you want in the graph (format: vertices edges):
        ```

    - **Input**: Two integers representing the number of vertices and edges (e.g., `5 7`).

    - **Enter Edges**:

        For each edge, the server prompts:

        ```
        Enter the edges (format: u v weight):
        ```

        - **Input**: Three integers per edge (e.g., `1 2 10`).

3. **Operations Menu**:

    After the graph is ready, the server presents a menu:

    ```
    Please choose an operation:
    1. Total weight of the MST
    2. Longest distance between two vertices
    3. Average distance between any two vertices in the MST
    4. Shortest distance between two vertices
    5. Add edge
    6. Remove edge
    7. New graph
    Enter the number of the operation:
    ```

    - **Operation Details**:

        - **1**: Computes the total weight of the current MST.
        - **2**: Finds the longest distance between any two vertices in the MST.
        - **3**: Calculates the average distance between all pairs of vertices in the MST.
        - **4**: Finds the shortest distance between two specified vertices.
            - **Prompt**: `Enter two vertices Xi and Xj:`
            - **Input**: Two integers representing vertex indices.
        - **5**: Adds a new edge to the graph.
            - **Prompt**: `Enter the edge to add (format: u v weight):`
            - **Input**: Three integers.
        - **6**: Removes an edge from the graph.
            - **Prompt**: `Enter the edge to remove (format: u v):`
            - **Input**: Two integers.
        - **7**: Creates a new graph (resets the current graph).

## Configuration

- **Port Number**: Change the `PORT` definition in `main.cpp` to use a different port.

    ```cpp
    #define PORT 9034
    ```

- **Thread Pool Size**: Adjust the number of threads in the thread pool by changing the parameter in `main()`:

    ```cpp
    ThreadPool threadPool(4); // Change '4' to the desired number of threads
    ```

## Project Structure

- **ActiveObject**: Implements asynchronous method execution using a separate thread.
- **Graph**: Manages graph data structures and provides thread-safe operations.
- **IMSTSolver**: Interface for MST solver classes.
- **KruskalMST**: Implements Kruskal's algorithm.
- **PrimMST**: Implements Prim's algorithm.
- **MSTFactory**: Factory pattern to create MST solver instances.
- **ThreadPool**: Manages a pool of worker threads for handling client connections.
- **main.cpp**: Entry point of the server application.
