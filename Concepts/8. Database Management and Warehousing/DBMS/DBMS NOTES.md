[[gate]]
# Introduction
## Data
Raw, unprocessed facts and figures collected from various sources, such as numbers, text, or observations, which on their own don’t carry specific meaning. 
Ex: all stock prices on the market.
## Information
Processed data that has been organized or interpreted to provide meaningful insights. 
Ex: identifying profitable stocks from the entire stock market data.
## Database
A structured collection of organized data, allowing easy access, retrieval, and management of information. 
Ex: a database storing all stock market transactions.
## Database Management System (DBMS)
Software that enables the creation, management, and querying of databases, making it easier to store, modify, and retrieve data. 
Ex: using a DBMS to filter stocks by price, volume, or performance.

## Schema
The schema is like the **structure or blueprint** of a database. It defines how the data is structured and what types of data will be stored.
Ex: **Student(name, age, course)** is the schema because it defines what information we will store for each student: their name, age, and course.

## Instance
The instance is the **actual data** stored within the schema at any given time. It’s the snapshot of information in the database at a specific moment.
Ex: **Student("Alice", 20, "Math")**
# Basics Transactions and concurrency control
## Transactions
A **transaction** is a sequence of operations performed as a single logical unit of work, typically involving read/write operations on the database. Its goal is to ensure data integrity and consistency, even in cases of system failures.
For ex: in a bank, transferring $100 from Account A to Account B involves two main operations: deducting $100 from Account A and adding $100 to Account B. Both operations must complete successfully to maintain accurate balances; otherwise, neither should apply.

Here, the **transaction** is the **entire process of transferring $100 from Account A to Account B**. It consists of two main operations:
1. **Deducting $100 from Account A**.
2. **Adding $100 to Account B**.

### Properties of Transactions (ACID):
1. **Atomicity**: Ensures the transaction is **"all or nothing"** – either all operations succeed, or none are applied.
   For ex: if the system fails after deducting $100 from Account A but before adding it to Account B, the transaction will roll back, leaving both accounts unchanged.
2. **Consistency**: Ensures the database moves from one valid state to another, maintaining integrity constraints.
   For ex: ensures that if both operations are completed, the total balance across accounts remains consistent.
3. **Isolation**: Transactions operate independently; intermediate states are hidden from other transactions.
   For ex: if two people transfer funds at the same time, each transaction proceeds as though it's alone, preventing interference between them.
4. **Durability**: Once committed, changes are permanent, even in the case of system crashes.
   For ex: after the transaction is committed (completed), the changes persist, so Account B retains the added $100 even if the system crashes.
### Q.1
> GATE CS 2016, Set 1, Question 32
"Which one of the following is **NOT** a part of the ACID properties of database transactions?"

Options:
- (a) Atomicity
- (b) Consistency
- (c) Isolation
- **(d) Deadlock-freedom** (Answer)

The correct answer is **(d) Deadlock-freedom**, as it is not part of the ACID properties (Atomicity, Consistency, Isolation, Durability).

### Transaction States
Taking the previous example of transferring $100 from Account A to Account B:
1. **Active**: The transaction starts, deducting $100 from Account A.
2. **Partially Committed**: $100 is deducted from Account A, but not yet added to Account B, and data is in memory, not saved to disk.
3. **Failed**: The transaction can’t proceed (e.g., system crash), and $100 isn't added to Account B.
4. **Aborted**: The transaction rolls back, restoring the $100 to Account A.
5. **Committed**: $100 is successfully added to Account B, and changes are saved permanently.

#### Q1.
If the transaction is in which of the state that we can guarantee that database is in consistent state?
- (a) Aborted
- (b) Committed
- **(c) Both aborted & committed** (Answer)
- (d) None

### Advantages of Concurrency:
1. **Improved Performance**: Multiple transactions execute simultaneously, utilizing CPU more efficiently.
2. **Better Resource Utilization**: Optimizes resource use, minimizing idle time.
3. **Increased Throughput**: Allows more transactions to complete in less time, boosting system productivity.
### Concurrency Problems in DBMS:

When transactions are executed concurrently, interleaving of operations may lead to issues, despite each transaction following ACID properties individually. 
For ex: two transactions trying to transfer or update Account A's balance can create problems:

