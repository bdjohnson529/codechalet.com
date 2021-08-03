---
layout: blog
title: Batch data processing
topic: data-engineering
order: 1
parent: Python
parent_path: python/
---

Batch processing is the processing of a large volume of data at the same time. Data is collected over a period of time, and then processed all at once. Batch data processing can be contrasted with real-time data processing, where data is processed as it is collected.

Most data processing jobs in the data warehouse are batch processing jobs. Unless you are working with streaming data, chances are, a large batch of data is loaded into your data warehouse for further processing. Computation resources can be optimized for batch processing jobs, for example, Spark parellelizes your code to run on large batches of data.

Most AI and ML algorithms also work with large batches of data. By nature, machine learning models are only effective when they are used with large datasets. One batch of data is used to train the model, another batch of data is used to test the model, and finally, the model is used to evaluate another batch of data.

This style guide introduces a framework for structuring production batch data processing jobs. We tried to keep the framework general so it would remain relevant for different programming languages.

# **The Framework**
With no further ado... here are some Pythonic solutions for batch data processing.

### **1. Single Point of Execution**
Batch processing jobs are going to be executed on many different computers. The entire batch processing job should be executed from a single script. Batch files are great in Windows, and shell scripts work with Linux. Throw em all in there, at the base directory of the repo.

```
run.bat
run.sh
run.py
```

The execution file should provide feedback through the console which displays errors, and confirms successful execution.

### **2. Isolated Environment**
A program should be capable of being run on different machines. Ideally, your program will be easy to execute on your local machine, a server, and your colleagues' computers. Every computer usually has different packages installed, which can lead to dependency conflicts. Each project should have an isolated execution environment, which is created by an `install.bat` file.


### **3. Self-Contained Documentation**
Documentation is contained in a folder named `docs`, and the `README.md` at the base of the repository. Documentation should include:
* Execution instructions
* Flow charts (directed acyclic graphs or other)

### **4. Stepwise Execution**
The process of building the final data model is broken out into a series of steps. We use Python to execute batches of SQL code, so there is one folder of SQL scripts and one Python script for every step of execution. Both share the same name - this naming convention improves readability significantly.


```
├── 01 Step 1
├── 02 Step 2
├── 03 Step 3
├── 01 Step 1.py
├── 02 Step 2.py
├── 03 Step 3.py
```

We use subprocess to execute each step of the build, typically in a `run.py` file.


### **6. Logs**
Logs are lovely, aren't they? Each execution step collects an execution log with relevant data. The data is saved into a `logs` folder, once again sharing the name of the associated Python script. For the above project structure, the `logs` folder might look like this:

```
01 Step 1 Log.csv
02 Step 2 Log.csv
03 Step 3 Log.csv
```

In addition, it is useful to keep an execution log which records the time taken for each step. This log can be collected in the `run.py` file. Good execution logs empower quality engineering - it becomes easy to isolate steps which are taking the longest.

### **7. Tests**
Every program should have tests which are executed at the end of the batch processing job. The tests validate the integrity of the results. At the most basic level, the tests can evaluate whether all the output tables are populated. The more specific you can make your tests, the better. **After fixing a bug, add a complementary test so that the bug is automatically caught if it reappears in the future.**

After the data build has been completed, a script responsible for testing the data model is executed. Pythonic methods of SQL execution, using templating, are described [in this blog post.](unit-testing.html)