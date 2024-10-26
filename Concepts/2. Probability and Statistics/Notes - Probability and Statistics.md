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

### **Permutation and Combination: All \( n \) Items Taken at Once**

#### 1. **Permutation (When Order Matters)**

**Definition**: A **permutation** is an arrangement of items where **order matters**. If you have $( n )$ different items, the number of ways to arrange (or permute) all of them **at once** is called the **number of permutations**.

The **formula** for the number of permutations when arranging $( n )$ items taken all at once is:

$$P(n) = n!$$

This is because:
- For the **first position**, you have $( n )$ choices.
- Once an item is placed in the first position, you have $( n-1 )$ choices left for the second position.
- For the **third position**, you have $( n-2 )$ choices, and so on, until you reach the last position where you only have **1 choice** left.

Thus, the total number of ways to arrange $( n )$ items taken all at once is:
$$n \times (n-1) \times (n-2) \times \dots \times 1 = n!$$

![[Pasted image 20241024110716.png]]
#### **Box Method for Permutation**
We have 5 items to arrange into 5 boxes. Each box represents a position in the arrangement. The number of choices decreases as we place each item in a box.

```
	 +-----+       +-----+     +-----+     +-----+       +-----+
	 | Box |  ->   | Box |  -> | Box |  -> | Box |  ->   | Box |
	 |  1  |       |  2  |     |  3  |     |  4  |       |  5  |
	 +-----+       +-----+     +-----+     +-----+       +-----+
	 Choices:     Choices:     Choices:     Choices:     Choices:
	    5            4            3            2            1
	(5 items)   (4 items left) (3 items left) (2 items left) (1 item left)
```

**Example**: Arranging the items $( A, B, C, D, E )$ taken all at once.

Let’s calculate the number of different ways to arrange these 5 items using the **box method**:

- **Step 1**: Place an item in the first box. You have **5 choices** for this (any one of $( A, B, C, D, E ))$.
  
- **Step 2**: After filling the first box, there are **4 items** left for the second box.
  
- **Step 3**: For the third box, you have **3 remaining items** to choose from.
  
- **Step 4**: For the fourth box, only **2 items** remain.
  
- **Step 5**: For the last box, you are left with **1 item**.

So, using the box method, the total number of permutations (arrangements) is:

$$ 5 \times 4 \times 3 \times 2 \times 1 = 5! = 120 $$

Thus, the number of ways to arrange $( A, B, C, D, E )$ all at once is **120**.

#### 2. **Combination (When Order Does Not Matter)**

**Definition**: A **combination** is a selection of items where **order does not matter**. If you have $( n )$ different items and you want to **select all of them** at once (without arranging them), then the number of ways to do this is **always 1**.

This is because:
- If order doesn’t matter, there is **only one way** to select all items. No matter how you rearrange them, the selection remains the same.

So, when **selecting all $( n )$ items** at once, the number of combinations is:

$$C(n) = 1$$

![[Pasted image 20241024110456.png]]

#### **Combination (Order Doesn’t Matter) vs Permutation (Order Matters)**

Imagine you are selecting **2 students** (Shivam and Ankit) from a group of 10 students in a college. Since **order doesn’t matter**, selecting **Shivam and Ankit** is the same as selecting **Ankit and Shivam**. This means there is **only 1 combination** for this selection, as order does not affect the group.

However, if you were **arranging** the students in an order (like for seating), then you would consider both **Shivam-Ankit** and **Ankit-Shivam** as different, leading to more possibilities (which is a **permutation** problem).

---

![[Pasted image 20241024121621.png]]

![[Pasted image 20241024122412.png]]

### **Permutations: $N$ Different Items Taken $( r )$ at a Time**
**Concept**: When you are arranging or selecting items where **order matters**, and you are not taking all the items, but a subset $( r )$ of the total $( n )$, the number of ways to arrange the items is called the **number of permutations**.

The formula for the **number of permutations** when choosing $( r )$ items from $( n )$ different items is:

$$^{n}P_{r} = P(n, r) = \frac{n!}{(n-r)!}$$

#### **1. Box Method for Permutation (Choosing $( r )$ at a Time)**

- Let’s say we have $5$ items: $( A, B, C, D, E )$, and we want to take **3 items** at a time to form permutations.
- The **box method** helps us visualize this by placing $( r = 3 )$ boxes for 3 positions, and each position can be filled by one of the $( n )$ items:

```
 +-----+      +-----+      +-----+
 | Box |  ->  | Box |  ->  | Box |
 |  1  |      |  2  |      |  3  |
 +-----+      +-----+      +-----+
 Choices:     Choices:     Choices:
    5            4            3
(5 items)   (4 items left)  (3 items left)
```

