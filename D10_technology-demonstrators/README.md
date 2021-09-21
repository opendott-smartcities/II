# 2.1 (D10) Technology Demonstrators

> This deliverable will be an output of T2.1, in which ESRs work with OFFINN to develop a deeper understanding of specific open prototyping technology that is applicable to their chosen domain (e.g. IoT-capable Arduinos, Mozilla Voice, Raspberry Pi).
> Documentation will take the form of source code, files for digital fabrication, videos, Instructables, etc., as appropriate.

The training on Open Hardware provided by Officine Innesto happened in two stages. The first one was an overview of what can be accomplished with open source hardware, whilst the second was hands-on and focused on turning our concepts into prototypes. This second part took place about the same time as I was conducting the workshops of the [reuse.city co-design lab](../D13_deployment-datasets/reuse-city). Such a timeframe proved perfect, as I was able to discuss improvements to the concept ideas with participants of the lab at the same time as I would learn and experiment about the possibilities and limits of current technology.

The technology demonstrators in this folder are modules that can be assembled to build a prototype named "E-I", as in "evaluation interface". The [concept idea](../D11_co-designed-concepts) in which E-I is based sees it taking different shapes: an app for mobile devices, a workbench machine, or a larger kiosk form-factor to be deployed in public spaces. User would present different objects to be assessed by E-I, whose screen would display information about the value and potential of reuse of said objects.

E-I is a speculative device, which relies both on the availability of trusted data and on the ability to recognise objects. Neither is feasible yet, at least universally. For prototyping purposes, though, the features of E-I can be simulated with a limited set of objects.

The [prototype](../D12_documentation-of-prototypes) the demonstrators on this folder relate to is the workbench version. It is composed of an articulated arm with a camera, attached to a display. Some sensors attached to a Raspberry Pi provide the desired functionality.

This folder consists of the following:

 - [References](references.md) about the hardware and software used for the prototype.
 - [E-I_NFC](E-I_NFC): Arduino code to recognise NFC tags using a GROVE NFC module, and send their identifier to the Raspberry Pi.
 - [E-I_node](E-I_NFC): Export of node-red flows that will:
    - Turn the display on when an object is put near the machine;
    - Display on the machine what is captured by the camera;
    - Receive the identifiers from the NFC sensor when the object's NFC tags are recognised;
    - Play an audio signal when a NFC tag is recognised.
    - Display different information on a web page each time a different NFC tag is recognised.

The node-red flows included here feature a simple web page displaying local information. At a later stage of prototyping it was decided to use a separate website for that purpose, whose documentation can be found on [this folder](../D12_documentation-of-prototypes/thingwiki).
