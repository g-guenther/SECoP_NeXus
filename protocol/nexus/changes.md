# NeXus Definition Changes

The modifications according to the deliverable of WP2 are implemented in the ./protocol/nexus/definitions directory which is a clone of https://github.com/nexusformat/definitions.git. The modifications according to WP2 are sketched in [protocol/nexus/2024_08_SECoP_NeXus_2.pptx](https://github.com/g-guenther/SECoP_NeXus/blob/master/protocol/nexus/2024_08_SECoP_NeXus_2.pptx) (or [./protocol/nexus/2024_08_SECoP_NeXus_2.pdf](https://github.com/g-guenther/SECoP_NeXus/blob/master/protocol/nexus/2024_08_SECoP_NeXus_2.pdf)), respectively. Some modifications were discussed at https://github.com/jkotan/secop-file-examples/issues.

Clone the SECoP repository to a local source and open the file definitions/build/manual/build/html/index.html in your browser, e.g. using the command 'firefox protocol/nexus/definitions/build/manual/build/html/index.html', to browse the modified NeXus documentation.

The following changes were applied:

- adding humidity, viscosity, and concentration to measurement field of NXsensor
- adding missing NXsensor/measurement values to NXsample; the following data fields were added to NXsample:
  - pH (adding NX_MOLAR_DENSITY to units, see nxdlTypes.xsd)
  - conductivity (adding NX_CONDUCTIVITY to units, see nxdlTypes.xsd)
  - resistance (adding NX_RESISTANCE to units, see nxdlTypes.xsd)
  - voltage
  - flow (adding NX_FLOW to units, see nxdlTypes.xsd)
  - strain
  - shear
  - surface_pressure
  - humidity
  - viscosity
- adding corresponding environment groups to NXsample:
  - electric_field_env
  - stress_field_env
  - pressure_env
  - pH_env
  - voltage_env
  - flow_env
  - strain_env
  - shear_env
  - surface_pressure_env
  - humidity_env
  - concentration_env
  - conductivity
  - resistance
  - viscosity
- adding (arbitrary) ENVIRONMENT groups to NXsample
- adding description field to NXsensor
- adding target_value_log group to NXsensor for sensor settings/nominal values
- adding @PID attribute to NXsensor/measurement field (to contain SECoP's meaning/link)
- adding @long_name attribute to NXsensor/measurement field (to contain SECoP's meaning/key)

---------------------------------------
As a result, the free structure of sample environments in this definition is supported by
  - any number of NXenvironments (SECoP nodes) in NXsample
  - any number of NXsensors (SECoP parameters) in NXenvironment
  - any number of NXlogs (any SECoP data fields) can be added anywhere as a NeXus design principal, see build/manual/build/html/design.html

NOT added:
  - explicit field status_log to NXsensor because NXlog values must be numbers and, I guess, the status of a sensor could be either a number or a string (like 'idle')
  - other typical SECoP fields such as meaning/importance because they are rather characteristic for SECoP; there names, arrangement and values should be defined separately by SECoP 

Two more general things:
- There was a discussion about adding a separate NXsample group for sample environment (which I don't like so much because 2 NXsample groups could introduce some ambiguity). However, the changes made to NXsensor and NXsample are required independently of realisation.
- In a recent discussion with Peter possible problems become apparent when arranging SE (meta)data automatically (e.g. by script) since HDF could not handle arrays of mixed types (e.g. strings and floats). As a result, complex data types could cause errors in such a script. It could be required that SECnodes deliver additionally a recommendation about how its data should be stored/arranged.