- In the first box, we have **5 choices** (any one of the items $( A, B, C, D, E )$).
- After placing one item in the first box, we have **4 items left** for the second box.
- After filling two boxes, we have **3 items left** for the third box.

Thus, the number of ways to arrange **3 items** from the 5 is:

$$^{n}P_{r} = ^{5}P_{3} = P(5, 3) = 5 \times 4 \times 3 = 60$$

In general, the formula is:

$$^{n}P_{r} = P(n, r) = \frac{n!}{(n - r)!}$$

#### **2. Example: Permuting 4 Letters from “DELHI”**

If we take the word "DELHI" and want to arrange 4 letters from it, we calculate the number of permutations using the same formula.

For $( n = 5 )$ (letters in "DELHI") and $( r = 4 )$ (we want to arrange 4 letters):

$$^{5}P_{4} = P(5, 4) = \frac{5!}{(5 - 4)!} = \frac{5 \times 4 \times 3 \times 2 \times 1}{1!} = 120$$

So, there are **120 ways** to arrange 4 letters from "DELHI".

#### **3. Combinations: N Different Items Taken $( r )$ at a Time**

**Concept**: In **combinations**, where **order does not matter**, the formula is different. If we are selecting $( r )$ items from $( n )$ items without caring about the order, the formula is:

$$^{n}C_{r} = C(n, r) = \frac{n!}{r!(n - r)!}$$

#### Example: Combinations from 5 Items (Order Doesn't Matter)

Let’s say we want to select **2 items** from the set $( A, B, C, D, E )$, and we don’t care about the order of selection. To calculate the number of combinations, we use the formula:

$$^{n}C_{r} = C(5, 2) = \frac{5!}{2!(5 - 2)!} = \frac{5 \times 4}{2!} = \frac{20}{2} = 10$$

So, there are **10 combinations** of selecting 2 items from 5.

#### **Combinations Visualization Using the Grid (From Image)**

- The grid in the image visualizes all possible **combinations** of 2 letters from the set $({ A, B, C, D, E})$.
  
  ```
      A   B   C   D   E
  A  AA  AB  AC  AD  AE
  B  BA  BB  BC  BD  BE
  C  CA  CB  CC  CD  CE
  D  DA  DB  DC  DD  DE
  E  EA  EB  EC  ED  EE
  ```

- Diagonal and repeated elements are removed because **order does not matter** in combinations. For example, $( AB )$ and $( BA )$ are considered the same combination, so we only keep one.
- After removing duplicates, we are left with **10 unique combinations**.

---

![[Pasted image 20241024130011.png]]

Based on the provided image and the transcription, here’s a detailed explanation focusing on **permutations and combinations** for scenarios with repeated items (i.e., \( p \)-alike, \( q \)-alike, and \( r \)-alike items).

---

