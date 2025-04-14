---
title: How to use C++ Code in Matlab or Python
author: me
date: 2025-04-13 11:33:00 +0800
categories: [Blog, Coding]
tags: [matlab, python, C++]
pin: false
math: false
mermaid: false
---



I mostly write the core of my projects in C++ and reuse the C++ code in python or Matlab through interface code. 
In this post I'll try lay out the main points on how to do so.
In particular, I will lay out the main details of my [template repository](https://github.com/paul0noah/cpp-pybind-mex-starter).



## 🏛️ Project Structure

The template repo is structured as follows:

```bash
├── cppsrc/
├── mex/
├── pythonbinding/
├── cmake/
├── pyproject.toml
├── CMakeLists.txt
├── main.cpp
├── setup.py
├── LICENSE
└── README.md
```  


- in `cppsrc` we will put all the C++ code
- in `mex` we will put the interface code for Matlab
- in `pythonbinding` we will put the interface code for python bindings
- `cmake` contains cmake helper-files (to download pybind and libigl)


The rest are various files needed for e.g. python wrapper installation. 

💡 Note that as a build system we use `cmake` and also automatically download and include `pybind11` as well as 
`libigl` into the project (both help us to make our life easier later on). 

## 🚀 The C++ Code

In the subfolder `cppsrc` in the [template repository](https://github.com/paul0noah/cpp-pybind-mex-starter) we have 
two very basic C++ functions `myfunc1` and `myfunc2` (without a particular functionality‼️) as well as a class `MyClass` 
defined. Our goal is to wrap those for python and Matlab so that we obtain the following interfaces in the languages:


- python interface:

  ```python
  import cpppymex
  np_array_output0, np_array_output1 = cpppymex.myfunc0()
  np_array_output0, np_array_output1 = cpppymex.myfunc1(np_array_input0, "stringinput")
  
  myclass = cpppymex.MyClass("name")
  myclass.print_name()
  ```

- Matlab interface:

  ```matlab
  func_id = 0
  [array_out_0, array_out_1] = cpppymex_myfunc(func_id);
  func_id = 1
  [array_out_0, array_out_1] = cpppymex_myfunc(func_id, array_input_0, 'stringinput'); % make sure to use '' instead of "" here!
  ```

## 🐍 Writing the Python Wrapper

Writing python wrappers is suprisingly easy (as long as you are mainly dealing with numpy arrays and 
work with Eigen matrices on the C++ side). We need to touch the following things:

- we need to edit the `pythonbinding/pythonwrappers.cpp` file (we add a python module with the name 
  `cpppymex` and define two functions as well as a class as can be seen below)
  ```cpp
  PYBIND11_MODULE(cpppymex, handle) {
      handle.doc() = "Python Wrappers";
  
      // how to wrap functions, easy huh? :D
      handle.def("myfunc0", &mycppcode::myfunc0);
      handle.def("myfunc1", &mycppcode::myfunc1);
  
      // how to wrap classes, also easy *_* (every class function has to be defined seperatly tho :/ )
      py::class_<mycppcode::MyClass, std::shared_ptr<mycppcode::MyClass>> myclass(handle, "MyClass");
      myclass.def(py::init<std::string>());
      myclass.def("print_name", &mycppcode::MyClass::printName);
  }
  ```

- in the `CMakesList.txt` (top level of the project) we must add the lines which ensure that we find 
  the python installation as well as that we build the correct python module (it is quite important 
  that the name `cpppymex` matches the pybind11 module we defined earlier)
  ```cmake
  find_package(Python3 REQUIRED)
  include_directories(${PYTHON_INCLUDE_DIRS})
  pybind11_add_module(cpppymex pythonbinding/pythonwrappers.cpp)
  add_subdirectory(pythonbinding)
  ``` 

- finally, we need to edit the `setup.py` file and tell it what module we want to build 
  (especially the `CMakeExtension(name='cpppymex')` must match the other module name that 
   we have defined before)
  ```python
  setup(
      name='cpppymex',
      version='0.0.1',
      description='Starter project for cpp python wrappers',
      packages=find_packages(),
      ext_modules=[CMakeExtension(name='cpppymex')],
      cmdclass=dict(build_ext=CMakeBuild),
      zip_safe=False,
      setup_requires=['wheel']
  )
  ```

Voila, we have written our own python wrapper for our C++ code 🥳.


For installation of the python wrapper simply run `python setup.py install` 
(with a terminal opened in the root of the template project).

## 🔺 Writing the Matlab Wrapper

Matlab wrappers do not have such easy syntax unfortunaltey an one has to deal with lots of pointer stuff. To write the 
wrapper we need to touch the following to things

- in the `CMakesList.txt` (top level of the project) we need to set a new target (e.g. `cpppy_myfunc`, the name of the 
  `.cpp` file in the `mex/` folder) and add the `mex` subdirectory (`find_matlab` might fail, see the repo on specifics 
  in such scenarios).
  ```cmake
  find_package(Matlab REQUIRED)
  set(PROJECT_NAME cpppy_myfunc)
  add_subdirectory(mex)
  ```

- in `cpppy_myfunc.cpp` we have to provide interfaces for each function. We'll do it for `my_func1` as an example.
  ```cpp
  // read input 
  Eigen::MatrixXd INP;
  igl::matlab::parse_rhs_double(&prhs[1], INP);
  Eigen::MatrixXi INPint = INP.cast<int>();
  
  std::string string_data = parseStringInput(prhs, 2);
  
  
  // call our C++ function
  std::tuple<Eigen::MatrixXi, Eigen::MatrixXf> out = mycppcode::myfunc1(INPint, string_data);
  
  
  // write output (for that we need to create matlab matrices via mxCreateDoubleMatrix)
  Eigen::MatrixXi A = std::get<0>(out);
  Eigen::MatrixXf B = std::get<1>(out);
  
  plhs[0] = mxCreateDoubleMatrix(A.rows(), A.cols(), mxREAL);
  std::copy(A.data(), A.data() + A.size(), mxGetPr(plhs[0]));
  
  plhs[1] = mxCreateDoubleMatrix(B.rows(), B.cols(), mxREAL);
  std::copy(B.data(), B.data() + B.size(), mxGetPr(plhs[1]));
  ```

Unfortunately, its not so easy to define wrappers for classes so we usually have to use functions alone as interfaces.

The installation can be done as follow:

```bash 
mkdir build
cd build
cmake .. -DBUILD_MEX_FILE=True
make -j 4 cpppy_myfunc
```

And afterwards you obtain e.g. a file `cpppy_myfunc.mexmaca64` in `build/mex/` folder which you can copy into your 
project and use there.



## 💡 Good to Know

- you cannot debug into either the mex code nor the python bindings. Best practice for developement is to set up a c++
  project via e.g.
  ```bash
  mkdir dev
  cd dev
  cmake .. -GXcode
  ```
  (this will create an Xcode project, yet you can use other IDEs e.g. for
  VSCode follow [this](https://code.visualstudio.com/docs/cpp/cmake-linux) tutorial)
- the c++ code (if not specified otherwise manually) will be compiled in Release mode. So it is as fast as it gets.
- pybind supports also more pythonic inputs and outputs, the full documentation can be 
  found [here](https://pybind11.readthedocs.io/en/stable/basics.html)
