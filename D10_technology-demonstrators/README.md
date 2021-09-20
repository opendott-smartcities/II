# 2.1 (D10) Technology Demonstrators

> This deliverable will be an output of T2.1, in which ESRs work with OFFINN to develop a deeper understanding of specific open prototyping technology that is applicable to their chosen domain (e.g. IoT-capable Arduinos, Mozilla Voice, Raspberry Pi).
> Documentation will take the form of source code, files for digital fabrication, videos, Instructables, etc., as appropriate.

The Open Hardware training module took place about the same time as the reuse.city co-design lab. Such a timeframe proved perfect, as I was able to discuss improvements to the concept ideas with participants of the lab at the same time as I would learn about the possibilities and limits of technology.

The technology demonstrators in this folder are modules that can be assembled to build a prototype named "E-I", as in "evaluation interface". The [concept idea](../D11_co-designed-concepts) in which E-I is based sees it taking different shapes: an app for mobile devices, a workbench machine, or a larger kiosk form-factor to be deployed in public spaces.

The [prototype](../D12_documentation-of-prototypes) these demonstrators relate to is the workbench version. It is composed of an articulated arm with a camera, attached to a display. A minicomputer (Raspberry Pi) and sensors are also present, and can be either hiden or exposed. The user would present different objects to be assessed by E-I, whose screen would display information about the value and potential of reuse of said objects.

The contents of this folder consists of the following:

 - [References](references.md) about the hardware and software used for the prototype.
 - [E-I_NFC](E-I_NFC): Arduino code to recognise NFC tags using a GROVE NFC module, and send their identifier to the Raspberry Pi.
 - [E-I_node](E-I_NFC): Export of node-red flows that will:
    - Turn the display on when an object is put near the machine;
    - Display on the machine what is captured by the camera;
    - Receive the identifiers from the NFC sensor when the object's NFC tags are recognised;
    - Play an audio signal when a NFC tag is recognised.
    - Display a different web page each time a different NFC tag is recognised.
