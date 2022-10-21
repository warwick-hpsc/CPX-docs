Usage
=====

Context
------------
CPX is currently designed to allow you to couple three mini-apps:

* MG-CFD, a CFD mini-app
* SIMPIC, an Eulerian-Lagrangian Particle mini-app
* FEniCS, a Finite-Element library

In all of our internal testing, we have coupled CFD with either SIMPIC or FEniCS, as our test cases all make use of CFD. As a reuslt, CPX currently exists as an extension of the MG-CFD mini-app, however we have plans in the future to create a standalone repository.

.. _installation:

Installation
------------

The CPX code can be retrievd from the `feature/coupler' branch of the MG-CFD GitHub:

.. code-block:: console

   $ git clone --branch feature/coupler https://github.com/warwick-hpsc/MG-CFD-app-OP2.git
   
 



