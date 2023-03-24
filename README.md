# 5G Standalone Registration

Standalone Access Registration is the process by which a device registers with a 5G network to gain access to its services. It involves various registration procedures, messages, and security measures to ensure authorized access and mutual authentication.

The "5G-NR RRC Connection Setup" sequence describes the steps involved in setting up a radio connection between a User Equipment (UE) and a 5G Node B (gNB). The sequence includes actions and messages exchanged between the UE and the gNB, such as the transmission of a preamble, allocation of temporary and dedicated Radio Network Temporary Identifiers (RNTIs), exchange of various control messages (Random Access Response, RRC Setup Request, RRC Setup Complete), and the setup of signaling and radio bearers. The ultimate goal of the sequence is to establish a radio connection and bring the UE into the `RRC_CONNECTED` state, allowing the UE to access the 5G network.

## Generating with EventStudio System Designer

The sequence diagrams have been generated using [EventStudio System Designer](https://www.eventhelix.com/EventStudio/). You will need to install the EventStudio extension for Visual Studio Code to view the diagrams. The extension can be downloaded from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=EventHelix.EventStudio).

## Feature Description File (FDL)

The sequence diagram is generated from the [5G Standalone Registration FDL file](model/5g-standalone-access-registration.FDL). The FDL file is a text file that describes the sequence diagram. It is written in a simple language that is easy to understand and modify. The FDL file is compiled by [EventStudio System Designer](https://www.eventhelix.com/EventStudio/) to generate the sequence diagram.

## Message Details in Markdown

When you click on a message in the sequence diagram, you see details about the message.

The message details are generated from the [5G Standalone Registration Markdown file](message-details/5g-standalone-access-registration.md).

## Help improve this sequence diagram

If you find any errors or omissions in this sequence diagram, please [create an issue](https://github.com/eventhelix/5g-nr-standalone/issues).






