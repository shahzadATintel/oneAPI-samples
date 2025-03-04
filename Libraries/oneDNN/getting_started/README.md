# `oneDNN Getting Started` Sample

oneAPI Deep Neural Network Library (oneDNN) is an open-source performance
library for deep learning applications. The library includes basic building
blocks for neural networks optimized for Intel Architecture Processors
and Intel Processor Graphics. oneDNN is intended for deep learning
applications and framework developers interested in improving application
performance on Intel CPUs and GPUs.
You can find library source code and code used by these samples at the oneDNN Github repository.

This sample is implemented in C++ and executes on CPU or GPU. The sample also
also includes [a Jupyer Notebook](https://github.com/oneapi-src/oneAPI-samples/blob/master/Libraries/oneDNN/tutorials/tutorial_getting_started.ipynb) that
demonstrates how to compile the code with various oneDNN configurations
in Intel® DevCloud for oneAPI environment.

| Optimized for                      | Description
| :---                               | :---
| OS                                 | Linux* Ubuntu* 18.04; Windows 10
| Hardware                           | Skylake with GEN9 or newer
| Software                           | oneAPI Deep Neural Network Library (oneDNN), oneAPI DPC++/C++ Compiler, oneAPI Threading Building Blocks (oneTBB), GNU Compiler Collection, Intel® C++ Compiler
| What you will learn                | Running a simple convolutional model on Intel CPU or Intel GPU
| Time to complete                   | 15 minutes

## Purpose

This sample demonstrates the basics of the oneDNN programming model. With this code 
sample, you will learn:
* How to create oneDNN memory objects.
* How to get data from application buffer into an oneDNN memory object.
* How tensor's logical dimensions and memory object formats relate.
* How to create oneDNN primitives.
* How to execute the primitives.

The sample executes on the system's CPU by default and can be executed on Intel GPU
using a command line parameter `gpu`.

## Key Implementation Details

This sample uses example file `${DNNLROOT}/examples/getting_started.cpp`
from oneDNN distribution. You can find this code in
[oneDNN Github repository](https://github.com/oneapi-src/oneDNN/blob/dev-v2/examples/getting_started.cpp).

Detailed code walkthrough is available in [oneDNN developer guide](https://oneapi-src.github.io/oneDNN/v2/getting_started.html)

## License

Code samples are licensed under the MIT license. See
[License.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/License.txt) for details.

Third party program Licenses can be found here: [third-party-programs.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/third-party-programs.txt)

## Building the sample for CPU and GPU

### On a Linux System

Perform the following steps:
1. Setup oneAPI development environment
```
source ${INTEL_ONEAPI_INSTALL_FOLDER}/setvars.sh
```
2. Build the program using `cmake`
```
mkdir build
cd build
cmake ..
make
```
> NOTE: The source file "getting_started.cpp" will be copied from ${INTEL_ONEAPI_INSTALL_FOLDER}/dnnl/latest/cpu_dpcpp_gpu_dpcpp/examples/ to build/src folder. Users can rebuild the getting_started.cpp by typing "make" under build folder.

3. Run the program
```
./bin/getting-started-cpp
```

By default, the sample uses oneAPI DPC++/C++ Compiler and can execute on CPUs or
Intel GPUs. You can build the sample with CPU support with other compilers
and threading runtimes:
* GNU C++ Compiler and GNU OpenMP runtime
```
source ${INTEL_ONEAPI_INSTALL_FOLDER}/setvars.sh --dnnl-configuration=cpu_gomp
CC=GCC CXX=g++ cmake ..
```
* Intel® C++ Compiler and Intel OpenMP runtime
```
source ${INTEL_ONEAPI_INSTALL_FOLDER}/setvars.sh --dnnl-configuration=cpu_iomp
CC=icc CXX=icpc cmake ..
```
* Intel® C++ Compiler and TBB runtime
```
source ${INTEL_ONEAPI_INSTALL_FOLDER}/setvars.sh --dnnl-configuration=cpu_tbb
CC=icc CXX=icpc cmake ..
```

### On a Windows* System 

Open "Intel oneAPI command prompt for Intel 64 for Visual Studio 2017" or 
"Intel oneAPI command prompt for Intel 64 for Visual Studio 2019" and perform the following steps:
1. Setup oneAPI development environment
```
C:\Program Files (x86)\Intel\oneAPI\setvars.bat
```
2. Build the program using `cmake`
```
cd C:\Program Files (x86)\Intel\oneAPI\dnnl\latest\cpu_dpcpp_gpu_dpcpp\examples\
mkdir build
cd build
set CC=clang
set CXX=clang++
cmake -G Ninja .. -DDNNL_CPU_RUNTIME=DPCPP -DDNNL_GPU_RUNTIME=DPCPP
cmake --build .
```

3. Run the program
```
getting-started-cpp.exe
```

### Include Files

The include folder is located at ${DNNLROOT}\include on your development system".

## Running the Sample

### Running Samples In DevCloud
If running a sample in the Intel DevCloud, remember that you must specify the compute node (CPU, GPU, FPGA) and whether to run in batch or interactive mode. For more information, see the Intel® oneAPI Base Toolkit Get Started Guide (https://devcloud.intel.com/oneapi/get-started/base-toolkit/)

### Application Parameters

You can specify the target device for this sample using command-line arguments:
* `cpu` (default) directs the application to run on the system's CPU
* `gpu` directs the sample to run on Intel GPU

> Note: When executed with `gpu` parameter the 
> sample will return an error if the sample is compiled with oneDNN configuration
> that does not support GPU, or no Intel GPUs are found in the system.

You can get additional information during the execution of this sample by setting
environment variable `DNNL_VERBOSE=1`.

#### On a Linux System
```
export DNNL_VERBOSE=1
```
#### On a Windows* System
```
set DNNL_VERBOSE=1
```

### Example of Output

```
Example passed on CPU.
```

When executed with `DNNL_VERBOSE=1`:
```
dnnl_verbose,info,cpu,runtime:DPC++
dnnl_verbose,info,cpu,isa:Intel AVX2
dnnl_verbose,info,gpu,runtime:DPC++
dnnl_verbose,info,cpu,engine,0,backend:OpenCL,name:Intel(R) Core(TM) i9-9900K CPU @ 3.60GHz,driver_version:2020.10.7
dnnl_verbose,info,gpu,engine,0,backend:Level Zero,name:Intel(R) Gen12LP,driver_version:0.8.0
dnnl_verbose,exec,cpu,eltwise,jit:avx2,forward_inference,data_f32::blocked:acdb:f0 diff_undef::undef::f0,,alg:eltwise_relu alpha:0 beta:0,1x3x13x13,0.125
Example passed on CPU.
```
