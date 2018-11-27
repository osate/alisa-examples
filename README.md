# ALISA Examples

The following examples are available to illustrate the use of incremental system assurance with ALISA. The capabilities of ALISA are summarized in the [ERTSS 2016 paper](http://www.erts2016.org/uploads/program/paper_13.pdf) and elaborated in the [ALISA online help in OSATE](https://rawgit.com/osate/alisa/develop/org.osate.alisa.help/contents/00-Main.html).

**Note**: Change for SimpleControlSystem. It now uses a separate project called CyberPhysical that contains definitions for physical concepts. See below.

**Note**: We keep a version of the example models consistent with stable releases of OSATE (2.3.5, 2.3.6) in seprate branches. The master branch has the most recent updates, which may require the nightly build version of OSATE to accommodate new features and bug fixes.

## SituationalAwarenessSystem
This is the public release version of a situational Awareness System in AADL. It consists of three projects. 

 * The *SituationalAwarenessCommon* project contains a set of packages and property sets used by the other two projects.
 * The *SituationalAwarenessSystem* project contains the AADL model of the system including a detailed model of pull protocols, and a requirement specification in ReqSpec. The [SEI Tech Report CMU/SEI-2015-SR-031](http://resources.sei.cmu.edu/library/asset-view.cfm?assetid=447184) provides some details about the model. The [SEI Tech Report CMU/SEI-2015-SR-030](http://resources.sei.cmu.edu/library/asset-view.cfm?assetid=447176) summarizes a number of potential integration issues we have identified in the process of creating and analyzing the model. We have also illustrated safety analysis on a primarily software subsystem with this example (see [SEI Tech Report CMU/SEI-2015-SR-032](http://resources.sei.cmu.edu/library/asset-view.cfm?assetid=447189) ).
 * The *SituationalAwarenessRefArch* project illustrates how a reference runtime architecture can be defined and elaborated into a specific situation awareness system.

This set of projects does not depend on *AlisaPredefined*.

## AlisaPredefined
This is a single project that contains a predefined set of categories that can be used on requirements and verification plans.
It also contains a verification method registry for methods that invoke different analysis plug-ins in OSATE.

These definitions are utilized by some projects. In that case you need to check out this project into your workspace. In the future, the definitions will be automatically be included.

## CyberPhysical
This project contains property types, measurement units, and abstract classifiers to represent physical system concepts. 

Initially, it has *Mass*, *ElectricalPower*, *HydraulicFlow*, and *PhysicalForce* as concepts. They are typically used to identify the type of physical interaction through abstract features.

It also defines *Voltage* as property, *Voltage_Type* as type, and *Voltage_Units* as measurement units. Other properties from the *SEI* property set will be moved to this set.

## MultiTierAircraftExample
This is an example of a multi-tier AADL model of an aircraft system. The model originally was developed as a proof of concept demo for the SAVI initiative using AADL V1 (see [SEI Technical Report CMU/SEI-2009-TR-01](http://resources.sei.cmu.edu/asset_files/technicalreport/2009_005_001_435167.pdf) ).

We have translated the model into AADL V2.2. We are using *abstract* components to represent physical resource types, generic *features* as access points for these resources, and *system* to define systems that supply these resources. We have also separated the hardware platform and application software elements of the flight guidance IMA system into two subsystems instead of the original single subsystem, which used the graphcial editor to create a logical, hardware, and electrial supply view of the IMA.

The model represents an aircraft as a physical Tier1 model, elaborates the flight guidance IMA as a tier2 model, subcontracts various flight guidance subsystems, integrqtes the elaborated subsystems as a task and communication model as a tier3 model.

We have associated requirement specifications with the aircraft model across the different tiers and defned verification plans for these requirements. Some requirements are system specific, while others are defined as reusable requirements and verification plans that can be associated with multiple subsystems. Assurance plans configure desirable assurance cases that can be used to automatically execute the verification activities, track the results, and export them in assurance case format.

The following projects make up the example (note that you must also include the *AlisaPredefined* project.

* The *MultiTierAircraft* project is a collection of projects (check out with nested projects checked). They define common elements, the aircraft and flight guidance in multiple tiers, as well as subsystem specifications and supplier elaborations. The top-level packages contain system implementations that can be instantiated and analyzed. They are:
  ** *AircraftSpecified*: Tier1 physical system specification of the aircraft. Supports *mass* (weight) and *electrical power* consumption analysis.
  ** *AircraftIntegrated*: Tier2 model with the flight guidance IMA elaborated into hardware and subsystem specifications. It adds resource budget analysis for processors, memory, and a first cut at an end to end flow latency analysis.
  ** *AircraftImplemented*: Tier3 model with subsystems elaborated with supplier implementations.
  ** The *FlightGuidance" and *FlightGuidanceImplementation* projects support analysis of the embedded software system on its hardware platform. *FlightGuidance* consists of one tier of subsystems and supports resoruce budget analysis as well as end-to-edn flow analysis. It is defined as separate embedded software and hardware platform systems. *FlightGuidanceImplementation* defines a *SubsystemSpec* configuration with supplier specifications for subsystems to demonstrate fucntional integrity checks (domain data types, measurement units, mapping the ARINC429 protocol), a *BuildConfiguration* that elaborates subsystems to the task & communication level, and *IMA* configurations with various levels of software to hardware binding.
* The *Alisa-IntegratorDemo* project contains requirement specifications in *ReqSpec*, verification plans in *Verify*, and assurance plans in *Alisa*. 
* The *Alisa-ADC-Sub1-Demo* project does the same for a supplier. 
* The *Alisa-Utils* projects contains examples of additional verification methods that are written in Jave/Xtend or resolute.

**Note**: This project set depends on *AlisaPredefined*, i.e., you will have to check this project out as well.

## SimpleControlSystem

This example illustrates a variety of user-defined verification methods and is used as the basis for a [tutorial on ReqSpec and Verify](https://github.com/osate/alisa-examples/blob/master/Documentation/BasicRequirementSpecificationGuidance.html).

The example consists of three projects found inside [github.com/osate/alisa-examples/SimpleControlSystem](https://github.com/osate/alisa-examples/tree/master/SimpleControlSystem).

**Note**: This project set depends on *AlisaPredefined* as well as on *CyberPhysical*, i.e., you will have to check those two projects out as well.