### **$( N )$ Different Items with Repeated Items Taken all at a time or all at once
When dealing with $( N )$ items where some **items are repeated**, calculating **permutations** (where order matters) and **combinations** (where order doesn't matter) requires adjusting for the repeated nature of some items.
#### 1. Permutations with Repeated Items:
$$\text{Number of Permutations} = \frac{n!}{p_1! \cdot p_2! \cdot \dots \cdot p_k!}$$

Where:
- $( n! )$ is the factorial of the total number of items.
- $( p_1!, p_2!, \dots, p_k! )$ are the factorials of the frequencies of the repeated items.

This formula ensures that we don't overcount the arrangements of indistinguishable items, treating them as the same.
#### **Example: Word "CALCULUS"**

Let's break down how we apply this to the word **CALCULUS**:
- Total letters: 8 $(C, A, L, C, U, L, U, S)$
- C occurs 2 times (P-alike),
- L occurs 2 times (Q-alike),
- U occurs 2 times (R-alike).

Using the formula:

$$\text{Permutations} = \frac{8!}{2! \cdot 2! \cdot 2!}$$

Calculating:

$$8! = 40320, \quad 2! = 2$$

$$\text{Permutations} = \frac{40320}{2 \cdot 2 \cdot 2} = \frac{40320}{8} = 5040$$

Thus, the total number of distinct permutations for the word **CALCULUS** is **5040**.

#### 2. Combinations with Repeated Items:

For **combinations** with repeated items, when you are **taking all items at once**, the result is always **1 combination**. This happens because:
- The order of selection does not matter in combinations.
- Since all items (including repeated ones) are being selected at once, there is no additional variability in how they can be grouped or selected differently.

#### **General Formula:**

$$\text{Number of Combinations} = 1$$

This holds true because when all items are taken at a time, no matter how many repeated items there are, there is only **one** way to select them. This is due to the fact that combinations disregard order and treat all identical items as indistinguishable from each other.

#### Example: Combinations for "CALCULUS"

If you're selecting **all the letters** in the word **CALCULUS** (C, A, L, C, U, L, U, S), the number of combinations is simply **1** because no matter the repetitions of letters, the selection is the same.

![[Pasted image 20241024134043.png]]


![[Pasted image 20241025091546.png]]

![[Pasted image 20241025092853.png]]

![[Pasted image 20241025093723.png]]

![[Pasted image 20241025094022.png]]

### Counting Principles and Probability Concepts from the Images

#### **Scenario 1: Number of Ways with Multiple Options**
  
1. **3 Letters into 4 Post Boxes**:
   - Total number of ways to distribute 3 letters into 4 post boxes is calculated as:
     $$4 \times 4 \times 4 = 4^3 = 64$$
   - This demonstrates how for each letter, you have 4 choices (one for each post box), leading to a multiplicative total for 3 letters.

2. **Three Dice Thrown**:
   - Total number of ways to throw 3 dice, where each die has 6 faces:
     $$6 \times 6 \times 6 = 6^3 = 216$$
   - The principle applied here is similar, where each independent die roll has 6 possible outcomes.

3. **Five Coin Tosses**:
   - The number of ways to toss 5 coins, each with 2 outcomes (heads or tails), is:
     $$2 \times 2 \times 2 \times 2 \times 2 = 2^5 = 32$$
   - Each coin flip is an independent event, so the total number of outcomes is the product of 2 for each coin.

#### **Scenario 2: Sampling - Drawing Balls from a Bag**

##### With and Without Replacement

1. **Without Replacement:**
   - Consider a bag with 3 yellow balls and 5 non-yellow balls (total 8 balls). The probability of drawing **2 yellow balls without replacement** is:
     $$P(\text{1st yellow}) = \frac{3}{8}, \quad P(\text{2nd yellow after 1st}) = \frac{2}{7}$$
   - Multiply these probabilities for the final result:
     $$P(\text{2 yellows}) = \frac{3}{8} \times \frac{2}{7} = \frac{6}{56} = \frac{3}{28}$$
   - In **without replacement** cases, the sample space decreases after each draw, making each event dependent on the previous one.

2. **With Replacement:**
   - In this case, the total number of balls remains constant after each draw. For example, if there are 6 white balls out of 10, the probability of drawing **6 white balls with replacement** is:
     $$P(\text{white ball}) = \frac{6}{10}, \quad P(\text{2nd white ball}) = \frac{6}{10}$$
   - The total probability is calculated as:
     $$P(\text{6 white balls}) = \left( \frac{6}{10} \right)^6$$
   - **With replacement** implies independent events, where each draw does not affect the probability of the subsequent draws.

#### **Multiple and Addition Principle**

1. **Multiplication Principle** (for dependent tasks):
   - If there are multiple stages to a task, and each stage has a certain number of possible outcomes, the total number of outcomes is the **product** of the possibilities at each stage. For example:
     $$\text{Ways to roll 3 dice} = 6 \times 6 \times 6 = 216$$
   - Each die roll is an independent event, and the total outcomes are calculated by multiplying the number of outcomes for each stage.

2. **Addition Principle** (for independent tasks):
   - If there are multiple mutually exclusive tasks (tasks that cannot happen simultaneously), the total number of ways to complete the tasks is the **sum** of the individual possibilities. For example, if you can complete task A in 5 ways and task B in 4 ways, the total number of ways to choose between A and B is:
     $$5 + 4 = 9$$
   - This applies to scenarios where different outcomes do not depend on each other and cannot happen at the same time.

#### **Scenario 3: Playing Cards**

- A deck of 52 cards can be divided as:
  - **26 red cards** (13 diamonds, 13 hearts)
  - **26 black cards** (13 clubs, 13 spades)
  - **Face cards**: King, Queen, Jack (4 suits × 3 cards = 12 face cards)
  - **Non-face cards**: Ace through 10 (4 suits × 10 cards = 40 non-face cards)
  
  - **Example of selection**:
    If you were to select a face card from the deck, the probability is:
    $$P(\text{face card}) = \frac{12}{52} = \frac{3}{13}$$


https://www.youtube.com/watch?v=DK8BV30N_c4&t=389s
2:00