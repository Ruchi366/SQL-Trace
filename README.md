# SQL::TRACE — Interactive Query Engine Visualizer

An interactive, browser-based SQL query engine and execution visualizer powered by a native execution core compiled to **WebAssembly (Rust)**. 

**SQL::TRACE** allows you to write SQL queries and visually inspect the underlying relational operator execution trees, storage engine structures, and hardware-level performance metrics in real time.

---

## Live Demo

Run the visualizer directly in your browser:
**[https://ruchi366.github.io/SQL-Trace/sql-trace.html](https://ruchi366.github.io/SQL-Trace/sql-trace.html)**

*(Or open `sql-trace.html` locally using any standard static file server or VS Code Live Server).*

---

## Key Features

### 1. Dynamic Physical Operator DAG
* **Pipeline Visualization:** Visualizes query plans as a Directed Acyclic Graph (DAG) of physical relational operators.
* **Real-time Operator State:** Tracks live tuple throughput and intermediate row counts across sequential scans (`Seq Scan`), hash builds (`Hash (Build)`), probe phases (`Hash Join (probe)`), projections, and final results[cite: 1, 2].
* **Execution Strategies:** Compare execution strategies like **Hash Join vs. Nested Loop** and **Index Scan vs. Full Table Scan**[cite: 1, 2].

### 2. Storage Engine & Index Inspection
* **Interactive B+ Tree:** Real-time tree hierarchy rendering root, internal, and leaf node splits and key lookups[cite: 1, 2].
* **Buffer Pool Frames:** Inspect frame caching and eviction dynamics through an integrated LRU cache table[cite: 1, 2].
* **Tuple Row Inspector:** Inspect raw record schemas and physical row states as pages are accessed[cite: 1, 2].

### 3. Hardware-Level Execution Metrics
* **Buffer Cache Hit/Miss:** Live ratio metrics showing memory cache performance[cite: 1, 2].
* **Disk I/O Reads:** Tracks physical page allocations and simulated read operations[cite: 1, 2].
* **WASM Memory Profiling:** Live telemetry tracking active execution memory buffers and WebAssembly linear heap allocations[cite: 1, 2].

---

## Example Query

```sql
SELECT orders.id, customers.name, orders.amount
FROM orders
JOIN customers ON orders.customer_id = customers.id
WHERE orders.amount > 5000;
