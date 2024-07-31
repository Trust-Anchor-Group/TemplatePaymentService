Payment Service (Template)
=============================

This repository provides a template solution containing a mock payment service. The solution can be forked by developers who want to 
create a custom payment service for the TAG Neuron(R).

Steps to create a custom payment service
--------------------------------------------

1.  Fork this repository
	* Follow naming conventions for repositories, to make the repository easy to find. A Tag Service running on the TAG Neuron(R) typically
	resides in a repository named `NeuronSERVICE`, where `SERVICE` is a short name for the service being implemented.
2.  Change the solution and project names.
	* Follow naming conventions for libraries, to avoid confusion when navigating code in the Neuron(R): `COMPANY.CATEGORY.SERVICE[.SUBSERVICE]`.
3.  Implement the payment interfaces, as shown in code.
	* Reuse libraries used by the Neuron(R) as much as possible, to simplify distribution and facilitate fixes and updates.
4.  Create Manifest file containing all assembly and content files necessary to install service on a Neuron(R).
5.  Create an installable package that can be distributed and installed on TAG Neurons.
6.  Compile and test on a local development Neuron(R).
7.  Once it works, sign and distribute package on test Neurons, and later production Neurons.
8.  Update project documentation for future developers, following documentation style of similar projects, for recognizability and ease of use.
9.  Append template documentation with useful hints or information, if needed.
10. Provide a correct license for the repository.
