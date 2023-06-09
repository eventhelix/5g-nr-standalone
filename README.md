# 5G Standalone Registration

Standalone Access Registration is the process by which a device registers with a 5G network to gain access to its services. It involves various registration procedures, messages, and security measures to ensure authorized access and mutual authentication.

## 5G-NR Standalone Access Registration
The [5G-NR  Standalone Access Registration](https://eventhelix.com/5g/standalone-access-registration/) sequence describes the steps involved in setting up a radio connection between a User Equipment (UE) and a 5G Node B (gNB). The sequence includes actions and messages exchanged between the UE and the gNB, such as the transmission of a preamble, allocation of temporary and dedicated Radio Network Temporary Identifiers (RNTIs), exchange of various control messages (Random Access Response, RRC Setup Request, RRC Setup Complete), and the setup of signaling and radio bearers. The ultimate goal of the sequence is to establish a radio connection and bring the UE into the `RRC_CONNECTED` state, allowing the UE to access the 5G network.

## Generating with EventStudio System Designer

The sequence diagrams have been generated using [EventStudio System Designer](https://www.eventhelix.com/EventStudio/). You will need to install the EventStudio extension for Visual Studio Code to view the diagrams. The extension can be downloaded from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=EventHelix.EventStudio).

## Feature Description File (.FDL)

The sequence diagram is generated from the [5g-standalone-access-registration.FDL](model/5g-standalone-access-registration.FDL). The FDL file is a text file that describes the sequence diagram. It is written in a simple language that is easy to understand and modify. The FDL file is compiled by [EventStudio System Designer](https://www.eventhelix.com/EventStudio/) to generate the sequence diagram.

EventStudio System Designer can generate multiple sequence diagrams from a single FDL file. The desired diagram types are specified in the [project.scn.json](project.scn.json) file.

## Project file (project.scn.json)

The [project.scn.json](project.scn.json) is a project file that defines the different documents that should be generated from [5g-standalone-access-registration.FDL](model/5g-standalone-access-registration.FDL).

Each document is generated by specifying a JSON description for the document to be generated. The following fields may be specified for each document defined in the project file:


| Field | Description |
| --- | --- |
| `"documentFormat"` | Choose between "pdf" and "emf" (MS Word Picture format) Note: documentFormat defaults to "pdf" when omitted for a document. |
| `"documentName"` | Defines the file name for the document |
| `"documentType"` | Choose between `"sequence-diagram"` and `"context-diagram"` Note: documentType defaults to "sequence-diagram" when omitted. |
| `"interactionLevel"` | Specify this option to define a high level sequence diagram at `"system"`, `"subsystem"`, `"module"` or `"component"` level. |
| `"interfaceFilter"` | Specify this option to limit the sequence diagram to interactions involving a specified object, component, module, subsystem, system or their respective type specifications. |
| `"defines"` | Specify the preprocessor defines that are specific to [5g-standalone-access-registration.FDL](model/5g-standalone-access-registration.FDL). For example, the file defines `UE_ONLY`, `GNB_ONLY`are used to fine tune the output for documents generateed with `"interfaceFilter"` set to  `"UE"`and `"GNB"` respectively. In addition to application specific defines, layout related defines may also be specified. The layout specific defines can be found in [inc.FDL](include/inc.FDL) file. For example, `POSTER` and `PRESENTATION` formats can be selected by adding them to the defines. |

The following documents are generated in PDF format:

* Complete sequence diagram (`5g-standalone-access-registration.pdf`)
* UE sequence diagram (`UE.pdf`)
* gNB sequence diagram (`gNB.pdf`)
* AMF sequence diagram (`AMF.pdf`)
* PCF sequence diagram (`PCF.pdf`)
* AUSF sequence diagram (`AUSF.pdf`)
* UDM sequence diagram (`UDM.pdf`)
* SMF sequence diagram (`SMF.pdf`)
* UPF sequence diagram (`UPF.pdf`)
* AMF context diagram (`amf-context-diagram.pdf`)

In addition to the above documents a `documents.html` file is generated that contains links to all the generated documents.

## Message Details in Markdown

When you click on a message in the sequence diagram, you see details about the message.

The message details are generated from the [5G Standalone Registration Markdown file](message-details/5g-standalone-access-registration.md).

The message detail file path should be specified by the `HYPERLINK` define in the [5g-standalone-access-registration.FDL](model/5g-standalone-access-registration.FDL) file.

```
#define HYPERLINK https://www.eventhelix.com/5G/standalone-access-registration/details/5g-standalone-access-registration.html
```


## Help improve this sequence diagram

If you find any errors or omissions in this sequence diagrams, please [create an issue](https://github.com/eventhelix/5g-nr-standalone/issues).

When reporting an issue, please include the 3GPP specification that describes the message or procedure.