1. **Dirty Read**: Occurs when Transaction A reads uncommitted data from Transaction B.
   - *Example*: Transaction B adds $100 to Account B but hasn’t committed. Transaction A reads this increased balance, leading to inconsistencies if B rolls back.

2. **Unrepeatable Read**: Happens when Transaction A reads the same data twice but gets different results because Transaction B has modified it in between.
   - *Example*: Transaction A reads Account B’s balance twice; meanwhile, Transaction B adds $100, causing different values for each read.

3. **Lost Update**: Occurs when two transactions overwrite each other’s updates.
   - *Example*: Transactions A and B both add $100 to Account B at the same time. Only one addition shows, causing a discrepancy.

4. **Phantom Read**: When a transaction reads a set of rows that another transaction modifies by adding/removing rows.
   - *Example*: Transaction A calculates the total of all account balances. During this, Transaction B adds a new account, affecting A's calculation.
#### Q1.

> The following schedule is suffering from:
> 
> - (a) Lost update problem
> - **(b) Unrepeatable read problem** (Answer)
> - (c) Both A and B
> - (d) Neither A nor B

The schedule shows:
1. $( T_1 )$: Reads $( y )$.
2. $( T_2 )$: Reads $( x )$, reads $( y )$, performs $( y = x + y )$, and writes $( y )$.
3. $( T_1 )$: Reads $( y )$ again.

**Solution:**
This schedule demonstrates an **unrepeatable read problem** because $( T_1 )$ reads $( y )$ before and after $( T_2 )$ modifies it, resulting in different values on each read. So, the answer is **$(b)$ Unrepeatable read problem**.

#### Q2.
Which of the following scenarios may lead to an irrecoverable error in a database system?

- (A) A transaction writes a data item after it is read by an uncommitted transaction
- (B) A transaction reads a data item after it is read by an uncommitted transaction
- (C) A transaction reads a data item after it is written by a committed transaction
- (D) A transaction reads a data item after it is written by an uncommitted transaction (Answer)

In database management systems, an irrecoverable error typically occurs when a transaction reads data written by an uncommitted transaction, and if the uncommitted transaction fails or is rolled back, it leaves the system in an inconsistent state. This scenario is commonly known as a **"dirty read."**

- **Option D** is correct because it describes a scenario where a transaction reads data written by an uncommitted transaction, which can lead to an irrecoverable error if the uncommitted transaction fails.

### Schedules
A **schedule** is an ordered sequence of operations from multiple transactions in a database that determines the order in which these operations are executed. It ensures that transactions interact correctly, maintaining data consistency and integrity.

**Schedules** are used to organize multiple operations. When transactions occur simultaneously or in quick succession, they can be combined into a schedule to ensure that the operations run in the correct order and maintain data integrity. 
For ex: Transferring $100 from Account A to Account B.
1. **Operation Requirements:** 
   - To transfer $100 from Account A to Account B, two key actions are required:
     - Deduct $100 from Account A.
     - Add $100 to Account B.
   - These actions need to execute together to keep account balances accurate. If one action fails, both should ideally be rolled back.

2. **Serial Schedule (One-by-One Execution):**
   - In a **serial schedule**, each transaction is completed in sequence without any overlap. For example:
     - First, the system might complete the entire transaction for deducting $100 from Account A.
     - Then, it will move to adding $100 to Account B.
   - This ensures that data remains consistent, but it’s slower because transactions do not overlap.

3. **Non-Serial Schedule (Concurrent Execution):**
   - A **non-serial schedule** allows `interleaving` operations from different transactions. For instance:
     - While deducting $100 from Account A, another transaction (like a deposit to Account B by another user) could also be processed.
   - This allows for concurrency, increasing efficiency, but risks inconsistency if not handled carefully.

### Conflicting/Non-Conflicting Instructions
**Conflicting instructions** occur when two operations, performed by different transactions, target the **same data item** and **at least one** of the operations is a write operation.

1. **Non-Conflicting Pair (Read-Read)**: 
   - Example: Transaction $( T_1 )$ reads data item $( Q )$, and then Transaction $( T_2 )$ also reads $( Q )$.
   - **Result**: No conflict because both transactions are only reading; they don’t interfere with each other’s operations.

2. **Conflicting Pair (Read-Write)**:
   - Example: Transaction $( T_1 )$ reads $( Q )$, and then Transaction $( T_2 )$ writes to $( Q )$.
   - **Result**: Conflict occurs because the write operation can change $( Q )$, affecting the validity of $( T_1 )$’s read result.

