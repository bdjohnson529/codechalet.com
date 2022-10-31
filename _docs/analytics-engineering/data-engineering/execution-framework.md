---
layout: blog
title: Structuring Jobs
order: 1
topic: Analytics Engineering
topic_path: /docs/analytics-engineering/index.html
---
This style guide introduces a framework for structuring production batch data processing jobs. I tried to keep the framework general so it would remain relevant for different programming languages.

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