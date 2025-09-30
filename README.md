# LineageOS Kernel Source Code for Sony Xperia with Qualcomm Snapdragon 888 (SM8350)

**PLEASE NOTE THAT THE ORIGINAL `README` WAS RENAMED AS `README.old`, THE SAME APPLIES FOR THE `README.md`**

## Disclaimer

  - I am **NOT** responsible for bricked devices, dead SD cards, thermonuclear war, or you getting fired because the alarm app failed.

  - Please do some research if you have any concerns about it before flashing anything!

  - **YOU** are choosing to make these modifications; I AM NOT RESPONSIBLE for any consequences.

## My purpose of creating this fork

  - Add a `build.sh` to automate the building process for my Sony Xperia 1 III

  - Add a new `README` to help those who want to build their own kernel from source

## Prerequisites

  - 1. A GNU/Linux operating system (I am using Gentoo Linux) and your advanced knowledge of it

  - 2. The corresponding phone that have the latest LineageOS installed

  - 3. The toolchain for cross-compiling (in this case, we need `aarch64-linux-gnu` for 64-bit ARM architecture since Android has deprecated 32-bit support in 2023)

  - 4. **Your capability** to recover your phone to a working state if **you have it bricked**

## Reminder

 - This copy of the kernel source code is provided by LineageOS and **MAY** only work with the latest LineageOS build of the corresponding phone

## Instrcutions to build

  - 1. Install all dependencies and necessary toolchain from your distro's software repository

      - For Gentoo Linux, you will need to follow the [instructions](https://wiki.gentoo.org/wiki/Crossdev) of using `sys-devel/crossdev` to build the toolchain

      - For Debian-based distros such as Ubuntu, you can refer to related guides to install all essential packages

      - For Arch-based distros, you might already know what to do  :)

  - 2. Download or clone this copy of the kernel source code

  - 3. Start to build

      - Automated approach (via `build_<codename>.sh`)

          *`pdx215` for Sony Xperia 1 III, and `pdx214` for Sony Xperia 5 III*

          > Feel free to modify the given `build_<codename>.sh` to suit your device and environment
    
          - 1. Navigate to the top-level directory of the kernel source
        
          - 2. Make sure `build_<codename>.sh` is executable
        
              > If not, run `chmod +x build_<codename>.sh` to make it executable

          - 3. Execute `build_<codename>.sh` to start
        
          - 4. If no error generated, the kernel image and dtb will be available in `out/arch/arm64/boot/`
          
          - 5. Proceed to pack the kernel via `AnyKernel3` or other methods like `mkbootimg` if you prefer, and flash it to your device to test

      - Manual approach

          - 1. Navigate to the top-level directory of the kernel source
        
          - 2. Set environment variables for the toolchain
  
              ```bash
              export LLVM=1    # Use Clang as the compiler
              export ARCH=arm64    # Set target architecture to ARM 64-bit
              export SUBARCH=arm64     # Set target sub-architecture to ARM 64-bit
              export LTO=thin    # Use ThinLTO for better performance and smaller binary size
              export CROSS_COMPILE=aarch64-linux-gnu-   # Set the cross-compiler
              ```

              > Make sure you have the toolchain added to your `PATH`

          - 3. Generate the default configuration file for your device

              ```bash
              make O=out <codename>_defconfig    # Generate the default configuration file in `out`
              ```

              > Note that all default configuration files are located in `arch/arm64/configs/`

          - 4. Start the compilation
        
              ```bash
              make O=out -j$(nproc)    # Compile the kernel with all available threads
              ```
        
          - 5.   ----- THE SAME AS STEP 4 AND 5 ABOVE -----
        
## Integration of KernelSU and its derivatives

  Their developers have done an excellent job on composing the self-explanatory documentation, refer to their respective GitHub repositories for more information.
