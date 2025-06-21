# TDWRPP-Instances
Instances created and solved for the Time-Dependent Windy Rural Postman Problem. 

You can find the best-known solutions for these instances in the [Best-known solutions file](Instances-bks.txt).
---

# Instance Data Format Description

This document describes the file format for the problem instances provided in this repository. Each instance is contained in a single `.txt` file and represents a directed graph with time-dependent arc costs.

The file is structured into several sections. Lines beginning with a hash symbol (`#`) are either comments or headers for a subsequent block of data.

---

## File Structure

An instance file is organized into the following sections:

1.  **Header Information**: Provides general parameters of the graph.
2.  **Arcs and Travel Times**: Defines all arcs in the graph and their associated travel times across different time intervals.
3.  **Required Edges**: Lists the specific arcs that must be traversed in a valid solution.
4.  **Time Intervals**: Defines the time boundaries for the travel time costs.

### 1. Header Information

The file begins with several key-value pairs that define the overall size and properties of the instance.

*   `# Nodes`
    The integer on the next line specifies the total number of nodes (vertices) in the graph. Nodes are typically 1-indexed.
    ```
    # Nodes
    64
    ```

*   `# Arcs`
    The integer on the next line specifies the total number of arcs (directed edges) in the graph.
    ```
    # Arcs
    232
    ```

*   `# Required Edges`
    The integer on the next line specifies the number of arcs that are designated as "required". These arcs must be included in any feasible solution. Note: Although termed "Edges", these are directed arcs.
    ```
    # Required Edges
    44
    ```

*   `# Num Intervals`
    The integer on the next line specifies the number of discrete time intervals for which travel times are defined.
    ```
    # Num Intervals
    5
    ```

### 2. Arcs and Travel Times

This section is preceded by the header `# Arcs and travel times`. It lists all the arcs in the graph. Each line has the following format:

`u v t_1 t_2 ... t_N`

-   `u`: The origin node (tail) of the arc.
-   `v`: The destination node (head) of the arc.
-   `t_1 t_2 ... t_N`: A sequence of `N` integers, where `N` is the value from `# Num Intervals`. Each `t_i` represents the travel time (or cost) of traversing the arc `(u, v)` during the `i`-th time interval.

**Example:**
```
# Arcs and travel times
1	2	688	873	803	889	822
2	1	710	953	852	862	748
```
In this example, the arc from node `1` to node `2` has a travel time of `688` in the first time interval, `873` in the second, and so on.

### 3. Required Edges

This section is preceded by the header `# Required Edges`. It provides a simple list of the arcs that must be traversed. Each line specifies one required arc.

The format of each line is:
`u v`

-   `u`: The origin node of the required arc.
-   `v`: The destination node of the required arc.

The number of lines in this section must match the value specified in the `# Required Edges` header.

**Example:**
```
# Required Edges
1	2
3	4
5	6
...
```

### 4. Time Intervals

This final section is typically preceded by the header `Time Intervals` (which may not have a `#`). It contains a list of `N` integers, where `N` is the value from `# Num Intervals`.

These integers `T_1, T_2, ..., T_N` define the end-points of the time intervals. Assuming time starts at 0, the intervals are defined as follows:

-   **Interval 1:** `[0, T_1]`
-   **Interval 2:** `(T_1, T_2]`
-   **Interval i:** `(T_{i-1}, T_i]`

**Example:**
```
Time Intervals
10800
21600
32400
43200
54000
```
Based on this example:
- The 1st travel time applies if a vehicle starts traversing an arc in the time window `[0, 10800]`.
- The 2nd travel time applies if it starts in `(10800, 21600]`.
- ... and so on.
