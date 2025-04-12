Multi-Level Capacitated Lot Sizing Problem (MLCLSP) Solver

This repository contains a Python implementation for solving the Multi-Level Capacitated Lot Sizing Problem (MLCLSP). The problem is typically used in manufacturing and supply chain optimization to manage inventory and production schedules considering resource constraints, setup costs, and lead times.

Problem Description

The MLCLSP involves determining the optimal production schedule for multiple items over multiple periods, subject to the following constraints:

Inventory Balance: Maintaining appropriate inventory levels across periods.

Production Capacity: Ensuring production does not exceed available resource capacities.

Setup Costs: Minimizing setup costs when switching between items.

Lead Time: Considering lead time requirements for each item.

Batching Approach: Production is scheduled in batches, and setup is required for each machine/resource.

The problem is formulated as a Mixed-Integer Linear Programming (MILP) model, and it is solved using the Gurobi Optimizer.

How to Run

Prerequisites

To run this code, you need the following dependencies:

Gurobi Optimizer: A commercial solver for optimization problems.

Python 3.x: The implementation is compatible with Python 3.x.

Gurobi Python Interface: Ensure you have the Gurobi Python interface installed (refer to Gurobi documentation).

Input Data Files

This implementation reads test instances from .dat files, where each file represents a different test case (A, B, C, D). The input files contain the following parameters:

Model name: The name of the model.

Number of periods: The number of time periods over which the production schedule is planned.

Number of items: The number of items to be produced.

Number of resources: The number of resources available for production.

Setup cost: The cost associated with setting up each item.

Holding cost: The cost associated with holding inventory.

Lead time: The required time to produce each item.

Initial inventory: The starting inventory for each item.

Bill of Materials (BOM): A matrix representing the required number of each item to produce another item.

External demand: The demand for each item in each period.

Capacity limits: The capacity limits of each resource in each period.

Overtime costs: The overtime costs associated with using resources beyond normal capacity.

The code will prompt you to select the test instance (A, B, C, or D) and load the respective file for the calculation.

Running the Code

To run the code, simply execute the script main.py:

The program will prompt you for a test instance (A, B, C, or D) and will then solve the optimization problem for the selected data. The solution is outputted by Gurobi, and it provides the optimal production and inventory schedule for the given instance.

Code Explanation

Data Parsing: The code starts by parsing the input .dat files containing various parameters needed for the MLCLSP model. It reads the data from the selected file and stores the parameters (like setup costs, inventory, demand, etc.) for further use in the optimization model.

Optimization Model: The problem is formulated as a MILP using the gurobipy library. The decision variables include:

Inventory: Inventory levels of each item across periods.

Production: Production quantities of each item in each period.

Production period binary variables: Whether or not a production period is used for an item.

Start time: The start time for producing an item in each period.

Successor production amount: The amount produced by the successor item.

Setup binary variables: Whether a machine setup is needed for a given item.

Changeover binary variables: Whether a changeover is needed between two items.

The objective is to minimize the total cost, which consists of:

Holding cost for inventory.

Setup cost for switching between items.

Constraints: The model includes several constraints:

Inventory balance: Ensures that inventory levels are maintained from one period to the next.

Production capacity: Ensures that production does not exceed the available resource capacities.

Machine setup: Ensures that there is exactly one setup per machine per period.

Setup state conservation: Ensures that setup states are carried over across periods.

Linked start and finish times for batches: Ensures that batches are produced in sequence.

Solution: The model is solved using Gurobi, which finds the optimal values for all decision variables. The result includes the optimal production schedule, inventory levels, and setup configurations.

License

This project is licensed under the MIT License - see the LICENSE file for details.