3. **Conflicting Pair (Write-Read)**:
   - Example: Transaction $( T_1 )$ writes to $( Q )$, and then Transaction $( T_2 )$ reads $( Q )$.
   - **Result**: Conflict occurs because $( T_2 )$’s read could retrieve modified data from $( T_1 )$’s write, creating a dependency.

4. **Conflicting Pair (Write-Write)**:
   - Example: Transaction $( T_1 )$ writes to $( Q )$, and then Transaction $( T_2 )$ writes to $( Q )$ as well.
   - **Result**: Conflict occurs because each write operation can overwrite the other’s changes, leading to inconsistent data.

> **"Managing these conflicts ensures data consistency in concurrent transactions, which is essential for maintaining the integrity of database operations."**

### Conflict Equivalent
Conflict equivalence between two schedules means they produce the **same outcome** on the database state by ensuring the same final values, even if the operations occur in different orders. 
For two schedules to be conflict equivalent, they must be able to transform into each other by **swapping non-conflicting instructions**.

![[Pasted image 20241027185954.png]]

1. **Two Transactions, $T_1$ and $T_2$**:
   - $T_1$: Reads from Account $A$, deducts 50, then reads from Account $B$.
   - $T_2$: Reads from Account $B$, adds 50, then reads from Account $A$.

2. **Conflict-Free Operations**:
   - The schedules are able to swap **non-conflicting instructions** (those that do not involve writing or modifying the same data at the same time) without affecting the result.
   - For example, reading from Account $B$ in $T_2$ and writing to Account $A$ in $T_1$ can happen in either order since they are independent.

3. **Conflict-Equivalent Schedules**:
   - By swapping non-conflicting operations, we can rearrange the sequence of instructions while preserving the correctness of the result.
   - In this example, both schedules perform the same set of operations on Accounts $A$ and $B$, leading to the same final state in both accounts, even though the order of operations differs.

4. **Conclusion**:
   - Since these two schedules lead to the same final result and can be transformed into each other by reordering non-conflicting operations, they are considered **conflict-equivalent schedules**.
   - Conflict-equivalent schedules help in concurrency control by allowing more flexible ordering of transactions while ensuring the integrity of the data.

In essence, conflict equivalence allows concurrent transactions to be reordered safely, as long as data integrity is maintained, which is crucial for ensuring consistent database states in multi-transaction environments.

#### Q1.
![[Pasted image 20241027223800.png]]
* ***Option a** is **Conflict Equivalent** because Conflict Operations aren't Swapped.
* **Option b** is **not Conflict Equivalent** because WD in T1 and RD in T2 swapped operations although they are Conflict Operations.
* **Option c** is **not Conflict Equivalent** because WD in T1 and RD in T2 swapped operations although they are Conflict Operations.
* **Option d** is **not Conflict Equivalent** because RC in T1 and WC in T2 swapped operations although they are Conflict Operations.

### Conflict Serializable Schedule
A **conflict serializable schedule** is one that can be transformed into a **serial schedule** by a series of swaps of **non-conflicting** operations. Essentially, if we can rearrange the operations in a non-serial schedule to match a serial order (where transactions are executed one at a time without overlapping), we ensure that the outcome is the same as if the transactions had run in isolation. This process is crucial for **concurrency control** in databases.

#### Q2.
![[Pasted image 20241027234225.png]]
Find the Node with Indegree Zero, note it then delete it and it's edges then find the next node with indegree Zero and then note it... & so on.

**Determining a conflict-equivalent serial schedule using a precedence graph and identifying the correct serial order by removing nodes with an indegree of zero.**

##### Steps to Solve Conflict Equivalent Serial Order Using Precedence Graph

1. **Construct the Precedence Graph**:
   - Each transaction is a node.
   - Draw directed edges from one transaction to another if there is a conflicting operation (read-write or write-write) on the same data item, with the direction indicating the dependency order.

2. **Identify Nodes with Indegree Zero**:
   - A node with an **indegree of zero** means it has no dependencies on other transactions and can be scheduled first in a serial order.
   - After selecting a node with zero indegree, "remove" it from the graph, which entails:
     - Deleting the node.
     - Removing all outgoing edges from that node.

