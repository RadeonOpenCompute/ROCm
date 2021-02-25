# AMD ROCm™ v4.0.1 Patch Release Notes 

## SUPPORTED OPERATING SYSTEMS

### List of Supported Operating Systems

The AMD ROCm platform is designed to support the following operating systems:

* Ubuntu 20.04.1 (5.4 and 5.6-oem) and 18.04.5 (Kernel 5.4)	
* CentOS 7.9 (3.10.0-1127) & RHEL 7.9 (3.10.0-1160.6.1.el7) (Using devtoolset-7 runtime support)
* CentOS 8.3 (4.18.0-193.el8) and RHEL 8.3 (4.18.0-193.1.1.el8) (devtoolset is not required)
* SLES 15 SP2

### SUPPORT FOR RHEL V8.3

This patch release extends support for RHEL v8.3. 

### FRESH INSTALLATION OF AMD ROCM V4.0.1 RECOMMENDED

A fresh and clean installation of AMD ROCm v4.0.1 is recommended. An upgrade from previous releases to AMD ROCm v4.0.1 is not supported. For more information, refer to the AMD ROCm Installation Guide.

**Note**: AMD ROCm release v3.3 or prior releases are not fully compatible with AMD ROCm v3.5 and higher versions. You must perform a fresh ROCm installation if you want to upgrade from AMD ROCm v3.3 or older to 3.5 or higher versions and vice-versa.

**Note**: *render* group is required only for Ubuntu v20.04. For all other ROCm supported operating systems, continue to use video group. 

* For ROCm v3.5 and releases thereafter, the clinfo path is changed to /opt/rocm/opencl/bin/clinfo. 

* For ROCm v3.3 and older releases, the clinfo path remains /opt/rocm/opencl/bin/x86_64/clinfo. 
 
### ROCM MULTI-VERSION INSTALLATION UPDATE

With the AMD ROCm v4.0.1 release, the following ROCm multi-version installation changes apply:

The meta packages rocm-dkms<version> are now deprecated for multi-version ROCm installs.  For example, rocm-dkms3.7.0, rocm-dkms3.8.0.
 
* Multi-version installation of ROCm should be performed by installing rocm-dev<version> using each of the desired ROCm versions. For example, rocm-dev3.7.0, rocm-dev3.8.0, rocm-dev3.9.0.   

* Version files must be created for each multi-version rocm <= 4.0.1

 * Command: echo <version> | sudo tee /opt/rocm-<version>/.info/version

 * Example: echo 4.0.1 | sudo tee /opt/rocm-4.0.1/.info/version

* The rock-dkms loadable kernel modules should be installed using a single rock-dkms package. 

* ROCm v3.9 and above will not set any ldconfig entries for ROCm libraries for multi-version installation.  Users must set LD_LIBRARY_PATH to load the ROCm library version of choice.

**NOTE**: The single version installation of the ROCm stack remains the same. The rocm-dkms package can be used for single version installs and is not deprecated at this time.



# AMD ROCm™ Release Notes v4.0

This page describes the features, fixed issues, and information about downloading and installing the ROCm software.
It also covers known issues in this release.

