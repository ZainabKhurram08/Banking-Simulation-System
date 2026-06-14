# 🏦 Banking Simulation System

**A multithreaded C simulation demonstrating all five core Operating Systems concepts : Scheduling, Synchronization, Deadlock Prevention, IPC, and Memory Management in a real banking environment.**

---

## 🔍 Overview

This project simulates a fully functional banking system built entirely in C, where each customer is a thread, every transaction is synchronized, and resource allocation is managed by the Banker's Algorithm. Built as an **Operating Systems course project**, it covers every major OS concept in one cohesive simulation.

Customers are loaded from a file with types (VIP, Premium, Corporate, Loan, Regular) and processed through six sequential modules each demonstrating a different OS concept with real output, Gantt charts, log files, and metrics.

---

## ⚙️ Modules

### 1. 🕐 CPU Scheduling
Three scheduling algorithms run on the same customer queue and produce Gantt charts with waiting time and turnaround time metrics:
- **FCFS** : First Come First Serve
- **Priority Scheduling** : Preemptive, based on customer type (VIP > Corporate > Premium > Loan > Regular)
- **Round Robin** : Time quantum = 2ms

### 2. 🧵 Multithreading
Each customer is spawned as a **POSIX pthread**. Threads run concurrently simulating real parallel bank service. All threads are joined and destroyed cleanly after completion.

### 3. 🔒 Synchronization
- A **mutex** (`pthread_mutex_t`) protects every account balance update to prevent race conditions
- A **semaphore** (`sem_t`) limits concurrent deposits to a maximum of 2 at a time
- Regular and Premium customers perform deposits; VIP and Corporate customers perform withdrawals
- All transactions logged to `race_condition_log.txt` as proof of synchronization

### 4. 🧠 Deadlock Prevention — Banker's Algorithm
Implements the full **Banker's Algorithm** with 3 resource types:
- Maintains `allocation`, `maximum`, `need`, and `available` matrices
- Runs a **safety check** to find a safe sequence before granting any resource request
- Supports `request_resources()` and `release_resources()` with safe/unsafe state detection
- Test cases demonstrate both safe grants and rejected unsafe requests

### 5. 📨 IPC — Inter-Process Communication
Pipe-based message passing between customer threads and a bank server:
- **Request format:** `{ customer_id, account_id, operation, amount, priority }`
- **Response format:** `{ customer_id, account_id, status, new_balance }`
- Supports `DEPOSIT`, `WITHDRAW`, and `LOAN_REQUEST` operations
- All communication logged to `ipc_log.txt`

### 6. 💾 Memory Management — Page Replacement
Simulates virtual memory with a 20-page reference string and 4 frames:
- **FIFO** — First In First Out page replacement
- **LRU** — Least Recently Used page replacement
- Compares both algorithms on page faults, page hits, and fault rate
- Results logged to `page_fault_log.txt`

---
---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **C** | Core language |
| **pthreads** | Multithreading, mutex, and semaphore |
| **POSIX Pipes** | IPC between customer threads and bank server |
| **GCC** | Compilation |
| **Ubuntu** | Target OS environment |

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/ZainabKhurram08/bankingSimulation.git
cd bankingSimulation

# Compile
gcc main.c scheduling.c sync.c banker.c memory.c -o banking -lpthread

# Run
./banking
```

---

## 📐 OS Concepts Covered

- CPU Scheduling FCFS, Preemptive Priority, Round Robin
- POSIX Multithreading with pthreads
- Mutex and Semaphore synchronization
- Banker's Algorithm for deadlock avoidance
- Pipe-based Inter-Process Communication
- FIFO and LRU Page Replacement

---

