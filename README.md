Payment Service (Template)
=============================

This repository provides a template solution containing a mock payment service. The solution can be forked by developers who want to 
create a custom payment service for the TAG Neuron(R).

Steps to create a custom payment service
--------------------------------------------

1.  Fork this repository
2.  Change the solution and project names.
	* Follow naming conventions for libraries, to avoid confusion when navigating code in the Neuron(R): `COMPANY.CATEGORY.FUNCTION[.SUBFUNCTION]`.
3.  Implement the payment interfaces, as shown in code.
4.  Create Manifest file containing all assembly and content files necessary to install service on a Neuron(R).
5.  Create an installable package that can be distributed and installed on TAG Neurons.
6.  Compile and test on a local development Neuron(R).
7.  Once it works, sign and distribute package on test Neurons, and later production Neurons.
8.  Update project documentation for future developers.
9.  Append template documentation with useful hints or information, if needed.
10. Provide a correct license for the repository.
