[[Concepts]] #ProbabilityAndStatisticsNotes

# 1. **Introduction to Probability**  
## **Basics**

![[Pasted image 20241023081045.png]]
**Probability(P)** is the measure of how likely an **event (E)** is to happen, and it ranges between **0 (impossible)** and **1 (certain)**.
  $$P(E) = \frac{\text{Number of desired outcomes}}{\text{Total outcomes}}$$
Where the **numerator** is the **count of desired outcomes** and the **denominator** is the **total number of possible outcomes**.
![[Pasted image 20241023081423.png]]
**Random Experiment**: An **experiment** where the **outcomes cannot be predicted with certainty** (e.g., rolling a die).
**Sample Space (S)**: The **set of all possible outcomes**. For example, the sample space for rolling a die is:
     $$S = \{1, 2, 3, 4, 5, 6\}$$
**Event (E)**: A **subset of the sample space**, such as getting an even number when rolling a die:
     $$E = \{2, 4, 6\}$$

### **Single Die Example**
 When rolling a single die:
   - **Total possible outcomes**: 6 (since a die has 6 faces).
   - **Probability of rolling a specific number (e.g., a 3)**:
     $$P(3) = \frac{\text{Number of desired outcomes}}{\text{Total outcomes}} = \frac{1}{6}$$
   - **Probability of rolling an even number (2, 4, 6)**:
     $$P(\text{even}) = \frac{\text{Number of desired outcomes}}{\text{Total outcomes}} = \frac{3}{6} = \frac{1}{2}$$
     
![[Pasted image 20241023081930.png]]
### **Throwing Two Dice Example Using the Grid Method**  
When **rolling two dice simultaneously**, the total number of outcomes is 36 $(6 \times 6)$. The **Grid Method** is a great way to visualize all possible outcomes.

Here's how the grid is structured. Each cell represents a pair of outcomes from die A and die B:

   ```
                     Die B
		     1    2    3    4    5    6
		   -----------------------------
		 1| 1,1  1,2  1,3  1,4  1,5  1,6
		 2| 2,1  2,2  2,3  2,4  2,5  2,6
Die A	 3| 3,1  3,2  3,3  3,4  3,5  3,6
		 4| 4,1  4,2  4,3  4,4  4,5  4,6
		 5| 5,1  5,2  5,3  5,4  5,5  5,6
		 6| 6,1  6,2  6,3  6,4  6,5  6,6
   ```

   - Each **row** represents the outcomes of **die A**.
   - Each **column** represents the outcomes of **die B**.
   - For example, in the cell where row 3 and column 4 intersect, the result is (3,4), meaning die A shows a 3 and die B shows a 4.

   Using this grid, you can easily:
   - **Count outcomes**: For example, if you want the probability of rolling a sum greater than 7, you can simply count the number of pairs where the sum of the two dice is greater than 7.
   - **Example**: Find the probability that the sum of two dice is 8. The pairs where the sum is 8 are:
     - $(2,6), (3,5), (4,4), (5,3), (6,2)$
     - These are 5 favorable(desired) outcomes out of 36, so:
     $$P(\text{sum} = 8) = \frac{\text{Number of desired outcomes}}{\text{Total outcomes}} = \frac{5}{36}$$

![[Pasted image 20241023082438.png]]
### **Tossing Two Coins Example Using the Grid Method**
When **tossing two coins simultaneously**, each coin has two possible outcomes: **Head (H)** or **Tail (T)**. Therefore, the total possible outcomes are $( 2 \times 2 = 4 ).$

Here’s how the grid looks for two coins:

```
				(Coin B)
				
			     H    T
			   ---------
(Coin A)    H | H,H  H,T
			T | T,H  T,T
```

- Each **row** represents the outcome of **Coin A**.
- Each **column** represents the outcome of **Coin B**.
- For example, the cell where row **H** and column **T** intersect gives $(H, T)$, meaning Coin A shows **Head** and Coin B shows **Tail**.

#### 1. **Total Outcomes**
   The total number of outcomes when tossing two coins is 4:
   $S = \{(H,H), (H,T), (T,H), (T,T)\}$

#### 2. **Probability of Getting the Same Outcome (Both Coins Show Heads or Both Show Tails)**
   - The favorable (desired) outcomes where both coins show the same result (**either both heads** or **both tails**) are:
     $(H,H), (T,T)$
   - There are 2 favorable outcomes. Hence, the probability is:
     $P(\text{same outcome}) = \frac{\text{Number of desired outcomes}}{\text{Total outcomes}} = \frac{2}{4} = \frac{1}{2}$

#### 3. **Probability of Getting Different Outcomes (One Coin Shows Heads and the Other Shows Tails)**
   - The favorable(desired) outcomes where the two coins show different results (one head, one tail) are:
     $(H,T), (T,H)$
   - There are 2 favorable outcomes. Hence, the probability is:
     $P(\text{different outcomes}) = \frac{\text{Number of desired outcomes}}{\text{Total outcomes}} =  \frac{2}{4} = \frac{1}{2}$

#### 4. **The Probability of Getting At Least One Head**

**Definition**: The probability of getting **at least** one head means that you get **one or more heads**. This excludes the case where there are no heads (i.e., both tails).

- **Favorable outcomes**:
  ${(H,H), (H,T), (T,H)}$
  These outcomes have at least one head.
  
