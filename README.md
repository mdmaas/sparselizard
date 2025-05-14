# Build instructions

Run the scripts in the 'install_external_libs' folder then configure and build:
```bash
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc)
```

---

Provide a custom path to the petsc, gmsh (optional) or mpi (optional) folder with:
```bash
cmake .. -DPETSC_PATH=/yourpath/petsc -DGMSH_PATH=/yourpath/gmsh -DMPI_PATH=/yourpath/mpi
```

It may be convenient to use the cmake GUI:
```bash
cmake-gui
```

# Add project

Simulation projects are located under `simulations`.
In order to create a new simulation:

1. Copy `simulations/default` folder with different name. Let's say that the new folder is
   `simulations/newsim`
1. Replace target name `default` with the new one in `simulations/newsim/CMakeLists.txt`
1. Add line `add_subdirectory(newsim)` to `simulations/CMakeLists.txt`
1. Configure and build. Executable file will be located in `build/simulations/newsim` folder



# Martin's installation notes

## Step 1: install external libraries using the sh scripts.

Note: I had to update the gmsh version to 4.13.1 in optional_install_gmsh.sh, because the hardcoded version was 4.5.X, which is not compatible with the examples using cohomology bases.

## Step 2: Create new simulation from the examples

clone the "default" simulation, and create a new folder with the main.cpp from the desired example.

## Step 3: Build

`` sh
mkdir -p build
cd build
cmake ..
cmake --build . -j$(nproc)
``

## Step 4: Add the libraries to the LD_LIBRARY_PATH
export LD_LIBRARY_PATH="$HOME/SLlibs/petsc/arch-linux-c-opt/lib:$HOME/SLlibs/gmsh/lib:$LD_LIBRARY_PATH"

## Step 5: Run the simulation

The simulation binaries are located in the build folder. You can run them directly from there. For example, to run the "example" simulation, you would do:

`` sh
cd build
cd simulations
cd default
./default
``