- [Supported Operating Systems and Documentation Updates](#Supported-Operating-Systems-and-Documentation-Updates)
  * [Supported Operating Systems](#Supported-Operating-Systems)
  * [ROCm Installation Updates](#ROCm-Installation-Updates)
  * [AMD ROCm Documentation Updates](#AMD-ROCm-Documentation-Updates)
   
- [What\'s New in This Release](#Whats-New-in-This-Release)
  * [INTRODUCING AMD INSTINCT MI100](#INTRODUCING-AMD-INSTINCT-MI100)
  * [RAS Enhancements](#RAS-Enhancements)
  * [Using CMake with AMD ROCm](#Using-CMake-with-AMD-ROCm)
  * [AMD ROCm and Mesa Multimedia](#AMD-ROCm-and-Mesa-Multimedia)
  * [ROCm System Management Information](#ROCm-System-Management-Information)
  * [AMD GPU Debugger Enhancements](#AMD-GPU-Debugger-Enhancements)

    
- [Known Issues](#Known-Issues)

- [Deprecations](#Deprecations)

  * [Compiler Generated Code Object Version 2 Deprecation ](#Compiler-Generated-Code-Object-Version-2-Deprecation)
  * [ROCr Runtime Deprecations](#ROCr-Runtime-Deprecations)
  * [AOMP Deprecation](#AOMP-Deprecation)
  

- [Deploying ROCm](#Deploying-ROCm)
 
- [Hardware and Software Support](#Hardware-and-Software-Support)

- [Machine Learning and High Performance Computing Software Stack for AMD GPU](#Machine-Learning-and-High-Performance-Computing-Software-Stack-for-AMD-GPU)
  * [ROCm Binary Package Structure](#ROCm-Binary-Package-Structure)
  * [ROCm Platform Packages](#ROCm-Platform-Packages)
  


# Supported Operating Systems 

## List of Supported Operating Systems

The AMD ROCm platform is designed to support the following operating systems:

* Ubuntu 20.04.1 (5.4 and 5.6-oem) and 18.04.5 (Kernel 5.4)	

* CentOS 7.8 (3.10.0-1127) & RHEL 7.9 (3.10.0-1160.6.1.el7) (Using devtoolset-7 runtime support)

* CentOS 8.2 (4.18.0-193.el8) and RHEL 8.2 (4.18.0-193.1.1.el8) (devtoolset is not required)

* SLES 15 SP2

 
# ROCm Installation Updates

## Fresh Installation of AMD ROCm v4.0 Recommended

A fresh and clean installation of AMD ROCm v4.0 is recommended. An upgrade from previous releases to AMD ROCm v4.0 is not supported.

For more information, refer to the AMD ROCm Installation Guide at:
https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html

**Note**: AMD ROCm release v3.3 or prior releases are not fully compatible with AMD ROCm v3.5 and higher versions. You must perform a fresh ROCm installation if you want to upgrade from AMD ROCm v3.3 or older to 3.5 or higher versions and vice-versa.

**Note**: *render group* is required only for Ubuntu v20.04. For all other ROCm supported operating systems, continue to use *video group*.

* For ROCm v3.5 and releases thereafter,the *clinfo* path is changed to -  */opt/rocm/opencl/bin/clinfo*.

* For ROCm v3.3 and older releases, the *clinfo* path remains unchanged -  */opt/rocm/opencl/bin/x86_64/clinfo*.

**Note**: After an operating system upgrade, AMD ROCm may upgrade automatically and result in an error. This is because AMD ROCm does not support upgrades currently. You must uninstall and reinstall AMD ROCm after an operating system upgrade.


## ROCm MultiVersion Installation Update

With the AMD ROCm v4.0 release, the following ROCm multi-version installation changes apply:

The meta packages rocm-dkms<version> are now deprecated for multi-version ROCm installs. For example, rocm-dkms3.7.0, rocm-dkms3.8.0.
 
* Multi-version installation of ROCm should be performed by installing rocm-dev<version> using   each of the desired ROCm versions. For example, rocm-dev3.7.0, rocm-dev3.8.0, rocm-dev3.9.0.   
* Version files must be created for each multi-version rocm <= 4.0.0

    * command: echo <version> | sudo tee /opt/rocm-<version>/.info/version

    * example: echo 4.0.0 | sudo tee /opt/rocm-4.0.0/.info/version

* The rock-dkms loadable kernel modules should be installed using a single rock-dkms package. 

* ROCm v3.9 and above will not set any *ldconfig* entries for ROCm libraries for multi-version installation.  Users must set *LD_LIBRARY_PATH* to load the ROCm library version of choice.


**NOTE**: The single version installation of the ROCm stack remains the same. The rocm-dkms package can be used for single version installs and is not deprecated at this time.



# AMD ROCm Documentation Updates

## AMD ROCm Installation Guide 

The AMD ROCm Installation Guide in this release includes:

* Supported Environments

* Installation Instructions for v4.0

* HIP Installation Instructions 

* AMD ROCm and Mesa Multimedia Installation 

* Using CMake with AMD ROCm 

For more information, refer to the ROCm documentation website at:

https://rocmdocs.amd.com/en/latest/


## AMD ROCm - HIP Documentation Updates

* HIP Programming Guide v4.0 

https://github.com/RadeonOpenCompute/ROCm/blob/master/HIP_Programming_Guide_v4.0.pdf

* HIP API Guide v4.0

https://github.com/RadeonOpenCompute/ROCm/blob/master/HIP-API_Guide_v4.0.pdf

* HIP FAQ  

For more information, refer to

https://rocmdocs.amd.com/en/latest/Programming_Guides/HIP-FAQ.html#hip-faq


## ROCm SMI API Documentation Updates 

* xGMI API

For more information, refer to the ROCm SMI API Guide at,

https://github.com/RadeonOpenCompute/ROCm/blob/master/ROCm_SMI_API_Guide_v4.0.pdf


## General AMD ROCm Documentation Links

Access the following links for more information:

* For AMD ROCm documentation, see 

  https://rocmdocs.amd.com/en/latest/

* For installation instructions on supped platforms, see

  https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html

* For AMD ROCm binary structure, see

  https://rocmdocs.amd.com/en/latest/Installation_Guide/Software-Stack-for-AMD-GPU.html
  

* For AMD ROCm Release History, see

 https://rocmdocs.amd.com/en/latest/Current_Release_Notes/ROCm-Version-History.html



# What\'s New in This Release

## INTRODUCING AMD INSTINCT MI100

The AMD Instinct™ MI100 accelerator is the world’s fastest HPC GPU, and a culmination of the AMD CDNA architecture, with all-new Matrix Core Technology, and AMD ROCm™ open ecosystem to deliver new levels of performance, portability, and productivity. AMD CDNA is an all-new GPU architecture from AMD to drive accelerated computing into the era of exascale computing. The new architecture augments scalar and vector processing with new Matrix Core Engines and adds Infinity Fabric™ technology to scale up to larger systems. The open ROCm ecosystem puts customers in control and is a robust, mature platform that is easy to develop for and capable of running the most critical applications. The overall result is that the MI100 is the first GPU to break the 10TFLOP/s FP64 barrier designed as the steppingstone to the next generation of Exascale systems that will deliver pioneering discoveries in machine learning and scientific computing.


### Key Features of AMD Instinct™ MI100 

Important features of the AMD Instinct™ MI100 accelerator include:

* Extended matrix core engine with Matrix Fused Multiply-Add (MFMA) for mixed-precision arithmetic and operates on KxN matrices (FP32, FP16, BF16, Int8) 

* Added native support for the bfloat16 data type

* 3 Infinity fabric connections per GPU enable a fully connected group of 4 GPUs in a ‘hive’ 

![Screenshot](https://github.com/Rmalavally/ROCm/blob/master/images/keyfeatures.PNG)


### Matrix Core Engines and GFX908 Considerations

The AMD CDNA architecture builds on GCN’s foundation of scalars and vectors and adds matrices while simultaneously adding support for new numerical formats for machine learning and preserving backward compatibility for any software written for the GCN architecture. These Matrix Core Engines add a new family of wavefront-level instructions, the Matrix Fused MultiplyAdd or MFMA. The MFMA family performs mixed-precision arithmetic and operates on KxN matrices using four different types of input data: 8-bit integers (INT8), 16-bit half-precision FP (FP16), 16-bit brain FP (bf16), and 32-bit single-precision (FP32). All MFMA instructions produce either a 32-bit integer (INT32) or FP32 output, which reduces the likelihood of overflowing during the final accumulation stages of matrix multiplication.

On nodes with gfx908, MFMA instructions are available to substantially speed up matrix operations. This hardware feature is used only in matrix multiplications functions in rocBLAS and supports only three base types f16_r, bf16_r, and f32_r. 

* For half precision (f16_r and bf16_r) GEMM, use the function rocblas_gemm_ex, and set the compute_type parameter to f32_r.

* For single precision (f32_r) GEMM, use the function rocblas_sgemm.

* For single precision complex (f32_c) GEMM, use the function rocblas_cgemm.


### References
* For more information about bfloat16, see 

https://rocblas.readthedocs.io/en/master/usermanual.html

* For more details about AMD Instinct™ MI100 accelerator key features, see 

https://www.amd.com/system/files/documents/instinct-mi100-brochure.pdf

* For more information about the AMD Instinct MI100 accelerator, refer to the following sources:

  - AMD CDNA whitepaper at https://www.amd.com/system/files/documents/amd-cdna-whitepaper.pdf
  
  - MI100 datasheet at https://www.amd.com/system/files/documents/instinct-mi100-brochure.pdf

* AMD Instinct MI100/CDNA1 Shader Instruction Set Architecture (Dec. 2020) – This document describes the current environment, organization, and program state of AMD CDNA “Instinct MI100” devices. It details the instruction set and the microcode formats native to this family of processors that are accessible to programmers and compilers.

https://developer.amd.com/wp-content/resources/CDNA1_Shader_ISA_14December2020.pdf


## RAS Enhancements

RAS (Reliability, Availability, and Accessibility) features provide help with data center GPU management. It is a method provided to users to track and manage data points via options implemented in the ROCm-SMI Command Line Interface (CLI) tool. 

For more information about rocm-smi, see 

https://github.com/RadeonOpenCompute/ROC-smi 

The command options are wrappers of the system calls into the device driver interface as described here:

https://dri.freedesktop.org/docs/drm/gpu/amdgpu.html#amdgpu-ras-support



## Using CMake with AMD ROCm

Most components in AMD ROCm support CMake 3.5 or higher out-of-the-box and do not require any special Find modules. A Find module is often used downstream to find the files by guessing locations of files with platform-specific hints. Typically, the Find module is required when the upstream is not built with CMake or the package configuration files are not available.

AMD ROCm provides the respective config-file packages, and this enables find_package to be used directly. AMD ROCm does not require any Find module as the config-file packages are shipped with the upstream projects.

For more information, see 

https://rocmdocs.amd.com/en/latest/Installation_Guide/Using-CMake-with-AMD-ROCm.html


## AMD ROCm and Mesa Multimedia

AMD ROCm extends support to Mesa Multimedia. Mesa is an open-source software implementation of OpenGL, Vulkan, and other graphics API specifications. Mesa translates these specifications to vendor-specific graphics hardware drivers.

For detailed installation instructions, refer to

https://rocmdocs.amd.com/en/latest/Installation_Guide/Mesa-Multimedia-Installation.html


## ROCm System Management Information 

The following enhancements are made to ROCm System Management Interface (SMI).

### Support for Printing PCle Information on AMD Instinct™100

AMD ROCm extends support for printing PCle information on AMD Instinct MI100. 

To check the pp_dpm_pcie file, use *"rocm-smi --showclocks"*.

*/opt/rocm-4.0.0-6132/bin/rocm_smi.py  --showclocks*

![Screenshot](https://github.com/Rmalavally/ROCm/blob/master/images/SMI.PNG)


### New API for xGMI 

Rocm_smi_lib now provides an API that exposes xGMI (inter-chip Global Memory Interconnect) throughput from one node to another. 

Refer to the rocm_smi_lib API documentation for more details. 

https://github.com/RadeonOpenCompute/ROCm/blob/master/ROCm_SMI_API_Guide_v4.0.pdf




## AMD GPU Debugger Enhancements

In this release, AMD GPU Debugger has the following enhancements:

* ROCm v4.0 ROCgdb is based on gdb 10.1

* Extended support for AMD Instinct™ MI100 




# Known Issues 

The following are the known issues in this release.

## Upgrade to AMD ROCm v4.0 Not Supported

An upgrade from previous releases to AMD ROCm v4.0 is not supported. A fresh and clean installation of AMD ROCm v4.0 is recommended. 



# Deprecations

This section describes deprecations and removals in AMD ROCm.

## Compiler Generated Code Object Version 2 Deprecation 

**WARNING**

Compiler-generated code object version 2 is no longer supported and will be removed shortly. AMD ROCm users must plan for the code object version 2 deprecation immediately. 

Support for loading code object version 2 is also being deprecated with no announced removal release.

## ROCr Runtime Deprecations

The following ROCr Runtime enumerations, functions, and structs are deprecated in the AMD ROCm v4.0 release.

### Deprecated ROCr Runtime Functions

* hsa_isa_get_info

* hsa_isa_compatible

* hsa_executable_create

* hsa_executable_get_symbol

* hsa_executable_iterate_symbols

* hsa_code_object_serialize

* hsa_code_object_deserialize

* hsa_code_object_destroy

* hsa_code_object_get_info

* hsa_executable_load_code_object

* hsa_code_object_get_symbol

* hsa_code_object_get_symbol_from_name

* hsa_code_symbol_get_info

* hsa_code_object_iterate_symbols


### Deprecated ROCr Runtime Enumerations

* HSA_ISA_INFO_CALL_CONVENTION_COUNT

* HSA_ISA_INFO_CALL_CONVENTION_INFO_WAVEFRONT_SIZE

* HSA_ISA_INFO_CALL_CONVENTION_INFO_WAVEFRONTS_PER_COMPUTE_UNIT

* HSA_EXECUTABLE_SYMBOL_INFO_MODULE_NAME_LENGTH

* HSA_EXECUTABLE_SYMBOL_INFO_MODULE_NAME

* HSA_EXECUTABLE_SYMBOL_INFO_AGENT

* HSA_EXECUTABLE_SYMBOL_INFO_VARIABLE_ALLOCATION

* HSA_EXECUTABLE_SYMBOL_INFO_VARIABLE_SEGMENT

* HSA_EXECUTABLE_SYMBOL_INFO_VARIABLE_ALIGNMENT

* HSA_EXECUTABLE_SYMBOL_INFO_VARIABLE_SIZE

* HSA_EXECUTABLE_SYMBOL_INFO_VARIABLE_IS_CONST

* HSA_EXECUTABLE_SYMBOL_INFO_KERNEL_CALL_CONVENTION

* HSA_EXECUTABLE_SYMBOL_INFO_INDIRECT_FUNCTION_CALL_CONVENTION

   - hsa_code_object_type_t
   
   - hsa_code_object_info_t
   
   - hsa_code_symbol_info_t


### Deprecated ROCr Runtime Structs

* hsa_code_object_t

* hsa_callback_data_t

* hsa_code_symbol_t



## AOMP Deprecation

As of AMD ROCm v4.0, AOMP (aomp-amdgpu) is deprecated. OpenMP support has moved to the openmp-extras auxiliary package, which leverages the ROCm compiler on LLVM 12.

For more information, refer to 

https://rocmdocs.amd.com/en/latest/Programming_Guides/openmp_support.html


# Deploying ROCm

AMD hosts both Debian and RPM repositories for the ROCm v4.0.0 packages. 

For more information on ROCM installation on all platforms, see

https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html


## Machine Learning and High Performance Computing Software Stack for AMD GPU

For an updated version of the software stack for AMD GPU, see

https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html#software-stack-for-amd-gpu



# Hardware and Software Support
ROCm is focused on using AMD GPUs to accelerate computational tasks such as machine learning, engineering workloads, and scientific computing.
In order to focus our development efforts on these domains of interest, ROCm supports a targeted set of hardware configurations which are detailed further in this section.

**Note:** The AMD ROCm™ open software platform is a compute stack for headless system deployments. GUI-based software applications are currently not supported.

#### Supported GPUs
Because the ROCm Platform has a focus on particular computational domains, we offer official support for a selection of AMD GPUs that are designed to offer good performance and price in these domains.

**Note:** The integrated GPUs of Ryzen are not officially supported targets for ROCm.

ROCm officially supports AMD GPUs that use following chips:

* GFX9 GPUs

  - 14 nm "Vega 10 XL" and "Vega 10 XT" chips, which LLVM calls a "gfx900" processor, found on:
    - AMD Radeon RX Vega 56
    - AMD Radeon RX Vega 64
    - AMD Radeon RX Vega 64 Liquid
    - AMD Radeon RX Vega Limited Edition
    - AMD Radeon RX Vega Frontier Edition (Air Cooled)
    - AMD Radeon RX Vega Frontier Edition (Liquid Cooled)
    - AMD Radeon Instinct™ MI25
    - AMD Radeon Pro WX 9100
    - AMD Radeon Pro V340
    - AMD Radeon Pro SSG (Vega, not Polaris)

  - 7 nm "Vega 20" chips, which LLVM calls a "gfx906" processor, found on:
    - AMD Radeon VII
    - AMD Radeon Pro VII
    - AMD Radeon Instinct™ MI50
    - AMD Radeon Instinct™ MI60

* CDNA GPUs

  - 7 nm	"MI100 XL" chips, which LLVM calls a "gfx908" processor, found on:
    - AMD Instinct™ MI100

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
However, they are not enabled in the HIP runtime, and may not work due to motherboard or OEM hardware limitations.
As such, they are not yet officially supported targets for ROCm.

For a more detailed list of hardware support, please see [the following documentation](https://en.wikipedia.org/wiki/List_of_AMD_graphics_processing_units).

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
* AMD "Carrizo" and "Bristol Ridge" APUs are enabled to run OpenCL, but do not yet support HIP or our libraries built on top of these compilers and runtimes.
  * As of ROCm 2.1, "Carrizo" and "Bristol Ridge" require the use of upstream kernel drivers.
  * In addition, various "Carrizo" and "Bristol Ridge" platforms may not work due to OEM and ODM choices when it comes to key configurations parameters such as inclusion of the required CRAT tables and IOMMU configuration parameters in the system BIOS.
  * Before purchasing such a system for ROCm, please verify that the BIOS provides an option for enabling IOMMUv2 and that the system BIOS properly exposes the correct CRAT table. Inquire with your vendor about the latter.
* AMD "Raven Ridge" APUs are enabled to run OpenCL, but do not yet support HIP or our libraries built on top of these compilers and runtimes.
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


# Disclaimer

AMD®, the AMD Arrow logo, AMD Instinct™, Radeon™, ROCm® and combinations thereof are trademarks of Advanced Micro Devices, Inc.

Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.

PCIe® is a registered trademark of PCI-SIG Corporation. Other product names used in this publication are for identification purposes only and may be trademarks of their respective companies.  

Google®  is a registered trademark of Google LLC.

Ubuntu and the Ubuntu logo are registered trademarks of Canonical Ltd.

Other product names used in this publication are for identification purposes only and may be trademarks of their respective companies.

