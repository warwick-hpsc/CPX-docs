Running
=====

Setup
------------
Before running a simulation, there are a few setup stages to perform:

* Configure the CPX setup file
* Configure the coupling parameters
* Configure the parameters of the mini-apps

Configuring the CPX setup file
-----------------
The CPX setup file is called 'cpx_input.cfg'. It is used to specify the number of cores to allocate to each mini-app and coupler instance, and to define the setup of the simulation. We will take a look at an example to understand the format:
:: 
   TOTAL 5

   MG-CFD 100
   MG-CFD 100
   SIMPIC 1000

   COUPLER 4
   TYPE SLIDING
   UNIT_1 1
   UNIT_2 2
   
   COUPLER 8
   TYPE OVERSET
   UNIT_1 2
   UNIT_2 3

* The first line must have the keyword 'TOTAL' followed by the total number of instances in the simulation. This value is the sum of the coupler units and mini-app instances. Here, the value is 5, as we are coupling 2 instances of the MG-CFD mini-app, and 1 instance of the SIMPIC mini-app using 2 coupler units.
* The next section defines each of the mini-app instances and the number of MPI ranks associated to each instance. Here we have defined two instances of MG-CFD, each with 100 ranks, and 1 instance of SIMPIC with 1000 ranks.
* The final section defines the coupler units. The first line specifies the number of ranks assocaited with that coupler unit, the second denotes the coupling type, and the third and fourth lines denote which two mini-app units the coupler units are coupling.

This produces the following configuration:

.. image:: figures/CPX_diag.png
  :width: 600
  :alt: An image showing the configuration generated with the above setup file. The diagram consists of 3 boxes, two labelled 'MG-CFD' and one labelled 'SIMPIC'. The boxes have a circle inbetween each which says 'CU' on it, meaning coupler unit. Each circle is labelled, with the first label reading '4 ranks, SLIDING coupling', and the second label reading '8 ranks, OVERSET coupling.