3. **Repeat Until All Nodes are Removed**:
   - Continue this process by finding nodes with indegree zero, noting their serial order, and removing them until the graph is empty.

4. **Resulting Order**:
   - The order in which you remove nodes represents a possible serial schedule that is conflict-equivalent to the original schedule.

The order you found, **$( T_1 \rightarrow T_3 \rightarrow T_4 \rightarrow T_2)$**, represents a **conflict-equivalent serial schedule** for the given schedule $( S )$.

**What This Order Means?**

This order means that the original interleaved schedule $( S )$ is equivalent, in terms of conflicts, to executing the transactions in the serial order of:
- $( T_1 )$ first,
- then $( T_3 )$,
- followed by $( T_4 )$,
- and finally $( T_2 )$.

In other words, if we were to run these transactions one after the other without any overlapping (purely serial execution), the order **$( T_1 \rightarrow T_3 \rightarrow T_4 \rightarrow T_2 )$** would yield the same result as the original schedule $( S )$ in terms of data consistency and conflicts.

#### Q3.
![[Pasted image 20241027235659.png]]
* Since the precedence graph of $S_1$ has a cycle, the schedule is **not conflict serializable**. If it is acyclic, the schedule is **conflict serializable** but here it is not.
* Since the precedence graph of $S_2$ has **no cycle**, the schedule is **conflict serializable**. If it is acyclic, the schedule is **conflict serializable** and here it is.

#### Q4.
![[Pasted image 20241028000903.png]]
### Conflict Equivalence vs Conflict Serializable Schedule
- Two schedules are **conflict equivalent** if they produce the same final result by following the same order of conflicting operations, even if the overall order differs.
- A schedule is **conflict serializable** if it can be reordered through swaps of non-conflicting operations to match a serial schedule.

### View Serializability
If a schedule is not conflict serializable, it might still be **view serializable**, meaning it can still produce a consistent outcome. View serializability allows for more flexible transaction orders than conflict serializability while ensuring correctness.

**Hierarchy**: Every conflict-serializable schedule is also view serializable, but not every view-serializable schedule is conflict serializable. 

**Checking Order**: We first check if a schedule is conflict serializable. If it is not, then we check for view serializability to determine if the schedule can still be considered valid.

![[Pasted image 20241028001201.png]]
### Non-Recoverable Schedule
A **non-recoverable schedule** is a schedule where a transaction reads data modified by another uncommitted transaction. If the first transaction fails or is rolled back, the second transaction cannot recover because it already used "dirty" or uncommitted data.

#### Example of a Non-Recoverable Schedule
1. **T1** starts and deducts $100 from Account A (uncommitted).
2. **T2** reads the modified balance of Account A and adds $100 to Account B based on this deduction.
3. **T1** fails or is rolled back (perhaps due to a system crash).

In this case, **T2** has already completed based on the data written by **T1**, which is now rolled back. **T2** cannot "un-apply" the addition to Account B, leading to an inconsistency. This situation is non-recoverable because the database cannot revert to a consistent state after **T1** fails.

#### Problem with Non-Recoverable Schedules
- Non-recoverable schedules can lead to **inconsistent states** in the database, as transactions depend on uncommitted data.
- They violate the principle that transactions should only use committed data.

### Recoverable Schedule 
1:53 https://www.youtube.com/watch?v=FchQ6wZVqsA
A **recoverable schedule** ensures that a transaction only commits if all transactions it depends on have also committed. This means that if **T2** reads data written by **T1**, **T1** must commit before **T2** can commit.

#### Example of a Recoverable Schedule
1. **T1** starts and deducts $100 from Account A.
2. **T1** commits after making the deduction.
3. **T2** reads the updated balance of Account A (now committed by **T1**) and proceeds to add $100 to Account B.
4. **T2** commits successfully.

In this case, since **T2** reads only committed data, the database can recover even if there’s a failure. **T1** has committed its changes before **T2** read the data, so there is no risk of inconsistency.

#### Advantage of Recoverable Schedules
- **Recoverable schedules** maintain database consistency because they ensure that transactions only use committed data.
- If a transaction fails, the dependent transactions can be rolled back without leaving the database in an inconsistent state.

# ER-Model
# Relational model, Functional Dependencies, Keys
# Normalization
# File organization, indexing (e.g., B and B+ trees)
# Relational algebra, tuple calculus, SQL
