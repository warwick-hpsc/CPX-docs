Build
=====

Context
------------
CPX is currently designed to allow you to couple three mini-apps:

* MG-CFD, a CFD mini-app
* SIMPIC, an Eulerian-Lagrangian Particle mini-app
* FEniCS, a Finite-Element library

In all of our internal testing, we have coupled CFD with either SIMPIC or FEniCS, as our test cases all make use of CFD. As a reuslt, CPX currently exists as an extension of the MG-CFD mini-app, however we have plans in the future to create a standalone repository.

.. _install:

Core Installation
-----------------

The CPX code can be retrieved from the `feature/coupler' branch of the MG-CFD GitHub:

.. code-block:: potato

   $ git clone --branch feature/coupler https://github.com/warwick-hpsc/MG-CFD-app-OP2.git
   
As CPX is currently an extension of the MG-CFD mini-app, you will need to build this mini-app to use CPX. Note that you can run simulations without MG-CFD (e.g coupling FEM-FEM), but MG-CFD will still need to be built first. First, build the following libraries:

* HDF5, a data format library
* Parmetis, a paritioner
* PT-Scotch, another partitioner
* ParHIP, another partitioner

These are all available online and building them is a fairly standard, either using make or CMake.

These libraries are used to build OP2, an unstructured mesh DSL which allows MG-CFD to use different hardware or parallel programming models without having write new code in the applications themselves. It can be found in the OP2 repo in the warwick-hpsc collection. To build OP2, a number of environment variables must be set, which include variables to the libraries mentioned above as well as the compiler to use. These can be seen by looking at the OP2 Makefiles in the library source directory.

Finally, clone the `feature/coupler' branch of the MG-CFD and build CPX using:
::
    $ COMPILER=x make mpi_cpx
   
where x is your choice of compiler. Supported compilers are available in the Makefile. You can now run coupled MG-CFD units with each other.

SIMPIC Installation
-----------------
To enable coupling between SIMPIC and MG-CFD, you need to build the SIMPIC library. This is located in the simpic folder in the main CPX directory, and can be built by running the command:
::
    $ make lib

This will build a library called libsimpic.a. To link with CPX, set the following environment variables:
::
    export SIMPIC=1
    export SIMPIC_INSTALL_PATH=/path/to/library

Finally, rebuild CPX by running the final command in the core installation section. You can now run coupled simulations with the SIMPIC mini-app.

FEniCS Installation
-----------------
To enable coupling between FEniCS and MG-CFD, you need to build the FEniCS library. This is located in the dolfinx folder in the main CPX directory, to build FEniCS you need to first build the following libraries:

* HDF5, a data format library
* FEniCSx, a FEM solver
* Boost, with Timer library
* Petsc, a PDE solver
* Parmetis, a paritioner
* PT-Scotch, another partitioner
* Cmake, a build manager

Then the FEniCS library can be built by running the following commands in the dolfinx folder:
::
    mkdir build
    cd build
    cmake ..
    make
    
This will build a library called libdolfinx.a in the bin directory. To link with CPX, set the following environment variables:
::
    export FENICS=1
    export PETSC_INSTALL_PATH=/path/to/install
    export DOLFINX_INSTALL_PATH=/path/to/install
    export BOOST_INSTALL_PATH=/path/to/install

Finally, rebuild CPX by running the final command in the core installation section. You can now run coupled simulations with the FEniCS mini-model.
