# 2.1 (D10) Technology Demonstrators

> This deliverable will be an output of T2.1, in which ESRs work with OFFINN to develop a deeper understanding of specific open prototyping technology that is applicable to their chosen domain (e.g. IoT-capable Arduinos, Mozilla Voice, Raspberry Pi).
> Documentation will take the form of source code, files for digital fabrication, videos, Instructables, etc., as appropriate.

This folder contains technological demonstrators developed during the second year of PhD research on Smart Cities within the OpenDoTT project (Open Design of Trusted Things). OpenDoTT is a PhD programme from Northumbria University and the Mozilla Foundation funded by the European Union / Horizon 2020 / Marie Skłodowska-Curie programme.

The PhD research focuses on waste prevention through collective practices of reuse, in the forms of repair, upcycling and re-circulation. It investigates the confluence of initiatives and policies in themes such as zero waste, social innovation, circular economy and the doughnut economy.

The contents of this folder range from sketches and schematics of open hardware to software used to explore the prototyping of technologies for reuse of materials.

## Context

As scheduled for the second year of PhD research, training on Open Hardware was provided by Officine Innesto. It had two stages. The first one was an overview of what can be accomplished with open source hardware, whilst the second was hands-on and focused on turning the research concepts into prototypes. This second part took place about the same time as I was conducting the workshops of the reuse.city co-design lab(../D13_deployment-datasets/reuse-city). Such a timeframe proved positive, as I was able to discuss improvements to the concept ideas with participants of the lab at the same time as I would learn and experiment about the possibilities and limits of current technologies.

The technology demonstrators in this folder are modules that can be assembled to build a prototype named "E-I", short for "evaluation interface". The concept idea(../D11_co-designed-concepts) in which E-I is based sees it taking different shapes: an app for mobile devices, a workbench machine, or a larger kiosk form-factor to be deployed in public spaces. Its user would present different objects to be assessed by E-I, whose screen would then display information about the value and potential of reuse of said objects.

E-I, short for Evaluation Interface, is a combination of speculative technologies conceived to help society reuse discarded materials. It addresses the following Research Questions:
1. What are the skills and abilities involved in the reuse of materials?
  1.1. Can those skills they be augmented and replicated with the aid of digital systems?
  1.2. What kind of hardware and software would contribute to make that happen?
  
The main purpose of E-I  is allowing users to assess the potential value of materials. E-I does that by identifying objects and parsing them against an open database with information relevant for evaluating and reusing said objects.

The prototype(../D12_documentation-of-prototypes) explored with the demonstrators on this folder relate to is the workbench version. It is composed of an articulated arm with a camera. Some sensors and a touchscreen display attached to a Raspberry Pi single-board computer provide the desired functionality.

This folder consists of the following:

 - E-I_overview.pdf - description and specifications of the exploratory version of E-I.
 - doc.txt: Technical documentation of the modules.
 - E-I_NFC: Arduino code to recognise NFC tags using a GROVE NFC module, and send their identifiers via USB to the Raspberry Pi.
 - E-I_node: Node-RED flows in JSON format that will:
    - Display on the machine the image that is captured by the camera;
    - Receive the identifiers from the NFC sensor when the object's NFC tags are recognised;
    - Display different information on a web page each time a different NFC tag is recognised.
 - notes.txt: Notes made while developing and improving the demonstrators and prototype.
 - references.txt: Further references about the hardware and software used for the prototype.

The Node-RED flows included here serve a dashboard that embeds the contents of a web page for each object. As the prototyping phase progressed, it was decided to use a separate website for that purpose, whose documentation can be found on the proper folder(../D12_documentation-of-prototypes/thingwiki).

---

The researcher is available for contact by email: f.fonseca@northumbria.ac.uk

This project has received funding from the European Union’s Horizon 2020 research and innovation programme under the Marie Skłodowska-Curie grant agreement No 813508.
