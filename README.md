# AMD ROCm Release Notes v3.3.0
This page describes the features, fixed issues, and information about downloading and installing the ROCm software.
It also covers known issues and deprecated features in the ROCm v3.3 release.

- [What Is ROCm?](#What-Is-ROCm)
  * [ROCm Components](#ROCm-Components)
  * [Supported Operating Systems](#Supported-Operating-Systems)
  * [Important ROCm Links](#Important-ROCm-Links)
  
- [What\'s New in This Release](#Whats-New-in-This-Release)
  * [Multi Version Installation](#Multi-Version-Installation)
  * [GPU Process Information](#GPU-Process-Information)
  * [Support for 3D Pooling Layers](#Support-for-3D-Pooling-Layers)
  * [ONNX Enhancements](#ONNX-Enhancements)
  
  
- [Deploying ROCm](#Deploying-ROCm)
 
- [Deprecations in This Release](#Deprecations-in-This-Release)
  * [Code Object Manager (Comgr) Functions](#Code-Object-Manager-(Comgr)-Functions)


- [Hardware and Software Support](#Hardware-and-Software-Support)
- [Machine Learning and High Performance Computing Software Stack for AMD GPU](#Machine-Learning-and-High-Performance-Computing-Software-Stack-for-AMD-GPU)
  * [ROCm Binary Package Structure](#ROCm-Binary-Package-Structure)
  * [ROCm Platform Packages](#ROCm-Platform-Packages)
  

## What Is ROCm?
ROCm is designed to be a universal platform for gpu-accelerated computing. This modular design allows hardware vendors to build drivers that support the ROCm framework. ROCm is also designed to integrate multiple programming languages and makes it easy to add support for other languages. 

Note: You can also clone the source code for individual ROCm components from the GitHub repositories.


### ROCm Components
The following components for the ROCm platform are released and available for the v3.3
release:

• Drivers

• Tools

• Libraries

• Source Code

You can access the latest supported version of drivers, tools, libraries, and source code for the ROCm platform at the following location:
https://github.com/RadeonOpenCompute/ROCm

### Supported Operating Systems
The ROCm v3.3.x platform is designed to support the following operating systems:


* Ubuntu 16.04.6 (Kernel 4.15) and 18.04.4 (Kernel 5.3)

* CentOS v7.7 (Using devtoolset-7 runtime support)

* RHEL v7.7 (Using devtoolset-7 runtime support)

* SLES 15 SP1 



### Important ROCm Links

Access the following links for more information on:

* ROCm documentation, see 
https://rocm-documentation.readthedocs.io/en/latest/index.html

* ROCm Release Notes
https://rocm-documentation.readthedocs.io/en/latest/Current_Release_Notes/Current-Release-Notes.html

* ROCm QuickStart Installation Guide, see
https://rocm-documentation.readthedocs.io/en/latest/Installation_Guide/Installation-Guide.html

* ROCm binary structure, see
https://rocm-documentation.readthedocs.io/en/latest/Installation_Guide/Installation-Guide.html#rocm-platform-packages


* Instructions to install PyTorch after ROCm is installed – https://rocm-documentation.readthedocs.io/en/latest/Deep_learning/Deep-learning.html#pytorch

Note: These instructions reference the rocm/pytorch:rocm3.0_ubuntu16.04_py2.7_pytorch image. However, you can substitute the Ubuntu 18.04 image listed at https://hub.docker.com/r/rocm/pytorch/tags


## What\'s New in This Release

### Multi Version Installation

Users can install and access multiple versions of the ROCm toolkit simultaneously.

Previously, users could install only a single version of the ROCm toolkit. 

Now, users have the option to install multiple versions simultaneously and toggle to the desired version of the ROCm toolkit. From the v3.3 release, multiple versions of ROCm packages can be installed in the */opt/rocm-<version>* folder. 


**Prerequisites**

Ensure the existing installations of ROCm, including/opt/rocm, are completely removed before the v3.3 ROCm toolkit installation. The ROCm v3.3 package requires a clean installation.

* To install a single instance of ROCm, use the rocm-dkms or rocm-dev packages to install all the required components. This creates a symbolic link /opt/rocm pointing to the corresponding version of ROCm installed on the system. 

* To install individual ROCm components, create the /opt/rocm symbolic link pointing to the version of ROCm installed on the system. 
For example, # ln -s /opt/rocm-3.3.0 /opt/rocm

* To install multiple instance ROCm packages, create /opt/rocm symbolic link pointing to the version of ROCm installed/used on the system. 
For example, # ln -s /opt/rocm-3.3.0 /opt/rocm

**NOTE**: The Kernel Fusion Driver (KFD) must be compatible with all versions of the ROCm software installed on the system.

**Before You Begin**

Review the following important notes:

Single Version Installation

To install a single instance of the ROCm package, access the non-versioned packages. You must not install any components from the multi-instance set.

For example, 

* rocm-dkms
* rocm-dev
* hip

A fresh installation or an upgrade of the single-version installation will remove the existing version completely and install the new version in the */opt/rocm-<version>* folder.

![ScreenShot](singleinstance.png)


**Multi-version Installation**

* To install a multi-instance of the ROCm package, access the versioned packages and components. 

For example,

* rocm-dkms3.3.0
* rocm-dev3.3.0
* hip3.3.0
	
* The new multi-instance package enables you to install two versions of the ROCm toolkit simultaneously and provides the ability to toggle between the two versioned packages.

* The ROCm-DEV package does not create symlinks

* Users must create symlinks if required

* Multi-version installation with previous ROCm versions is not supported

* Kernel Fusion Driver (KFD) must be compatible with all versions of ROCm installations

![ScreenShot](MultiIns.png)

**IMPORTANT**: A single instance ROCm package cannot co-exist with the multi-instance package. 

**NOTE**: The multi-instance installation applies only to ROCm v3.3 and above. This package requires a fresh installation after the complete removal of existing ROCm packages. **The multi-version installation is not backward compatible.**


## GPU Process Information 

A new functionality to display process information for GPUs is available in this release. For example,  you can view the process details to determine if the GPU(s) must be reset. 

To display the GPU process details, you can:

* Invoke the API 

or

* Use the Command Line Interface (CLI)

For more details about the API and the command instructions, see

https://github.com/RadeonOpenCompute/rocm_smi_lib/blob/master/docs/ROCm_SMI_Manual.pdf


## Support for 3D Pooling Layers

AMD ROCm is enhanced to include support for 3D pooling layers. The implementation of 3D pooling layers now allows users to run 3D convolutional networks, such as ResNext3D, on AMD Radeon Instinct GPUs. 


## ONNX Enhancements
 
Open Neural Network eXchange (ONNX) is a widely-used neural net exchange format. The AMD model compiler & optimizer support the pre-trained models in ONNX, NNEF, & Caffe formats. Currently, ONNX versions 1.3 and below are supported. 

The AMD Neural Net Intermediate Representation (NNIR) is enhanced to handle the rapidly changing ONNX versions and its layers. 

![ScreenShot](onnx.png)

For more details about AMD support for ONNX and ISV samples, see

https://github.com/GPUOpen-ProfessionalCompute-Libraries/MIVisionX/tree/master/model_compiler



## Deploying ROCm
AMD hosts both Debian and RPM repositories for the ROCm v3.3.0x packages. 

The following directions show how to install ROCm on supported Debian-based systems such as Ubuntu 18.04.x. 

Note: These directions may not work as written on unsupported Debian-based distributions. For example, newer versions of Ubuntu may not be compatible with the rock-dkms kernel driver. In this case, you can exclude the rocm-dkms and rock-dkms packages.

For more information on ROCM installation on all platforms, see

https://rocm-documentation.readthedocs.io/en/latest/Installation_Guide/Installation-Guide.html


## Deprecations in This Release

### Code Object Manager (Comgr) Functions

The following Code Object Manager (Comgr) functions are deprecated.

* `amd_comgr_action_info_set_options` 

* `amd_comgr_action_info_get_options` 

These functions were originally deprecated in version 1.3 of the Comgr library as they no longer support options with embedded spaces. 
The deprecated functions are now replaced with the array-oriented options API, which includes 

* `amd_comgr_action_info_set_option_list`

* `amd_comgr_action_info_get_option_list_count`

* `amd_comgr_action_info_get_option_list_item`


## Hardware and Software Support
ROCm is focused on using AMD GPUs to accelerate computational tasks such as machine learning, engineering workloads, and scientific computing.
In order to focus our development efforts on these domains of interest, ROCm supports a targeted set of hardware configurations which are detailed further in this section.

#### Supported GPUs
Because the ROCm Platform has a focus on particular computational domains, we offer official support for a selection of AMD GPUs that are designed to offer good performance and price in these domains.

ROCm officially supports AMD GPUs that use following chips:

  * GFX8 GPUs
    * "Fiji" chips, such as on the AMD Radeon R9 Fury X and Radeon Instinct MI8
    * "Polaris 10" chips, such as on the AMD Radeon RX 580 and Radeon Instinct MI6
  * GFX9 GPUs
    * "Vega 10" chips, such as on the AMD Radeon RX Vega 64 and Radeon Instinct MI25
    * "Vega 7nm" chips, such as on the Radeon Instinct MI50, Radeon Instinct MI60 or AMD Radeon VII

ROCm is a collection of software ranging from drivers and runtimes to libraries and developer tools.
Some of this software may work with more GPUs than the "officially supported" list above, though AMD does not make any official claims of support for these devices on the ROCm software platform.
The following list of GPUs are enabled in the ROCm software, though full support is not guaranteed:

  * GFX8 GPUs
    * "Polaris 11" chips, such as on the AMD Radeon RX 570 and Radeon Pro WX 4100
    * "Polaris 12" chips, such as on the AMD Radeon RX 550 and Radeon RX 540
  * GFX7 GPUs
    * "Hawaii" chips, such as the AMD Radeon R9 390X and FirePro W9100

As described in the next section, GFX8 GPUs require PCI Express 3.0 (PCIe 3.0) with support for PCIe atomics. This requires both CPU and motherboard support. GFX9 GPUs require PCIe 3.0 with support for PCIe atomics by default, but they can operate in most cases without this capability.

The integrated GPUs in AMD APUs are not officially supported targets for ROCm.
As described [below](#limited-support), "Carrizo", "Bristol Ridge", and "Raven Ridge" APUs are enabled in our upstream drivers and the ROCm OpenCL runtime.
However, they are not enabled in our HCC or HIP runtimes, and may not work due to motherboard or OEM hardware limitations.
As such, they are not yet officially supported targets for ROCm.

For a more detailed list of hardware support, please see [the following documentation](https://rocm.github.io/hardware.html).

#### Supported CPUs
As described above, GFX8 GPUs require PCIe 3.0 with PCIe atomics in order to run ROCm.
In particular, the CPU and every active PCIe point between the CPU and GPU require support for PCIe 3.0 and PCIe atomics.
The CPU root must indicate PCIe AtomicOp Completion capabilities and any intermediate switch must indicate PCIe AtomicOp Routing capabilities.

Current CPUs which support PCIe Gen3 + PCIe Atomics are:

  * AMD Ryzen CPUs
  * The CPUs in AMD Ryzen APUs
  * AMD Ryzen Threadripper CPUs
  * AMD EPYC CPUs
  * Intel Xeon E7 v3 or newer CPUs
  * Intel Xeon E5 v3 or newer CPUs
  * Intel Xeon E3 v3 or newer CPUs
  * Intel Core i7 v4, Core i5 v4, Core i3 v4 or newer CPUs (i.e. Haswell family or newer)
  * Some Ivy Bridge-E systems

Beginning with ROCm 1.8, GFX9 GPUs (such as Vega 10) no longer require PCIe atomics.
We have similarly opened up more options for number of PCIe lanes.
GFX9 GPUs can now be run on CPUs without PCIe atomics and on older PCIe generations, such as PCIe 2.0.
This is not supported on GPUs below GFX9, e.g. GFX8 cards in the Fiji and Polaris families.

If you are using any PCIe switches in your system, please note that PCIe Atomics are only supported on some switches, such as Broadcom PLX.
When you install your GPUs, make sure you install them in a PCIe 3.1.0 x16, x8, x4, or x1 slot attached either directly to the CPU's Root I/O controller or via a PCIe switch directly attached to the CPU's Root I/O controller.

In our experience, many issues stem from trying to use consumer motherboards which provide physical x16 connectors that are electrically connected as e.g. PCIe 2.0 x4, PCIe slots connected via the Southbridge PCIe I/O controller, or PCIe slots connected through a PCIe switch that does
not support PCIe atomics.

If you attempt to run ROCm on a system without proper PCIe atomic support, you may see an error in the kernel log (`dmesg`):
```
kfd: skipped device 1002:7300, PCI rejects atomics
```

Experimental support for our Hawaii (GFX7) GPUs (Radeon R9 290, R9 390, FirePro W9100, S9150, S9170)
does not require or take advantage of PCIe Atomics. However, we still recommend that you use a CPU
from the list provided above for compatibility purposes.

#### Not supported or limited support under ROCm
##### Limited support

* ROCm 2.9.x should support PCIe 2.0 enabled CPUs such as the AMD Opteron, Phenom, Phenom II, Athlon, Athlon X2, Athlon II and older Intel Xeon and Intel Core Architecture and Pentium CPUs. However, we have done very limited testing on these configurations, since our test farm has been catering to CPUs listed above. This is where we need community support. _If you find problems on such setups, please report these issues_.
* Thunderbolt 1, 2, and 3 enabled breakout boxes should now be able to work with ROCm. Thunderbolt 1 and 2 are PCIe 2.0 based, and thus are only supported with GPUs that do not require PCIe 3.1.0 atomics (e.g. Vega 10). However, we have done no testing on this configuration and would need community support due to limited access to this type of equipment.
* AMD "Carrizo" and "Bristol Ridge" APUs are enabled to run OpenCL, but do not yet support HCC, HIP, or our libraries built on top of these compilers and runtimes.
  * As of ROCm 2.1, "Carrizo" and "Bristol Ridge" require the use of upstream kernel drivers.
  * In addition, various "Carrizo" and "Bristol Ridge" platforms may not work due to OEM and ODM choices when it comes to key configurations parameters such as inclusion of the required CRAT tables and IOMMU configuration parameters in the system BIOS.
  * Before purchasing such a system for ROCm, please verify that the BIOS provides an option for enabling IOMMUv2 and that the system BIOS properly exposes the correct CRAT table. Inquire with your vendor about the latter.
* AMD "Raven Ridge" APUs are enabled to run OpenCL, but do not yet support HCC, HIP, or our libraries built on top of these compilers and runtimes.
  * As of ROCm 2.1, "Raven Ridge" requires the use of upstream kernel drivers.
  * In addition, various "Raven Ridge" platforms may not work due to OEM and ODM choices when it comes to key configurations parameters such as inclusion of the required CRAT tables and IOMMU configuration parameters in the system BIOS.
  * Before purchasing such a system for ROCm, please verify that the BIOS provides an option for enabling IOMMUv2 and that the system BIOS properly exposes the correct CRAT table. Inquire with your vendor about the latter.

##### Not supported

* "Tonga", "Iceland", "Vega M", and "Vega 12" GPUs are not supported in ROCm 2.9.x
* We do not support GFX8-class GPUs (Fiji, Polaris, etc.) on CPUs that do not have PCIe 3.0 with PCIe atomics.
  * As such, we do not support AMD Carrizo and Kaveri APUs as hosts for such GPUs.
  * Thunderbolt 1 and 2 enabled GPUs are not supported by GFX8 GPUs on ROCm. Thunderbolt 1 & 2 are based on PCIe 2.0.

#### ROCm support in upstream Linux kernels

As of ROCm 1.9.0, the ROCm user-level software is compatible with the AMD drivers in certain upstream Linux kernels.
As such, users have the option of either using the ROCK kernel driver that are part of AMD's ROCm repositories or using the upstream driver and only installing ROCm user-level utilities from AMD's ROCm repositories.

These releases of the upstream Linux kernel support the following GPUs in ROCm:
 * 4.17: Fiji, Polaris 10, Polaris 11
 * 4.18: Fiji, Polaris 10, Polaris 11, Vega10
 * 4.20: Fiji, Polaris 10, Polaris 11, Vega10, Vega 7nm

The upstream driver may be useful for running ROCm software on systems that are not compatible with the kernel driver available in AMD's repositories.
For users that have the option of using either AMD's or the upstreamed driver, there are various tradeoffs to take into consideration:

|   | Using AMD's `rock-dkms` package | Using the upstream kernel driver |
| ---- | ------------------------------------------------------------| ----- |
| Pros | More GPU features, and they are enabled earlier | Includes the latest Linux kernel features |
|      | Tested by AMD on supported distributions | May work on other distributions and with custom kernels |
|      | Supported GPUs enabled regardless of kernel version | |
|      | Includes the latest GPU firmware | |
| Cons | May not work on all Linux distributions or versions | Features and hardware support varies depending on kernel version |
|      | Not currently supported on kernels newer than 5.4 | Limits GPU's usage of system memory to 3/8 of system memory (before 5.6). For 5.6 and beyond, both DKMS and upstream kernels allow use of 15/16 of system memory. |
|      |   | IPC and RDMA capabilities are not yet enabled |
|      |   | Not tested by AMD to the same level as `rock-dkms` package |
|      |   | Does not include most up-to-date firmware |


## Software Support
As of AMD ROCm v1.9.0, the ROCm user-level software is compatible with the AMD drivers in certain upstream Linux kernels. You have the following options:

• Use the ROCk kernel driver that is a part of AMD’s ROCm repositories 
or
• Use the upstream driver and only install ROCm user-level utilities from AMD’s ROCm repositories

The releases of the upstream Linux kernel support the following GPUs in ROCm:

• Fiji, Polaris 10, Polaris 11
• Fiji, Polaris 10, Polaris 11, Vega10
• Fiji, Polaris 10, Polaris 11, Vega10, Vega 7nm



## Machine Learning and High Performance Computing Software Stack for AMD GPU

ROCm Version 3.3.0

### ROCm Binary Package Structure

 ROCm is a collection of software ranging from drivers and runtimes to libraries and developer tools.
In AMD's package distributions, these software projects are provided as a separate packages.
This allows users to install only the packages they need, if they do not wish to install all of ROCm.
These packages will install most of the ROCm software into `/opt/rocm/` by default.

The packages for each of the major ROCm components are:

* ROCm Core Components
  - ROCk Kernel Driver: `rock-dkms`
  - ROCr Runtime: `hsa-rocr-dev`, `hsa-ext-rocr-dev`
  - ROCt Thunk Interface: `hsakmt-roct`, `hsakmt-roct-dev`
* ROCm Support Software
  - ROCm SMI: `rocm-smi`
  - ROCm cmake: `rocm-cmake`
  - rocminfo: `rocminfo`
  - ROCm Bandwidth Test: `rocm_bandwidth_test`
* ROCm Development Tools
  - HCC compiler: `hcc`
  - HIP: `hip_base`, `hip_doc`, `hip_hcc`, `hip_samples`
  - ROCm Device Libraries: `rocm-device-libs`
  - ROCm OpenCL: `rocm-opencl`, `rocm-opencl-devel` (on RHEL/CentOS), `rocm-opencl-dev` (on Ubuntu)
  - ROCM Clang-OCL Kernel Compiler: `rocm-clang-ocl`
  - Asynchronous Task and Memory Interface (ATMI): `atmi`
  - ROCr Debug Agent: `rocr_debug_agent`
  - ROCm Code Object Manager: `comgr`
  - ROC Profiler: `rocprofiler-dev`
  - ROC Tracer: `roctracer-dev`
  - Radeon Compute Profiler: `rocm-profiler`
* ROCm Libraries
  - rocALUTION: `rocalution`
  - rocBLAS: `rocblas`
  - hipBLAS: `hipblas`
  - hipCUB: `hipCUB`
  - rocFFT: `rocfft`
  - rocRAND: `rocrand`
  - rocSPARSE: `rocsparse`
  - hipSPARSE: `hipsparse`
  - ROCm SMI Lib: `rocm_smi_lib64`
  - rocThrust: `rocThrust`
  - MIOpen: `MIOpen-HIP` (for the HIP version), `MIOpen-OpenCL` (for the OpenCL version)
  - MIOpenGEMM: `miopengemm`
  - MIVisionX: `mivisionx`
  - RCCL: `rccl`

To make it easier to install ROCm, the AMD binary repositories provide a number of meta-packages that will automatically install multiple other packages.
For example, `rocm-dkms` is the primary meta-package that is used to install most of the base technology needed for ROCm to operate.
It will install the `rock-dkms` kernel driver, and another meta-package (`rocm-dev`) which installs most of the user-land ROCm core components, support software, and development tools.

The `rocm-utils` meta-package will install useful utilities that, while not required for ROCm to operate, may still be beneficial to have.
Finally, the `rocm-libs` meta-package will install some (but not all) of the libraries that are part of ROCm.

The chain of software installed by these meta-packages is illustrated below

```
  rocm-dkms
    |--rock-dkms
    \--rocm-dev
       |--comgr
       |--hcc
       |--hip_base
       |--hip_doc
       |--hip_hcc
       |--hip_samples
       |--hsakmt-roct
       |--hsakmt-roct-dev
       |--hsa-amd-aqlprofile
       |--hsa-ext-rocr-dev
       |--hsa-rocr-dev
       |--rocm-cmake
       |--rocm-device-libs
       |--rocm-smi
       |--rocprofiler-dev
       |--rocr_debug_agent
       \--rocm-utils
          |--rocminfo
          \--rocm-clang-ocl # This will cause OpenCL to be installed

  rocm-libs
    |--hipblas
    |--hipcub
    |--hipsparse
    |--rocalution
    |--rocblas
    |--rocfft
    |--rocprim
    |--rocrand
    |--rocsparse
    \--rocthrust
```

These meta-packages are not required but may be useful to make it easier to install ROCm on most systems.

Note:Some users may want to skip certain packages. For instance, a user that wants to use the upstream kernel drivers (rather than those supplied by AMD) may want to skip the `rocm-dkms` and `rock-dkms` packages, and instead directly install `rocm-dev`.

Similarly, a user that only wants to install OpenCL support instead of HCC and HIP may want to skip the `rocm-dkms` and `rocm-dev` packages. Instead, they could directly install `rock-dkms`, `rocm-opencl`, and `rocm-opencl-dev` and their dependencies.


### ROCm Platform Packages

Drivers, ToolChains, Libraries, and Source Code 

The latest supported version of the drivers, tools, libraries and source code for the ROCm platform have been released and are available from the following GitHub repositories:

#### ROCm Core Components
  - [ROCk Kernel Driver](https://github.com/RadeonOpenCompute/ROCK-Kernel-Driver/tree/roc-3.3.0)
  - [ROCr Runtime](https://github.com/RadeonOpenCompute/ROCR-Runtime/tree/rocm-3.3.0)
  - [ROCT Thunk Interface](https://github.com/RadeonOpenCompute/ROCT-Thunk-Interface/tree/roc-3.3.0)  

  
#### ROCm Support Software
  - [ROCm SMI](https://github.com/RadeonOpenCompute/ROC-smi/tree/roc-3.3.0)
  - [ROCm cmake](https://github.com/RadeonOpenCompute/rocm-cmake/tree/rocm-3.3.0)
  - [rocminfo](https://github.com/RadeonOpenCompute/rocminfo/tree/rocm-3.3.0)
  - [ROCm Bandwidth Test](https://github.com/RadeonOpenCompute/rocm_bandwidth_test/tree/rocm-3.3.0)
  
#### ROCm Development ToolChain
  - [HCC compiler](https://github.com/RadeonOpenCompute/hcc/tree/rocm-3.3.0)
  
  - [HIP](https://github.com/ROCm-Developer-Tools/HIP/tree/rocm-3.3.0)
  
  - [ROCm Device Libraries HCC](https://github.com/RadeonOpenCompute/ROCm-Device-Libs/tree/roc-ocl-3.3.0)
  
  - [ROCm OpenCL Runtime](http://github.com/RadeonOpenCompute/ROCm-OpenCL-Runtime/tree/roc-3.3.0)
   
  - [ROCm LLVM OCL](http://github.com/RadeonOpenCompute/llvm-project/tree/rocm-ocl-3.3.0)   
      
  - [ROCm Device Libraries OCL](https://github.com/RadeonOpenCompute/ROCm-Device-Libs/tree/rocm-ocl-3.3.0)
      
  - [ROCM Clang-OCL Kernel Compiler](https://github.com/RadeonOpenCompute/clang-ocl/tree/rocm-3.3.0)
  
  - [Asynchronous Task and Memory Interface (ATMI)](https://github.com/RadeonOpenCompute/atmi/tree/rocm-3.3.0)
  
  - [ROCr Debug Agent](https://github.com/ROCm-Developer-Tools/rocr_debug_agent/tree/roc-3.3.0)
  
  - [ROCm Code Object Manager](https://github.com/RadeonOpenCompute/ROCm-CompilerSupport/tree/rocm-3.3.0)
  
  - [ROC Profiler](https://github.com/ROCm-Developer-Tools/rocprofiler/tree/roc-3.3.0)
  
  - [ROC Tracer](https://github.com/ROCm-Developer-Tools/roctracer/tree/roc-3.3.0)
  
  - [AOMP](https://github.com/ROCm-Developer-Tools/aomp/tree/roc-3.3.0)
  
  - [Radeon Compute Profiler](https://github.com/GPUOpen-Tools/RCP/tree/3a49405)
  
  - [ROCmValidationSuite](https://github.com/ROCm-Developer-Tools/ROCmValidationSuite/tree/roc-3.3.0)
  
  - Example Applications:
    - [HCC Examples](https://github.com/ROCm-Developer-Tools/HCC-Example-Application/tree/ffd65333)
    
    - [HIP Examples](https://github.com/ROCm-Developer-Tools/HIP-Examples/tree/rocm-3.3.0)
    
#### ROCm Libraries

  - [rocBLAS](https://github.com/ROCmSoftwarePlatform/rocBLAS/tree/rocm-3.3.0)
  
  - [hipBLAS](https://github.com/ROCmSoftwarePlatform/hipBLAS/tree/rocm-3.3.0)
  
  - [rocFFT](https://github.com/ROCmSoftwarePlatform/rocFFT/tree/rocm-3.3)
  
  - [rocRAND](https://github.com/ROCmSoftwarePlatform/rocRAND/tree/rocm-3.3.0)
  
  - [rocSPARSE](https://github.com/ROCmSoftwarePlatform/rocSPARSE/tree/rocm-3.3.0)
  
  - [hipSPARSE](https://github.com/ROCmSoftwarePlatform/hipSPARSE/tree/rocm-3.3.0)
  
  - [rocALUTION](https://github.com/ROCmSoftwarePlatform/rocALUTION/tree/rocm-3.3.0)
  
  - [MIOpenGEMM](https://github.com/ROCmSoftwarePlatform/MIOpenGEMM/tree/b51a125)
  
  - [MIOpen](https://github.com/ROCmSoftwarePlatform/MIOpen/tree/roc-3.3.0)
  
  - [rocThrust](https://github.com/ROCmSoftwarePlatform/rocThrust/tree/rocm-3.3.0)
  
  - [ROCm SMI Lib](https://github.com/RadeonOpenCompute/rocm_smi_lib/tree/rocm-3.3.0)
  
  - [RCCL](https://github.com/ROCmSoftwarePlatform/rccl/tree/rocm-3.3.0)
  
  - [MIVisionX](https://github.com/GPUOpen-ProfessionalCompute-Libraries/MIVisionX/commit/755e7a08d5299a95c42def092af7c736d5eda90c)
  
  - [MIVisionX](https://github.com/GPUOpen-ProfessionalCompute-Libraries/MIVisionX/tree/1.7)
  
  - [hipCUB](https://github.com/ROCmSoftwarePlatform/hipCUB/tree/rocm-3.3.0)
  
  - [AMDMIGraphX](https://github.com/ROCmSoftwarePlatform/AMDMIGraphX/commit/d1e945dabce0078d44c78de67b00232b856e18bc)


Features and enhancements introduced in previous versions of ROCm can be found in [version_history.md](version_history.md)
