# ShardPaxosBank

### Fault-Tolerant Distributed Banking System using Paxos, Sharding & Two-Phase Commit

ShardPaxosBank is a distributed transaction processing system built to explore how banking transactions can remain **consistent, available, and fault-tolerant across replicated shards**.

The system partitions accounts across multiple clusters, replicates data across nodes, and coordinates transactions using **Paxos/Multi-Paxos consensus** and **Two-Phase Commit (2PC)**. It supports both intra-shard and cross-shard transactions while handling node failures, concurrency conflicts, and quorum loss.

---

## 🏗️ System Architecture

Account data is distributed across multiple shards, with each shard replicated across several server nodes.

Replication and consensus allow the system to continue processing transactions despite fail-stop node failures while maintaining consistency between replicas.

<img width="922" alt="Distributed banking system architecture" src="https://github.com/user-attachments/assets/1ea73657-ad37-4ae8-a378-97b6e457d86a" />

<img width="922" alt="Shard and replication architecture" src="https://github.com/user-attachments/assets/6ac177e2-c496-4fed-9e21-43f7d2cc3f9b" />

---

## ⚙️ Transaction Processing

### Intra-Shard Transactions

Transactions involving accounts within the same shard are coordinated through **Paxos/Multi-Paxos consensus**.

Replicated nodes agree on transaction ordering before execution, allowing the shard to maintain consistent state even when individual replicas fail.

### Cross-Shard Transactions

Transactions spanning multiple shards require coordination between independent clusters.

The system combines:

* **Paxos** for consensus within each participating shard
* **Two-Phase Commit (2PC)** for atomic coordination across shards

A cross-shard transaction is therefore either committed across all participating shards or aborted without leaving partially applied state.

<img width="922" alt="Cross-shard transaction processing" src="https://github.com/user-attachments/assets/975481c9-1e2c-4fee-9f0d-ba22c8c42e35" />

---

## 🔑 Distributed Systems Concepts

### Consensus

Uses **Paxos and Multi-Paxos** to establish consistent transaction ordering across replicated nodes.

### Sharding & Replication

Partitions account data across clusters while maintaining multiple replicas per shard for scalability and fault tolerance.

### Atomic Transactions

Uses **Two-Phase Commit (2PC)** to coordinate transactions involving accounts located on different shards.

### Concurrency Control

Applies locking and conflict-management mechanisms to prevent conflicting transactions from producing inconsistent account states.

### Fault Tolerance

Designed around a fail-stop failure model. Transactions can safely abort when the system encounters conditions such as:

* insufficient account balances
* lock contention
* unavailable replicas
* insufficient consensus quorum

### Recovery & Durability

Uses **Write-Ahead Logging (WAL)** to preserve transaction history and support state recovery.

---

## 📊 Performance

The system evaluates distributed transaction performance using:

* **Throughput (transactions/second)**
* **Transaction latency**
* **Node-level execution metrics**

The implementation was tested with **9 server nodes running as independent processes across different ports**.

<img width="1512" alt="Nine-node distributed banking test" src="https://github.com/user-attachments/assets/d31c27b7-717c-4587-8c96-354f254eef7d" />

<img width="522" alt="Distributed transaction output" src="https://github.com/user-attachments/assets/d31c27b7-717c-4ed6-a494-2ebfa213f7c4" />

---

## 🧠 What I Implemented & Explored

This project provided hands-on experience with:

* Designing **sharded and replicated distributed architectures**
* Implementing **Paxos/Multi-Paxos consensus**
* Coordinating atomic cross-shard transactions using **2PC**
* Handling concurrent transactions using locking and conflict resolution
* Designing systems resilient to **node and quorum failures**
* Maintaining durability through **Write-Ahead Logging**
* Measuring transaction throughput and latency across distributed nodes
* Implementing communication between independent server processes

---

## 🛠️ Tech & Concepts

`Go` · `Distributed Systems` · `Paxos` · `Multi-Paxos` · `Two-Phase Commit` · `Sharding` · `Replication` · `RPC` · `WAL` · `Concurrency Control` · `Fault Tolerance`

---

## 📤 System Output

The system provides:

* Account balances across replicated servers
* Committed transaction logs for debugging and verification
* Transaction execution status
* Performance statistics for individual nodes
* Visibility into distributed transaction behavior during failures

---

## 🎯 Engineering Takeaways

ShardPaxosBank demonstrates the trade-offs involved in building strongly consistent distributed transaction systems.

The project explores how **consensus, replication, sharding, concurrency control, and atomic commit protocols** interact when transactions must remain correct despite failures and when data spans multiple independently replicated clusters.

It also demonstrates the additional coordination cost introduced by cross-shard transactions compared with transactions contained within a single consensus group.
