---
title: How to Use FastDOG - a Highly Parallelised ILP Solver
author: me
date: 2024-01-15 11:33:00 +0800
categories: [Blog, Python]
tags: [python]
pin: false
math: false
mermaid: false
---

# 🐶 How to Use FastDOG - a Highly Parallelised ILP Solver

![Desktop View](/assets/img/posts/fastdog/fastdog.png){: width="300" height="730" }

In one of our recent [papers](https://arxiv.org/abs/2310.08230) we use and adapt FastDOG ([paper](https://arxiv.org/abs/2111.10270), [code](https://github.com/LPMP/BDD)) solver with which _large binary integer linear programs_ (ILPs) can be solved. Key features of the solver are:
- computing lower bounds for ILPs
- compute a (not necessarily the globally optimal) primal feasible solution
- CPU, multicore CPU as well as GPU support (highly parallised!)
- faster convergence speeds for general problem classes through second order information, i.e. LBFGS updates (contribution of our [paper](https://arxiv.org/abs/2310.08230))

In this blog post we learn how to install and use the solver through its python bindings.

## ⚙️ Installation

1) (Optional but highly recommended) Create python virtual environment
```bash
conda create -n ilp_solver python=3.8 # create new virtual environment
conda activate ilp_solver
```

2) Install FastDog python bindings
```bash
git clone git@github.com:LPMP/BDD.git
cd BDD
python setup.py install
cd ..
```

### 🚧 Troubleshooting (incomplete list)
- No CUDA available on your system: change `'-DWITH_CUDA=ON'` to `'-DWITH_CUDA=OFF'` and install via `python setup.py install` Note: you have to change the options to `opts.bdd_solver_type = bdd_solver_options.bdd_solver_types.lbfgs_parallel_mma`
- Unsupported gpu archtiecture `compute native`: Make sure your cmake version is larger than 3.25. Through `conda upgrade conda install -c anaconda cmake`
- Missing `CUDA_INCLUDE_DIRS` when installing the solver: Install latest cuda toolkit AND PERFORM POST-INSTALLATION ACTIONS: `export PATH=/usr/local/cuda-12.2/bin${PATH:+:${PATH}}`
- (Last Resort and kind of a hack) Missing `CUDA_INCLUDE_DIRS` when installing the solver: Manually set the cuda variables for cmake ie add the following lines in `BDD/setup.py`
```python
cmake_args = [...
              '-DWITH_CUDA=ON',
              ### start of added lines, ADJUST THE PATH TO CUDA AS ON YOUR OWN SYSTEM
              '-DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.7/bin/nvcc',
              '-DCUDA_NVCC_EXECUTABLE=/usr/local/cuda-11.7/bin/nvcc'
              ### end of added lines
            ]
```

If you find troubles installing and furthermore a fix for that feel free to contact me so I can add it to this list 👍

## 🚀 Using FastDOG 🐶

Once you have successfully installed the solver into your virtual environment we can start discussing how to use the solver. Generally, the solver can solve problems of the following form
```
min 1 * x_1 + 2 * x_2
subject to
x_1, x_2 binary
A x <= b
```

### Basics

A basic example which is the simplified version of [this](https://github.com/LPMP/BDD/blob/main/test/test_bdd_solver_py.py).
```python
import BDD.ILP_instance_py as ilp_instance
from BDD.bdd_solver_py import bdd_solver as bdd_solver
from BDD.bdd_solver_py import bdd_solver_options as bdd_solver_options
import numpy as np

# Function to create a so-called ilp-instance which can be passed onto the solver
def create_toy_problem():
    objective = {'x1': 2.0, 'x2': 1.0, 'x3': -1.0, 'x4': 1.0, 'x5': -2.0, 'x6': -5.0}
    constraints = [
        ['C1', {'x1': 1.0, 'x2': 1.0, 'x3': 1.0}, '=', 1.0],
        ['C2', {'x3': 1.0, 'x4': 1.0, 'x5': 1.0}, '<', 1.0],
        ['C3', {'x4': 1.0, 'x5': 1.0, 'x6': 1.0}, '>', 1.0]
    ]
    ilp = ilp_instance.ILP_instance()
    for var_name, coeff in objective.items():
        ilp.add_new_variable_with_obj(var_name, coeff)

    for con in constraints:
        con_name = con[0]
        con_vars = list(con[1].keys())
        con_coeffs = list(con[1].values())
        con_coeffs = [int(c) for c in con_coeffs] # Only integer coefficients are supported.
        con_sense = con[2]
        rhs_value = int(con[3]) # Only integer right hand side value is supported.
        if con_sense == '=':
            ineq_type = ilp_instance.equal
        elif con_sense == '<':
            ineq_type = ilp_instance.smaller_equal
        else:
            assert(con_sense == '>')
            ineq_type = ilp_instance.greater_equal
        ilp.add_new_constraint(con_name, con_vars, con_coeffs, rhs_value, ineq_type)
    return ilp

# creating an optimisation problem
ilp = create_toy_problem()

# passing ilp instance to solver options
opts = bdd_solver_options(ilp)

# this setting enables finding a primal feasible solution. If this is false only a lower bound will be computed.
opts.incremental_primal_rounding = True

# initialize solver
solver = bdd_solver(opts)

# solve dual problem
solver.solve_dual()
lower_bound = solver.lower_bound()

# run primal heuristic
upper_bound, sol = solver.round()

# extracting the solution as a numpy array
sol_numpy = np.array(sol)
```

### More Advanced

Further settings of the solver can be tweaked to extract more performance and thus faster solver times for your specific problem. If you have many of the same problem instances you might want to consider [DODGE Train](https://arxiv.org/abs/2205.11638) to tweak the parameters.
Currently available parameters are:
```python
# More general options
opts.bdd_solver_type = bdd_solver_options.bdd_solver_types.lbfgs_cuda_mma # solver types: sequential_mma, mma_cuda, parallel_mma, hybrid_parallel_mma, lbfgs_cuda_mma, lbfgs_parallel_mma, subgradient
opts.incremental_primal_rounding = True # enable for finding primal solution
opts.dual_time_limit = 3600 # time limit for solving the dual problem
opts.incremental_primal_num_rounds = 100 # maximum number of primal rounding iterations (each iteration might take some time)
opts.cuda_split_long_bdds = False # if you have very long constraints you might want to switch this on to avoid sequential bottlenecks on GPU


# More detailed parameters (solving dual problem, i.e. getting lower bound)
opts.dual_max_iter = 10000 # maximum allowed number of iterations, solver can terminate early due to convergence criteria below:
opts.dual_tolerance = 1e-9
opts.dual_improvement_slope = 1e-6

# More detailed parameters (for lbfgs solver version)
opts.lbfgs_step_size = 1e-8
opts.lbfgs_history_size = 5
opts.lbfgs_required_relative_lb_increase = 1e-6
opts.lbfgs_step_size_decrease_factor = 0.8
opts.lbfgs_step_size_increase_factor = 1.1

# More detailed parameters (primal rounding)
opts.incremental_initial_perturbation = 1.1
opts.incremental_growth_rate = 1.1
opts.incremental_primal_num_itr_lb = 100 # primal rounding will re-optimise the dual problem with at most this amount of iters


# More detailed parameters (for extremly long constraints)
opts.cuda_split_long_bdds_length = 1000

```

### More Efficient Problem Generation 
In case you want to create extremly large problem instances as we did in our shape matching [paper](https://arxiv.org/abs/2310.08230) you might actually want to create your problem (i.e. the ilp instance) in c++, write python bindings for that and return an ilp object. We did that in this [repository](https://github.com/paul0noah/sm-comb) and sketch the main steps here:
1) Create a c++ project which links to the bdd-solver repository. If you use CMAKE you would have some lines similar to this in your CMakeLists.txt file:
```python
add_subdirectory(external/BDD) # assuming you cloned git@github.com:LPMP/BDD.git into the external folder
target_include_directories(${PROJECT_NAME} PUBLIC external/BDD/include/)
target_link_libraries(${PROJECT_NAME} PUBLIC LPMP-BDD)
```

2) Write a function which creates the ILP object
A fully working example for shape matching can be found [here](https://github.com/paul0noah/sm-comb/blob/main/c%2B%2B/shapeMatchModel/shapeMatchModel.cpp#L365). Generally, the function would look sth like this:
```c++
#include <ILP_input.h>

class YourGenerator {
public:
LPMP::ILP_input getIlpObj() {
    ilp = LPMP::ILP_input();
    
    // Add variables to ilp
    for (int i = 0; i < NUM_VARIABLES; i++) {
        std::string varName = getVariableName(i);
        ilp.add_new_variable(varName);
        ilp.add_to_objective((double) getObjectiveValue(i), i);
    }
    
    // Add constraints to ilp
    for (int k = 0; k < NUM_CONSTRAINTS; ++k) {
        /*
            beginNewInequality   => creates new constraint
            inequalityIdentifier => name of the constraint e.g. R101
            inequalityType       => in this example always "="
        */
        
        ilp.begin_new_inequality();
        const std::string identifier = "R" + std::to_string(k) + " ";
        ilp.set_inequality_identifier(identifier);
        ilp.set_inequality_type(LPMP::ILP_input::inequality_type::equal);
        for (auto it: getConstraint(k) {
            const int variableCoefficient = it.value();
            const int variableIndex = it.index();
            ilp.add_to_constraint(variableCoefficient,variableCoefficient);
        }
        const int right_hand_side = 1;
        ilp.set_right_hand_side(right_hand_side);
        
    }

    return ilp;
}
}; // class YourGenerator
```

3) Write python bindings for that c++ code (we use `pybind11` for that)
Again, a fully working example for shape matching can be found [here](https://github.com/paul0noah/sm-comb/blob/main/c%2B%2B/shapeMatchModel/shapeMatchModelPB.cpp).
Basically, your python binding code has to look sth like this:
```c++
#include "YourGenerator.hpp"
#include <ILP_input.h>
#include <pybind11/pybind11.h>
#include <pybind11/stl.h>
#include <pybind11/eigen.h>


namespace py = pybind11;
using namespace pybind11::literals;  // NOLINT

PYBIND11_MODULE(your_python_bindings, handle) {
    handle.doc() = "Your Python Bindings to create an ILP Object";

    py::class_<YourGenerator, std::shared_ptr<YourGenerator>> smm(handle, "YourGenerator");
    smm.def("getIlpObj", &YourGenerator::getIlpObj);
    smm.def(py::init<>());

    // this is important so that python knows this type
    py::class_<LPMP::ILP_input>(handle, "ILP_instance")
        .def(py::init<>());
}
```

4) After compiling your python bindings (see our shape matching project for an example) you can use your generator in python 
```python
from your_python_bindings import YourGenerator

// create ilp object
generator = YourGenerator()
ilp = generator.getIlpObj()
```
