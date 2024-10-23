# Roadmap to High Performance Computing with Python

Achieving high performance computing (HPC) with Python involves leveraging parallel computing techniques, optimizing code, and utilizing specialized libraries.

## **1. Introduction to High Performance Computing (HPC) with Python**

### **1.1 Understanding HPC Concepts**

- **Definition and Importance of HPC**
	High-Performance Computing (HPC) is the use of powerful computers, called **clusters**, to solve complex problems that are too large or time-consuming for standard computers. **Each cluster consists of multiple computers** (or nodes) working together to process large volumes of data, making tasks like simulations, data analysis, and scientific research much faster. In fields like healthcare, finance, and engineering, HPC accelerates innovation by allowing researchers and businesses to tackle large-scale challenges efficiently.
	
	The importance of HPC lies in its ability to significantly reduce the time it takes to process and analyze data, enabling faster discoveries, better decision-making, and the advancement of technology across various industries. By using cloud-based HPC solutions like AWS, Azure and Google Cloud, organizations can scale resources as needed, cutting costs and improving performance.

  **Example**: Simulating weather patterns using supercomputers to predict climate changes.

  - *Resource*: [What is High Performance Computing?](https://www.youtube.com/watch?v=nIBu1EFYmBU) (YouTube)

- **Python in HPC**

  **Definition**: Python is a versatile programming language widely used in HPC due to its simplicity and the availability of numerous libraries that support parallel computing.

  **Example**: Using Python's `multiprocessing` library to perform large-scale data analysis across multiple CPU cores.

  - *Resource*: [Python in High Performance Computing](https://www.researchgate.net/publication/280096197_Python_in_High_Performance_Computing) (Article)

### **1.2 Challenges and Limitations**

- **Global Interpreter Lock (GIL)**

  **Definition**: The Global Interpreter Lock (GIL) is a **mutex** in the CPython interpreter that prevents multiple native threads from executing Python **bytecodes** at once.

  **Example**: When using threads in Python, the GIL can become a bottleneck because it forces threads to execute one at a time, limiting concurrency.

  - *Resource*: [Understanding the Python GIL](https://realpython.com/python-gil/) (Article)

- **CPU-bound vs. I/O-bound Tasks**

  **Definition**:
  - **CPU-bound**: Tasks that require heavy computation and use significant CPU resources.
  - **I/O-bound**: Tasks that spend most of their time waiting for input/output operations.

  **Example**:
  - **CPU-bound**: Calculating large mathematical simulations.
  - **I/O-bound**: Reading and writing files to disk or network operations.

  - *Resource*: [CPU Bound vs I/O Bound Processes](https://www.youtube.com/watch?v=5eMo1koqdUI) (YouTube)

---

## **2. Python Multiprocessing**

### **2.1 Basics of Multiprocessing**

- **Introduction to Multiprocessing Module**

  **Definition**: The `multiprocessing` module allows the creation of processes, enabling true parallelism by utilizing multiple CPU cores.

  **Example**: Running multiple instances of a function simultaneously on different data subsets to speed up computation.

  ```python
  import multiprocessing

  def worker(num):
      """Function that prints the square of the given number"""
      print(f'Worker {num}: {num * num}')

  if __name__ == '__main__':
      processes = []
      for i in range(5):
          p = multiprocessing.Process(target=worker, args=(i,))
          processes.append(p)
          p.start()
  ```

  - *Resource*: [Python Multiprocessing Tutorial](https://www.youtube.com/watch?v=fKl2JW_qrso) (YouTube)

- **Process vs. Thread**

  **Definition**:
  - **Process**: An independent program in execution with its own memory space.
  - **Thread**: A sequence of execution within a process that shares the process's memory space.

  **Example**:
  - **Process**: Running a Python script that performs data analysis.
  - **Thread**: Handling multiple user requests within a web server process.

  - *Resource*: [Python Threads vs Processes](https://realpython.com/python-concurrency/) (Article)

### **2.2 Process Creation and Management**

- **Creating Processes**

  **Definition**: Using the `Process` class to create a new process that runs independently from the main program.

  **Example**:

  ```python
  from multiprocessing import Process

  def print_numbers():
      for i in range(5):
          print(i)

  if __name__ == '__main__':
      p = Process(target=print_numbers)
      p.start()
      p.join()
  ```

  - *Resource*: [Multiprocessing in Python - Creating Processes](https://www.geeksforgeeks.org/multiprocessing-python-set-1/) (Article)

- **Process Class and Arguments**

  **Definition**: Passing arguments to processes using the `args` parameter of the `Process` class.

  **Example**:

  ```python
  from multiprocessing import Process

  def multiply(a, b):
      print(f'{a} * {b} = {a * b}')

  if __name__ == '__main__':
      p = Process(target=multiply, args=(5, 7))
      p.start()
      p.join()
  ```

  - *Resource*: [Python Multiprocessing: Process Class](https://docs.python.org/3/library/multiprocessing.html#the-process-class) (Official Documentation)

### **2.3 Using Pools for Parallel Tasks**

- **Pool Class and Map Function**

  **Definition**: The `Pool` class provides a convenient way to parallelize execution of a function across multiple input values using a pool of processes.

  **Example**:

  ```python
  from multiprocessing import Pool

  def square(x):
      return x * x

  if __name__ == '__main__':
      with Pool(4) as p:
          result = p.map(square, [1, 2, 3, 4, 5])
      print(result)  # Output: [1, 4, 9, 16, 25]
  ```

  - *Resource*: [Python Multiprocessing Pool](https://www.machinelearningplus.com/python/parallel-processing-python/) (Article)

- **Asynchronous Execution with Pools**

  **Definition**: Running tasks asynchronously using `apply_async`, which allows other processes to proceed without waiting for the result.

  **Example**:

  ```python
  from multiprocessing import Pool

  def compute_factorial(n):
      import math
      return math.factorial(n)

  if __name__ == '__main__':
      with Pool(3) as p:
          results = [p.apply_async(compute_factorial, args=(i,)) for i in range(5, 10)]
          output = [r.get() for r in results]
      print(output)  # Output: [120, 720, 5040, 40320, 362880]
  ```

  - *Resource*: [Asynchronous Task Execution](https://superfastpython.com/multiprocessing-pool-apply-async/) (Article)

### **2.4 Interprocess Communication**

- **Queues and Pipes**

  **Definition**:
  - **Queue**: A thread and process-safe FIFO implementation that can be used for interprocess communication.
  - **Pipe**: A unidirectional or bidirectional communication channel between two processes.

  **Example**:

  ```python
  from multiprocessing import Process, Queue

  def producer(q):
      q.put('Hello')

  def consumer(q):
      msg = q.get()
      print(msg)

  if __name__ == '__main__':
      q = Queue()
      p1 = Process(target=producer, args=(q,))
      p2 = Process(target=consumer, args=(q,))
      p1.start()
      p2.start()
      p1.join()
      p2.join()
  ```

  - *Resource*: [Interprocess Communication using Queues and Pipes](https://www.youtube.com/watch?v=WBp7-JAcPyo) (YouTube)

- **Shared Memory Objects**

  **Definition**: Objects like `Value` and `Array` that can be shared between processes.

  **Example**:

  ```python
  from multiprocessing import Process, Value, Array

  def increment(n, shared_value, shared_array):
      n.value += 1
      for i in range(len(shared_array)):
          shared_array[i] += 1

  if __name__ == '__main__':
      num = Value('i', 0)
      arr = Array('i', [1, 2, 3])
      p = Process(target=increment, args=(num, arr))
      p.start()
      p.join()
      print(num.value)       # Output: 1
      print(arr[:])          # Output: [2, 3, 4]
  ```

  - *Resource*: [Sharing State Between Processes](https://docs.python.org/3/library/multiprocessing.html#sharing-state-between-processes) (Official Documentation)

### **2.5 Synchronization Primitives**

- **Locks, Semaphores, Events**

  **Definition**:
  - **Lock**: A synchronization primitive that allows only one process to access a resource at a time.
  - **Semaphore**: A variable used to control access to a common resource by multiple processes.
  - **Event**: A flag used for communication between processes.

  **Example (Using Lock)**:

  ```python
  from multiprocessing import Process, Lock

  def printer(item, lock):
      with lock:
          print(item)

  if __name__ == '__main__':
      lock = Lock()
      items = ['apple', 'banana', 'cherry']
      processes = [Process(target=printer, args=(item, lock)) for item in items]
      for p in processes:
          p.start()
      for p in processes:
          p.join()
  ```

  - *Resource*: [Synchronization Between Processes](https://pymotw.com/3/multiprocessing/communication.html) (Article)

- **Preventing Race Conditions**

  **Definition**: A race condition occurs when multiple processes access and modify shared data concurrently, leading to unpredictable results.

  **Example**: Without locks, two processes incrementing a shared counter might interfere, causing incorrect counts.

  - *Resource*: [Understanding Race Conditions](https://www.geeksforgeeks.org/race-condition-in-processes/) (Article)

---

## **3. Advanced Parallel Computing Techniques**

### **3.1 Multithreading in Python**

- **Threading Module Overview**

  **Definition**: The `threading` module provides a way to create and manage threads in Python.

  **Example**:

  ```python
  import threading

  def worker():
      print('Worker thread is running')

  t = threading.Thread(target=worker)
  t.start()
  t.join()
  ```

  - *Resource*: [Python Threading Tutorial](https://realpython.com/intro-to-python-threading/) (Article)

- **When to Use Threads vs. Processes**

  **Definition**:
  - **Threads**: Best for I/O-bound tasks due to lower overhead and shared memory.
  - **Processes**: Better for CPU-bound tasks as they bypass the GIL.

  **Example**: Using threads for handling multiple client connections in a server, processes for performing heavy computations.

  - *Resource*: [Threads vs Processes in Python](https://www.youtube.com/watch?v=LUjEX4ZsZ6o) (YouTube)

### **3.2 Asynchronous Programming**

- **Asyncio Library**

  **Definition**: The `asyncio` library provides infrastructure for writing single-threaded concurrent code using coroutines.

  **Example**:

  ```python
  import asyncio

  async def fetch_data():
      print('Start fetching')
      await asyncio.sleep(2)
      print('Done fetching')
      return {'data': 1}

  async def main():
      data = await fetch_data()
      print(data)

  asyncio.run(main())
  ```

  - *Resource*: [Async IO in Python: A Complete Walkthrough](https://realpython.com/async-io-python/) (Article)

- **Coroutines and Event Loops**

  **Definition**:
  - **Coroutine**: A function declared with `async def` that can `await` on other coroutines.
  - **Event Loop**: Manages and distributes the execution of different coroutines.

  **Example**: The `main()` function above is a coroutine that runs within an event loop.

  - *Resource*: [Understanding Python Coroutines](https://www.youtube.com/watch?v=ZzfHjytDceU) (YouTube)

### **3.3 Distributed Computing**

- **Using Dask for Parallel Computing**

  **Definition**: Dask is a flexible parallel computing library for analytics that integrates with existing Python tools.

  **Example**:

  ```python
  import dask.array as da

  x = da.random.random((10000, 10000), chunks=(1000, 1000))
  y = x + x.T
  z = y.mean(axis=0)
  result = z.compute()
  ```

  - *Resource*: [Dask Tutorial](https://www.youtube.com/watch?v=RA_2qdipVng) (YouTube)

- **Apache Spark with PySpark**

  **Definition**: PySpark allows you to use Apache Spark with Python, enabling large-scale data processing.

  **Example**:

  ```python
  from pyspark.sql import SparkSession

  spark = SparkSession.builder.appName('Example').getOrCreate()
  df = spark.read.csv('data.csv', header=True)
  df = df.groupBy('category').count()
  df.show()
  ```

  - *Resource*: [PySpark Tutorial for Beginners](https://www.youtube.com/watch?v=3rzGRt3xZjY) (YouTube)

### **3.4 GPU Computing**

- **Numba and CUDA**

  **Definition**: Numba is a JIT compiler that translates Python functions to optimized machine code using LLVM. It can target CUDA GPUs.

  **Example**:

  ```python
  from numba import cuda

  @cuda.jit
  def vector_add(a, b, c):
      idx = cuda.grid(1)
      if idx < a.size:
          c[idx] = a[idx] + b[idx]

  import numpy as np

  n = 1000000
  a = np.ones(n, dtype=np.float32)
  b = np.ones(n, dtype=np.float32)
  c = np.zeros(n, dtype=np.float32)

  threadsperblock = 256
  blockspergrid = (a.size + (threadsperblock - 1)) // threadsperblock

  vector_add[blockspergrid, threadsperblock](a, b, c)
  ```

  - *Resource*: [Getting Started with Numba and CUDA](https://numba.pydata.org/numba-doc/latest/cuda/index.html) (Official Documentation)

- **TensorFlow and GPU Acceleration**

  **Definition**: TensorFlow is an end-to-end open-source platform for machine learning that can utilize GPUs for acceleration.

  **Example**:

  ```python
  import tensorflow as tf

  with tf.device('/GPU:0'):
      a = tf.constant([[1.0, 2.0], [3.0, 4.0]])
      b = tf.constant([[1.0, 1.0], [0.0, 1.0]])
      c = tf.matmul(a, b)
      print(c)
  ```

  - *Resource*: [TensorFlow with GPU Support](https://www.tensorflow.org/install/gpu) (Official Documentation)

---

## **4. Optimizing Python Code for Performance**

### **4.1 Profiling and Benchmarking**

- **Using cProfile and timeit**

  **Definition**:
  - **cProfile**: A profiler that records the time spent in each function.
  - **timeit**: A module to measure execution time of small code snippets.

  **Example (Using timeit)**:

  ```python
  import timeit

  setup_code = 'import math'
  stmt = 'math.sqrt(12345)'
  execution_time = timeit.timeit(stmt, setup=setup_code, number=100000)
  print(execution_time)
  ```

  - *Resource*: [Python Performance Profiling](https://realpython.com/python-performance-tuning/) (Article)

- **Identifying Bottlenecks**

  **Definition**: Finding sections of code that are slowing down the program.

  **Example**: Using cProfile to see which functions take the most time.

  ```python
  import cProfile

  def slow_function():
      for i in range(1000000):
          pass

  cProfile.run('slow_function()')
  ```

  - *Resource*: [Profiling Python Code](https://www.youtube.com/watch?v=_O2B8pvgFII) (YouTube)

### **4.2 Efficient Data Structures**

- **Choosing the Right Data Structures**

  **Definition**: Using data structures that provide optimal performance for the required operations.

  **Example**: Using a `set` for membership tests instead of a `list`.

  ```python
  items_list = [1, 2, 3, 4, 5]
  items_set = {1, 2, 3, 4, 5}

  # Membership test
  3 in items_list  # Slower
  3 in items_set   # Faster
  ```

  - *Resource*: [Data Structures in Python](https://realpython.com/python-data-structures/) (Article)

- **Using Arrays and Memory Views**

  **Definition**: Arrays provide more efficient storage and faster access compared to lists for numerical data.

  **Example**:

  ```python
  import array

  arr = array.array('i', [1, 2, 3, 4, 5])
  ```

  - *Resource*: [High Performance Arrays in Python with NumPy](https://www.youtube.com/watch?v=QUT1VHiLmmI) (YouTube)

### **4.3 Just-In-Time Compilation**

- **Using Numba for JIT Compilation**

  **Definition**: Numba compiles Python functions to optimized machine code at runtime, improving performance.

  **Example**:

  ```python
  from numba import njit
  import numpy as np

  @njit
  def sum_array(arr):
      total = 0
      for i in arr:
          total += i
      return total

  arr = np.arange(1000000)
  print(sum_array(arr))
  ```

  - *Resource*: [Accelerate Python with Numba](https://www.youtube.com/watch?v=GFX4EW7N5bw) (YouTube)

- **Cython for Compiling Python Code**

  **Definition**: Cython is a superset of Python that allows you to compile Python code to C for performance gains.

  **Example**:

  ```cython
  def sum_array(int[:] arr):
      cdef int total = 0
      for i in arr:
          total += i
      return total
  ```

  - *Resource*: [Cython Tutorial](https://cython.readthedocs.io/en/latest/src/tutorial/index.html) (Official Documentation)

### **4.4 Parallelizing Code**

- **Multiprocessing vs. Multithreading**

  **Definition**:
  - **Multiprocessing**: Using multiple processes to execute code in parallel.
  - **Multithreading**: Using multiple threads within a single process.

  **Example**: Using `multiprocessing` for CPU-bound tasks, `threading` for I/O-bound tasks.

  - *Resource*: [Parallelization in Python](https://realpython.com/python-concurrency/) (Article)

- **Vectorization with NumPy**

  **Definition**: Writing code that operates on arrays without explicit loops, leveraging optimized C libraries.

  **Example**:

  ```python
  import numpy as np

  arr = np.arange(1000000)
  result = arr * 2  # Vectorized operation
  ```

  - *Resource*: [Writing Fast NumPy Code](https://www.youtube.com/watch?v=EEUXKG97YRw) (YouTube)

---

## **5. Practical Applications and Examples**

### **5.1 Scientific Computing**

- **Simulations and Modeling**

  **Definition**: Using computational methods to simulate physical systems.

  **Example**: Simulating particle interactions in physics using Python and HPC techniques.

  - *Resource*: [Python for Scientific Computing](https://www.scipy-lectures.org/) (Article)

- **Using SciPy and NumPy**

  **Definition**: SciPy and NumPy are libraries for numerical computations.

  **Example**:

  ```python
  import numpy as np
  from scipy import integrate

  def f(x):
      return x ** 2

  result = integrate.quad(f, 0, 10)
  print(result)
  ```

  - *Resource*: [NumPy and SciPy Tutorial](https://www.youtube.com/watch?v=GB9ByFAIAH4) (YouTube)

### **5.2 Data Processing and Analysis**

- **Pandas for Data Manipulation**

  **Definition**: Pandas is a library providing high-performance data structures and data analysis tools.

  **Example**:

  ```python
  import pandas as pd

  df = pd.read_csv('data.csv')
  df = df[df['age'] > 30]
  df.to_csv('filtered_data.csv')
  ```

  - *Resource*: [Fast Data Processing with Pandas](https://realpython.com/pandas-python-explore-dataset/) (Article)

- **Optimizing Data Pipelines**

  **Definition**: Improving data processing workflows for efficiency and scalability.

  **Example**: Using chunking in Pandas to process large datasets without loading them entirely into memory.

  ```python
  import pandas as pd

  chunks = pd.read_csv('large_data.csv', chunksize=100000)
  for chunk in chunks:
      process(chunk)
  ```

  - *Resource*: [Building Efficient Data Pipelines](https://www.youtube.com/watch?v=KzmeSNgkG_M) (YouTube)

### **5.3 Machine Learning and AI**

- **Training Models Efficiently**

  **Definition**: Utilizing HPC techniques to speed up the training of machine learning models.

  **Example**: Parallelizing hyperparameter tuning using multiprocessing.

  ```python
  from sklearn.model_selection import GridSearchCV
  from sklearn.svm import SVC

  param_grid = {'C': [1, 10], 'kernel': ['linear', 'rbf']}
  grid = GridSearchCV(SVC(), param_grid, n_jobs=-1)
  grid.fit(X_train, y_train)
  ```

  - *Resource*: [High Performance Machine Learning in Python](https://www.youtube.com/watch?v=Gj0iyo265bc) (YouTube)

- **Parallel Processing in Scikit-Learn**

  **Definition**: Scikit-Learn supports parallel execution of certain operations using the `n_jobs` parameter.

  **Example**:

  ```python
  from sklearn.ensemble import RandomForestClassifier

  clf = RandomForestClassifier(n_estimators=100, n_jobs=-1)
  clf.fit(X_train, y_train)
  ```

  - *Resource*: [Parallelism in Scikit-Learn](https://scikit-learn.org/stable/computing/parallelism.html) (Official Documentation)

---

## **6. Tools and Libraries for HPC in Python**

### **6.1 Multiprocessing and Threading Libraries**

- **Concurrent.futures Module**

  **Definition**: A high-level interface for asynchronously executing callables using threads or processes.

  **Example**:

  ```python
  from concurrent.futures import ProcessPoolExecutor

  def task(n):
      return n * n

  with ProcessPoolExecutor() as executor:
      results = executor.map(task, range(10))
  print(list(results))
  ```

  - *Resource*: [Concurrent Futures in Python](https://docs.python.org/3/library/concurrent.futures.html) (Official Documentation)

- **Joblib for Easy Parallel Computing**

  **Definition**: Joblib is a set of tools to provide lightweight pipelining in Python, particularly for machine learning.

  **Example**:

  ```python
  from joblib import Parallel, delayed

  def task(n):
      return n * n

  results = Parallel(n_jobs=4)(delayed(task)(i) for i in range(10))
  print(results)
  ```

  - *Resource*: [Parallel Processing with Joblib](https://joblib.readthedocs.io/en/latest/) (Official Documentation)

### **6.2 HPC Libraries**

- **MPI for Python (mpi4py)**

  **Definition**: MPI for Python provides bindings for the Message Passing Interface (MPI) standard, enabling parallel computing across multiple nodes.

  **Example**:

  ```python
  from mpi4py import MPI

  comm = MPI.COMM_WORLD
  rank = comm.Get_rank()

  print(f'Hello from process {rank}')
  ```

  - *Resource*: [mpi4py Tutorial](https://mpi4py.readthedocs.io/en/stable/tutorial.html) (Official Documentation)

- **Ray for Distributed Computing**

  **Definition**: Ray is a framework for building and running distributed applications.

  **Example**:

  ```python
  import ray

  ray.init()

  @ray.remote
  def f(x):
      return x * x

  futures = [f.remote(i) for i in range(4)]
  print(ray.get(futures))
  ```

  - *Resource*: [Ray: A Fast and Simple Framework for Building and Running Distributed Applications](https://www.youtube.com/watch?v=6UvX8J1N82I) (YouTube)

### **6.3 Profiling and Optimization Tools**

- **Line Profiler and Memory Profiler**

  **Definition**:
  - **Line Profiler**: Profiles the time spent on each line of code.
  - **Memory Profiler**: Monitors memory consumption of a Python program.

  **Example (Using Memory Profiler)**:

  ```python
  @profile
  def my_func():
      a = [1] * (10 ** 6)
      b = [2] * (2 * 10 ** 7)
      del b
      return a

  if __name__ == '__main__':
      my_func()
  ```

  - *Resource*: [Profiling Memory Usage in Python](https://www.youtube.com/watch?v=9LV6lqXvQIo) (YouTube)

- **PyPy for Speed Improvements**

  **Definition**: PyPy is an alternative implementation of Python that features a Just-In-Time compiler, resulting in significant speed improvements.

  **Example**: Running your Python script with PyPy instead of CPython can result in faster execution times without changing the code.

  - *Resource*: [PyPy - A Faster Python Implementation](https://www.pypy.org/) (Official Website)

---

## **7. Best Practices and Tips**

### **7.1 Writing Efficient Python Code**

- **Code Optimization Techniques**

  **Definition**: Strategies to make code run faster and use fewer resources.

  **Example**: Avoiding unnecessary computations, using built-in functions, and efficient looping.

  ```python
  # Inefficient
  result = []
  for i in range(len(items)):
      result.append(items[i] * 2)

  # Efficient
  result = [item * 2 for item in items]
  ```

  - *Resource*: [Writing Efficient Python Code](https://realpython.com/python-code-optimization/) (Article)

- **Avoiding Common Pitfalls**

  **Definition**: Being aware of practices that can degrade performance.

  **Example**: Using global variables excessively or neglecting to close file handles.

  - *Resource*: [Common Performance Pitfalls in Python](https://www.youtube.com/watch?v=YjHsOrOOSuI) (YouTube)

### **7.2 Testing and Debugging in Parallel Computing**

- **Debugging Parallel Programs**

  **Definition**: Techniques to identify and fix issues in code that runs concurrently.

  **Example**: Using logging instead of print statements to trace execution in multiprocessing code.

  ```python
  import logging
  logging.basicConfig(level=logging.DEBUG, format='%(processName)s:%(message)s')
  ```

  - *Resource*: [Debugging Multiprocessing Code](https://stackoverflow.com/questions/20083587/how-to-debug-a-python-multiprocessing-application) (StackOverflow)

- **Ensuring Correctness and Reproducibility**

  **Definition**: Making sure that parallel programs produce the correct results consistently.

  **Example**: Setting random seeds and using locks to prevent race conditions.

  - *Resource*: [Testing Parallel Python Applications](https://semaphoreci.com/community/tutorials/testing-python-applications-with-pytest) (Article)

---

## **8. Latest Books on High Performance Computing with Python**

1. **"High Performance Python: Practical Performant Programming for Humans"** by Micha Gorelick and Ian Ozsvald (2nd Edition, 2020)
   - *Description*: This book provides practical techniques for optimizing Python code, including profiling, understanding performance bottlenecks, and using concurrency.

2. **"Parallel and High Performance Computing"** by Robert Robey and Yuliana Zamora (2021)
   - *Description*: Covers the fundamentals of parallel computing, including threading, multiprocessing, and GPU computing, with Python examples.

3. **"Mastering Concurrency in Python"** by Quan Nguyen (2018)
   - *Description*: Although not the latest, it offers insights into concurrent programming techniques in Python, including threading, multiprocessing, and asyncio.

4. **"Effective Python: 90 Specific Ways to Write Better Python"** by Brett Slatkin (2nd Edition, 2019)
   - *Description*: Provides tips and best practices for writing efficient and effective Python code, including sections on concurrency and performance.

5. **"Hands-On GPU Computing with Python"** by Avimanyu Bandyopadhyay (2019)
   - *Description*: Explores GPU computing concepts and how to implement them using Python libraries like Numba and CuPy.

---

# Mock Exam – Student API Documentation

---

## Workflow 1: Upload and Process Exam Answer Images

### Purpose

Allow students to upload images of their exam answers. The system performs OCR (Optical Character Recognition) to extract text and separates it into question-answer pairs, which are then stored in the database linked to the respective user, course, exam, and question paper.

### Endpoint

`POST /upload-exam-answers`

### How It Works

1. **Image Upload**: Students upload images of their exam answers.
2. **OCR Processing**: The system extracts text from the images using OCR.
3. **Question-Answer Extraction**: Extracted text is analyzed to identify question numbers and corresponding answers.
4. **Data Storage**: Question-answer pairs are saved in the database, linked to the student and relevant exam details.

### Request Body

- **User Information**:
  - `user_id`: String
- **Course and Exam Information**:
  - `course_code`: String
  - `exam_code`: String
  - `question_paper_code`: String
- **Images**:
  - `images`: Array of image objects
    - `image_id`: String
    - `image_url`: String

**Example**

```json
{
  "user_id": "USER123",
  "course_code": "CA-FND-2024",
  "exam_code": "CA-FO-PAPER1",
  "question_paper_code": "QP001",
  "images": [
    {
      "image_id": "img_1",
      "image_url": "https://example.com/image1.jpg"
    },
    {
      "image_id": "img_2",
      "image_url": "https://example.com/image2.jpg"
    }
  ]
}
```

### Response

- **Status**: Success or failure of the operation.
- **Extracted Text**: Combined text extracted from all images.
- **Question-Answer Pairs**: Array of extracted question-answer pairs.
- **Message**: Confirmation or error message.

**Example**

```json
{
  "status": "success",
  "user_id": "USER123",
  "course_code": "CA-FND-2024",
  "exam_code": "CA-FO-PAPER1",
  "question_paper_code": "QP001",
  "extracted_text": "The going concern concept assumes a business will continue to operate indefinitely...", // Combined Extracted Text
  "qa_pairs": [
    {
      "question_number": "1.a",
      "answer": "The going concern concept assumes that a business will continue to operate indefinitely."
    },
    {
      "question_number": "1.b",
      "answer": "The accounting equation is Assets = Liabilities + Capital."
    }
    // Additional question-answer pairs
  ],
  "message": "Question-answer pairs extracted and saved successfully."
}
```

---

## Workflow 2: Evaluate Question-Answer Pairs

### Purpose

Evaluate the student's answers by comparing them with standard answers stored in the database using Large Language Models (LLMs). Assign marks based on the evaluation and provide feedback.

### Endpoint

`POST /evaluate-answers`

### How It Works

1. **Data Retrieval**: The system retrieves question-answer pairs, standard answers, and total marks for each question.
2. **Evaluation Process**:
   - **LLM1**: Evaluates the student's answer against the standard answer.
   - **LLM2**: Verifies LLM1's evaluation for accuracy.
   - **LLM3**: If discrepancies are found, re-evaluates and provides a final assessment.
3. **Mark Assignment**: Assign marks to each question based on the evaluation.
4. **Result Compilation**: Compile final marks and feedback.
5. **Data Storage**: Save evaluation results in the database and return them to the client.

### Request Body

- **User Information**:
  - `user_id`: String
- **Course and Exam Information**:
  - `course_code`: String
  - `exam_code`: String
  - `question_paper_code`: String
- **Question-Answer Pairs**:
  - `qa_pairs`: Array of objects
    - `question_number`: String
    - `student_answer`: String
    - `standard_answer`: String
    - `total_marks`: Integer

**Example**

```json
{
  "user_id": "USER123",
  "course_code": "CA-FND-2024",
  "exam_code": "CA-FO-PAPER1",
  "question_paper_code": "QP001",
  "qa_pairs": [
    {
      "question_number": "1.a",
      "student_answer": "FastAPI is a modern, fast web framework.",
      "standard_answer": "FastAPI is a high-performance web framework for building APIs.",
      "total_marks": 10
    },
    {
      "question_number": "1.b",
      "student_answer": "OCR is Optical Character Recognition.",
      "standard_answer": "OCR is a technology that converts different types of documents into editable data.",
      "total_marks": 10
    }
  ]
}
```

### Response

- **Status**: Success or failure of the evaluation.
- **Evaluation Results**: Array containing detailed evaluations for each question.
- **Final Score**: Total marks awarded.
- **Message**: Confirmation or error message.

**Example**

```json
{
  "status": "success",
  "user_id": "USER123",
  "course_code": "CA-FND-2024",
  "exam_code": "CA-FO-PAPER1",
  "question_paper_code": "QP001",
  "total_exam_marks": 100,
  "evaluation": [
    {
      "question_number": "1.a",
      "llm_evaluation": "The student's answer closely matches the standard answer.",
      "marks_awarded": 9,
      "total_marks": 10
    },
    {
      "question_number": "1.b",
      "llm_evaluation": "The student's answer is partially correct but lacks detail.",
      "marks_awarded": 6,
      "total_marks": 10
    }
    // Additional evaluations
  ],
  "final_score": 15,
  "message": "Evaluations completed and results returned."
}
```

---

## Probable NoSQL Database Schema

### Collections

1. **Users**

   - `user_id`: String (Primary Key)
   - `name`: String
   - `email`: String
   - // Additional user details

2. **Courses**

   - `course_code`: String (Primary Key)
   - `course_name`: String
   - // Additional course details

3. **Exams**

   - `exam_code`: String (Primary Key)
   - `course_code`: String (Foreign Key)
   - `exam_name`: String
   - `total_exam_marks`: Integer
   - // Additional exam details

4. **QuestionPapers**

   - `question_paper_code`: String (Primary Key)
   - `exam_code`: String (Foreign Key)
   - `questions`: Array of objects
     - `question_number`: String
     - `standard_answer`: String
     - `total_marks`: Integer

5. **StudentAnswers**

   - `user_id`: String (Foreign Key)
   - `course_code`: String
   - `exam_code`: String
   - `question_paper_code`: String
   - `qa_pairs`: Array of objects
     - `question_number`: String
     - `student_answer`: String
     - `extracted_text`: String
     - `marks_awarded`: Integer
     - `total_marks`: Integer
     - `llm_evaluation`: String

---