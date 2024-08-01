Payment Service (Template)
=============================

This repository provides a template solution containing a mock payment service. The solution can be forked by developers who want to 
create a custom payment service for the TAG Neuron(R).

Steps to create a custom payment service
--------------------------------------------

1.  Fork this repository
	* Follow naming conventions for repositories, to make the repository easy to find. A Tag Service running on the TAG Neuron(R) typically
	resides in a repository named `NeuronSERVICE`, where `SERVICE` is a short name for the service being implemented.
	* It has been assumed the repository will be cloned to `C:\My Projects\TemplatePaymentService`, see build events below.

2.  Change the solution and project names, as well as the corresponding *manifest file* (see below).
	* Follow naming conventions for libraries, to avoid confusion when navigating code in the Neuron(R): `COMPANY.CATEGORY.SERVICE[.SUBSERVICE]`.

3.  Update the *post build events*, to match the folder and project names you will use.

4.  [Install a Neuron](https://lab.tagroot.io/Documentation/Neuron/InstallBroker.md) on your development machine, that you can use for debugging 
	and testing.
	* Make sure the *IoT Broker* Windows Service is not started (Disabled or Manual), and does not start automatically. You will start it from the
	Visual Studio when debugging. Stop the service if it started automatically after installation.
	* Update the *post build events* so they refer to the tools available in the Neuron installation folder.
	* Alternatively, clone the [IoT Gateway repository](https://github.com/PeterWaher/IoTGateway) and compile it. In the post build events, it is 
	assumed it is cloned to `C:\My Projects\IoT Gateway`. It �lso contains the tools referenced from the build script to generate packages.
	
5.  Make the payment service the default *Startup Project*, and edit its *Debug Launch Profile* from *project properties*, so the folders match
	the folders your Neuron was installed at.

6.  Compile and run the template service. Make sure the console version of the Neuron is started. Once started, go to the administation page
	and make sure the *Payment Template* button is available in the *Software* section.

7.  Implement the payment interfaces, as shown in code.
	* Reuse libraries used by the Neuron(R) as much as possible, to simplify distribution and facilitate fixes and updates.
	* Go through all comments in code marked with `TODO`.

8.  Update the Manifest file so it contains all referenced assemblies and content files necessary to install service on a Neuron(R). You do
	not need to reference assemblies or content files that are part of the Neuron(R) distribution itself.

9.  Create an installable package that can be distributed and installed on TAG Neurons.

10. Compile and test on a local development Neuron(R).

11. Once it works, sign and distribute package on test Neurons, and later production Neurons.

12. Update project documentation for future developers, following documentation style of similar projects, for recognizability and ease of use.

13. Append template documentation with useful hints or information, if needed.

14. Provide a correct license for the repository.

## Projects

The solution contains the following C# projects:

| Project                      | Framework         | Description |
|:-----------------------------|:------------------|:------------|
| `TAG.Payments.Template`      | .NET Standard 2.0 | Payment Mock service that works as a good starting point for developing new payment services for the TAG Neuron(R). |

## Nugets

The following external nugets are used. They faciliate common programming tasks, and enables the service to be hosted on the 
[TAG Neuron](https://lab.tagroot.io/Documentation/Index.md) without conflicts. For a list of general nugets available that can
be used, see the [IoT Gateway repository](https://github.com/PeterWaher/IoTGateway).

| Nuget                                                                              | Description |
|:-----------------------------------------------------------------------------------|:------------|
| [Paiwise](https://www.nuget.org/packages/Paiwise)                                  | Contains services for integration of financial services into Neurons. |
| [Waher.Content](https://www.nuget.org/packages/Waher.Content/)                     | Pluggable architecture for accessing, encoding and decoding Internet Content. Include nugets named `Waher.Content.*` to access features of specific Content Types. |
| [Waher.Events](https://www.nuget.org/packages/Waher.Events/)                       | An extensible architecture for event logging in the application. |
| [Waher.IoTGateway](https://www.nuget.org/packages/Waher.IoTGateway/)               | Contains the [IoT Gateway](https://github.com/PeterWaher/IoTGateway) hosting environment. |
| [Waher.Networking](https://www.nuget.org/packages/Waher.Networking/)               | Tools for working with communication, including troubleshooting. Include nugets named `Waher.Networking.*` if you need support for specific communication protocols. |
| [Waher.Runtime.Inventory](https://www.nuget.org/packages/Waher.Runtime.Inventory/) | Maintains an inventory of type definitions in the runtime environment, and permits easy instantiation of suitable classes, and inversion of control (IoC). |
| [Waher.Runtime.Settings](https://www.nuget.org/packages/Waher.Runtime.Settings/)   | Provides easy access to persistent settings. |

## Installable Package

To create a package, that can be distributed or installed, you begin by creating a *manifest file*. The
`TAG.Payments.Template` project has a manifest file called `TAG.Payments.Template.manifest`. It defines the
assemblies and content files included in the package. You then use the `Waher.Utility.Install` and `Waher.Utility.Sign` command-line
tools in the [IoT Gateway](https://github.com/PeterWaher/IoTGateway) repository, to create a package file and cryptographically
sign it for secure distribution across the Neuron network.

## Building, Compiling & Debugging

The repository assumes you have the [IoT Gateway](https://github.com/PeterWaher/IoTGateway) repository cloned in a folder called
`C:\My Projects\IoT Gateway`, and that this repository is placed in `C:\My Projects\TemplatePaymentService`. You can place the
repositories in different folders, but you need to update the build events accordingly. You can also use an installed Neuron(R)
on your development machine, and use it instead of the IoT Gateway. If you do so, you need to update the build events and debug
profiles to match the installation folder. To run the application, you select the `TAG.Payments.Template` project as your startup 
project. It will execute the console version of the [IoT Gateway](https://github.com/PeterWaher/IoTGateway), and make sure the compiled 
files of the `TemplatePaymentService` solution is run with it.

### Gateway.config

To simplify development, once the project is cloned, add a `FileFolder` reference
to your repository folder in your [gateway.config file](https://lab.tagroot.io/Documentation/IoTGateway/GatewayConfig.md). 
This allows you to test and run your changes to Markdown and Javascript immediately, 
without having to synchronize the folder contents with an external 
host, or recompile or go through the trouble of generating a distributable software 
package just for testing purposes. Changes you make in .NET can be applied in runtime
if you the *Hot Reload* permits, otherwise you need to recompile and re-run the
application again.

Example of how to point a web folder to your project folder:

```
<FileFolders>
  <FileFolder webFolder="/Template" folderPath="C:\My Projects\TemplatePaymentService\TAG.Payments.Template\Root\Template"/>
</FileFolders>
```

**Note**: Once the file folder reference is added, you need to restart the Neuron(R) for the change to take effect.

**Note 2**:  Once the Neuron(R) is restarted, the source for the files is taken from the new location. Any changes you make 
in the corresponding `ProgramData` subfolder will have no effect on what you see via the browser.

**Note 3**: This file folder is only necessary on your developer machine, to give you real-time updates as you edit the files in your
development folder. It is not necessary in a production environment, as the files are copied into the correct folders when the package 
is installed.