- **Total outcomes**: 4
- **Number of favorable(desired) outcomes**: 3

Hence, the probability of getting at least one head is:
$P(\text{at least one head}) = \frac{\text{Number of favorable outcomes}}{\text{Total possible outcomes}} =  \frac{3}{4}$

##### Notation for "At Least" X = H:
$P(X \geq 1) = P(X = 1) + P(X = 2) = \frac{2}{4} + \frac{1}{4} = \frac{3}{4}$
This means that the probability of getting **at least 1 head** is $( \frac{3}{4})$.

#### 5. **The Probability of Getting At Most One Head**

**Definition**: The probability of getting **at most** one head means that the number of heads is **either 0 or 1**. This excludes the case where there are two heads.

- **Favorable outcomes**:
  ${(H,T), (T,H), (T,T)}$
  These outcomes have at most one head.
  
- **Total outcomes**: 4
- **Number of favorable(desired) outcomes**: 3

Hence, the probability of getting at most one head is:
$P(\text{at most one head}) = \frac{\text{Number of desired outcomes}}{\text{Total possible outcomes}} =  \frac{3}{4}$

##### Notation for "At Most" X = H:
$P(X \leq 1) = P(X = 0) + P(X = 1) = \frac{1}{4} + \frac{2}{4} = \frac{3}{4}$
This means that the probability of getting **at most 1 head** is $\frac{3}{4}$.







![[Pasted image 20241023110100.png]]

![[Pasted image 20241023105021.png]]
### **Tossing 3 Coins using Tree Method**
When **tossing three coins simultaneously**, each coin can land on either **Head (H)** or **Tail (T)**. Thus, the total possible outcomes:
- Each coin has two outcomes: **H** or **T**.
- The total number of outcomes for **3 coins** is $(2 \times 2 \times 2 = 8)$ outcomes.
##### Tree Diagram:
Starting with the first coin, we branch out into two possibilities: **H (Head)** and **T (Tail)**. Each of these branches then has two more possibilities for the second coin, and so on for the third coin:

![[Pasted image 20241023105457.png]]

```
Tossing Three Coins Simultaneously
         H         T        Coin A
        / \       /  \     
       H   T     H    T     Coin B
      / \ / \   / \  / \
     H  T H  T  H  T H  T   Coin C
```

The **outcomes** from the tree are:
$S = \{ HHH, HHT, HTH, HTT, THH, THT, TTH, TTT \}$

#### Probability of Different Events

##### 1. Probability of Getting Exactly One Head $P(X = 1H)$
- From the tree, the outcomes with exactly one head are:
  $\{HTT, THT, TTH\}$
  - There are 3 favorable outcomes out of 8.
  - Probability:
    $P(X = 1H) = \frac{3}{8}$

##### 2. Probability of Getting Exactly Two Heads $P(X = 2H)$
- The outcomes with exactly two heads are:
  $\{ HHT, HTH, THH \}$
  - There are 3 favorable outcomes out of 8.
  - Probability:
    $P(X = 2H) = \frac{3}{8}$

##### 3. Probability of Getting Three Heads $P(X = 3H)$
- The only outcome with all heads is:
  $\{ HHH \}$
  - There is 1 favorable outcome out of 8.
  - Probability:
    $P(X = 3H) = \frac{1}{8}$

#### Concepts of "At Least" and "At Most"

##### At Least One Head $P(X \geq 1)$
- This means **one or more heads**.
- Favorable outcomes: \{ HHH, HHT, HTH, HTT, THH, THT, TTH \} (7 outcomes)
- Probability:
  $P(X \geq 1) = P(X = 1) + P(X = 2) + P(X = 3) = \frac{3}{8} + \frac{3}{8} + \frac{1}{8} = \frac{7}{8}$

##### At Most Two Heads $P(X \leq 2)$
- This means **zero, one, or two heads**.
- Favorable outcomes: $\{ TTT, HTT, THT, TTH, HHT, HTH, THH \}$ (**7 outcomes**)
- Probability:
  $P(X \leq 2) = P(X = 0) + P(X = 1) + P(X = 2) = \frac{1}{8} + \frac{3}{8} + \frac{3}{8} = \frac{7}{8}$

### Total Probability Law
The **sum of probabilities for all the events** equals 1, known as the **Total Probability Law**:
$$\text{Sum of Probabilities of all the Events} = 1 $$
$$P(X = 0H) + P(X = 1H) + P(X = 2H) + P(X = 3H) = 1$$
- $P(X = 0H) = \frac{1}{8}$
- $P(X = 1H) = \frac{3}{8}$
- $P(X = 2H) = \frac{3}{8}$
- $P(X = 3H) = \frac{1}{8}$

$\frac{1}{8} + \frac{3}{8} + \frac{3}{8} + \frac{1}{8} = 1$

#### Probability of **Happening** and **Not Happening**
- If $P(A)$ is the probability of an event happening, the probability of the event **not happening** is:
$$P(\text{Not Happening}) = 1 - P(A)$$
- Example: If $$P(\text{Heads on all 3 coins}) = \frac{1}{8}$$then, the probability of **not getting all heads** is:
$$P(\text{Not All Heads}) = 1 - \frac{1}{8} = \frac{7}{8}$$


## **Counting Principle**
https://www.youtube.com/watch?v=DK8BV30N_c4&t=389s
52:03
