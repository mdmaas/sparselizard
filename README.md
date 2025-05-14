# Martin's installation notes

### Step 1: install external libraries using the sh scripts.

Note: I had to update the gmsh version to 4.13.1 in optional_install_gmsh.sh, because the hardcoded version was 4.5.X, which is not compatible with the examples using cohomology bases.

### Step 2: Build

`` sh
mkdir -p build
cd build
cmake ..
cmake --build . -j$(nproc)
``

### Step 3: Add the libraries to the LD_LIBRARY_PATH

`` sh
export LD_LIBRARY_PATH="$HOME/SLlibs/petsc/arch-linux-c-opt/lib:$HOME/SLlibs/gmsh/lib:$LD_LIBRARY_PATH"
``

### Step 4: Run the simulation

The simulation binaries are located in the build folder. You can run them directly from there. For example, to run the "example" simulation, you would do:

`` sh
cd build
cd simulations
cd default
./default
``


# Add project

Simulation projects are located under `simulations`.
In order to create a new simulation:

1. Copy `simulations/default` folder with different name. Let's say that the new folder is
   `simulations/newsim`
1. Replace target name `default` with the new one in `simulations/newsim/CMakeLists.txt`
1. Add line `add_subdirectory(newsim)` to `simulations/CMakeLists.txt`
1. Configure and build. Executable file will be located in `build/simulations/newsim` folder



# Improved cmake build system in this PR

Tried to merge this PR with a new cmake build system that uses system packages instead of custom shell scripts
https://github.com/halbux/sparselizard/pull/66

I could not get the latest version of gmsh using the system package manager as I am on Ubuntu 22, so I had to use the custom sh script to install gmsh. The PR could be probably merged and the custom sh scripts removed if you are on a newer version of Ubuntu or other distro that has the latest gmsh version in the system package manager.
