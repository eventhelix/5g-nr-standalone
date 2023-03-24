
# 5G Standalone Access Registration Signaling Messages

This document details messages involved in the 5G standalone access registration procedure. These messages are referenced from the [5G Standalone Access Registration Sequence Diagrams](https://www.eventhelix.com/5G/standalone-access-registration/).

|Message | Path |
|:-------|------|
| [Preamble](#preamble)|UE ➔ gNB|
| [PDCCH DCI Format 1_0](#pdcch-dci-format-10)<br> └[<small>Format 1_0 - CRC Scrambled with RA-RNTI</small>](#format-10---crc-scrambled-with-ra-rnti)|gNB ➔ UE|
| [Random Access Response](#random-access-response)<br> └[<small>MAC PDU</small>](#mac-pdu)<br>  └[<small>MAC Payload for Random Access Response</small>](#mac-payload-for-random-access-response)<br>   └[<small>RAR UL Grant</small>](#rar-ul-grant)|gNB ➔ UE|
| [RRCSetupRequest](#rrcsetuprequest)|UE ➔ gNB|
| [PDCCH DCI Format 1_0](#pdcch-dci-format-10)<br> └[<small>Format 1_0 - CRC Scrambled with C-RNTI</small>](#format-10---crc-scrambled-with-c-rnti)|gNB ➔ UE|
| [RRCSetup](#rrcsetup)<br> ├[<small>RadioBearerConfig</small>](#radiobearerconfig)<br> └[<small>CellGroupConfig</small>](#cellgroupconfig)|gNB ➔ UE|
| [PDCCH DCI Format 0_0](#pdcch-dci-format-00)<br> └[<small>Format 0_0 - CRC Scrambled with C-RNTI</small>](#format-00---crc-scrambled-with-c-rnti)|gNB ➔ UE|
| [RRCSetupComplete](#rrcsetupcomplete)<br> └[<small>Registration Request</small>](#registration-request)|UE ➔ gNB|
| [Initial UE Message](#initial-ue-message)<br> └[<small>Registration Request</small>](#registration-request)|gNB ➔ New AMF|
| [Namf_Communication_UEContextTransfer Request](#namfcommunicationuecontexttransfer-request)<br> └[<small>Registration Request</small>](#registration-request)|New AMF ➔ Old AMF|  
| [Namf_Communication_UEContextTransfer Response](#namfcommunicationuecontexttransfer-response)<br> └[<small>UE Context in AMF</small>](#ue-context-in-amf)|Old AMF ➔ New AMF|  
| [Identity Request](#identity-request)|New AMF ➔ gNB ➔ UE|
| [Identity Response](#identity-response)|UE ➔ gNB ➔ New AMF|
| [Nausf_UEAuthenticate_authenticate Request](#nausfueauthenticateauthenticate-request)| New AMF ➔ AUSF|
| [Nudm_UEAuthenticate_Get Request](#nudmueauthenticateget-request)| AUSF ➔ UDM|
| [Nudm_UEAuthenticate_Get Response](#nudmueauthenticateget-response)| UDM ➔ AUSF|
| [Nausf_UEAuthenticate_authenticate Response](#nausfueauthenticateauthenticate-response) |AUSF ➔ New AMF|
| [Authentication Request](#authentication-request)|New AMF ➔ gNB ➔ UE|
| [Authentication Response](#authentication-response)|UE ➔ gNB ➔ New AMF|
| [NAS Security Mode Command](#nas-security-mode-command)|New AMF ➔ gNB ➔ UE|
| [NAS Security Mode Complete](#nas-security-mode-complete)|UE ➔ gNB ➔ New AMF|
| [N5g-eir_EquipmentIdentityCheck Request](#n5g-eirequipmentidentitycheck-request)| New AMF ➔ 5G-EIR|
| [N5g-eir_EquipmentIdentityCheck Response](#n5g-eirequipmentidentitycheck-response)| 5G-EIR ➔ New AMF|
| [Namf_Communication_RegistrationCompleteNotify](#namfcommunicationregistrationcompletenotify)| New AMF ➔ Old AMF |
| [Nudm_UEContextManagement_Registration Request](#nudmuecontextmanagementregistration-request)<br> └[<small>Amf3GppAccessRegistration</small>](#amf3gppaccessregistration)| New AMF ➔ UDM |
| [Nudm_UEContextManagement_Registration Response](#nudmuecontextmanagementregistration-response)| UDM ➔ New AMF |
| [Nudm_SubscriberDataManagement_Get Request](#nudmsubscriberdatamanagementget-request) | New AMF ➔ UDM|
| [Nudm_SubscriberDataManagement_Get Response](#nudmsubscriberdatamanagementget-response)<br> ├[<small>AccessAndMobilitySubscriptionData</small>](#accessandmobilitysubscriptiondata)<br> ├[<small>SmfSelectionSubscriptionData</small>](#smfselectionsubscriptiondata)<br> └[<small>UeContextInSmfData</small>](#uecontextinsmfdata) | UDM ➔ New AMF|
| [Nudm_UEContextManagement_Deregistration_Notify](#nudmuecontextmanagementderegistrationnotify)|UDM ➔ Old AMF|
| [Nsmf_PDUSession_ReleaseSMContext](#nsmfpdusessionreleasesmcontext)|Old AMF ➔ SMF|
| [Npcf_AMPolicyControl_Create Request](#npcfampolicycontrolcreate-request)| New AMF ➔ PCF| 
| [Npcf_AMPolicyControl_Create Response](#npcfampolicycontrolcreate-response)<br> └[<small>PolicyAssociation</small>](#policyassociation)<br>  └[<small>PolicyAssociationRequest</small>](#policyassociationrequest)| PCF ➔ New AMF|
| [Namf_EventExpose_Subscribe Request](#namfeventexposesubscribe-request)<br> └[<small>AmfCreateEventSubscription</small>](#amfcreateeventsubscription)<br>  └[<small>AmfEventSubscription</small>](#amfeventsubscription)| PCF ➔ New AMF |
| [Namf_EventExpose_Subscribe Response](#namfeventexposesubscribe-request)<br> └[<small>AmfCreatedEventSubscription</small>](#amfcreatedeventsubscription)| New AMF ➔ PCF |
| [Npcf_AMPolicyControl_Delete Request](#npcfampolicycontroldelete-request)| Old AMF ➔ PCF |
| [Npcf_AMPolicyControl_Delete Response](#npcfampolicycontroldelete-response)| PCF ➔ Old AMF |
| [Nsmf_PDUSession_UpdateSMContext Request](#nsmfpdusessionupdatesmcontext-request)| New AMF ➔ SMF |
| [PFCP Session Modification Request](#pfcp-session-modification-request)| SMF ➔ UPF|
| [PFCP Session Modification Response](#pfcp-session-modification-response)| UPF ➔ SMF|
| [Nsmf_PDUSession_UpdateSMContext Response](#nsmfpdusessionupdatesmcontext-response)| SMF ➔ New AMF |
| [Initial Context Setup Request](#initial-context-setup-request)<br> └[<small>Registration Accept</small>](#registration-accept)|New AMF ➔ gNB|
| [SecurityModeCommand](#securitymodecommand)|gNB ➔ UE|
| [SecurityModeComplete](#securitymodecomplete)|UE ➔ gNB |
| [RRCReconfiguration](#rrcreconfiguration)<br> ├[<small>Registration Accept</small>](#registration-accept)<br> ├[<small>RadioBearerConfig</small>](#radiobearerconfig)<br> ├[<small>secondaryCellGroup</small>](#cellgroupconfig)<br> ├[<small>MeasConfig</small>](#measconfig)<br> └[<small>masterCellGroup</small>](#cellgroupconfig)|gNB ➔ UE|
| [RRCReconfigurationComplete](#rrcreconfigurationcomplete)<br> └[<small>UplinkTxDirectCurrentList</small>](#uplinktxdirectcurrentlist)|UE ➔ gNB |
| [Initial Context Setup Response](#initial-context-setup-response) | gNB ➔ New AMF|
| [Registration Complete](#registration-complete)|UE ➔ gNB|
| [Nsmf_PDUSession_UpdateSMContext Request](#nsmfpdusessionupdatesmcontext-request)| New AMF ➔ SMF |
| [PFCP Session Modification Request](#pfcp-session-modification-request)| SMF ➔ UPF|
| [PFCP Session Modification Response](#pfcp-session-modification-response)| UPF ➔ SMF|
| [Nsmf_PDUSession_UpdateSMContext Response](#nsmfpdusessionupdatesmcontext-response)| SMF ➔ New AMF |

## Preamble

UE ➔ gNB

[TS 38.213](#5g-specifications), [TS 38.321](#5g-specifications), [TS 38.211](#5g-specifications)

The UE picks a random preamble. The preamble is referenced with the Random Access Preamble Id (RAPID). The preamble transmission is a Zadoff-Chu sequence. 

Each preamble transmission is associated with an [RA-RNTI](#ra-rnti). 

### RA-RNTI

The RA-RNTI associated with the PRACH in which the Random Access Preamble is transmitted, is computed as:

```
RA-RNTI= 1 + s_id + 14 × t_id + 14 × 80 × f_id + 14 × 80 × 8 × ul_carrier_id
```

Where:
| Identifier | Description |
|------------|-------------|
|s_id |Index of the first OFDM symbol of the specified PRACH (0 ≤ s_id < 14)|
|t_id |Index of the first slot of the specified PRACH in a system frame (0 ≤ t_id < 80) |
|f_id |Index of the specified PRACH in the frequency domain (0 ≤ f_id < 8) |
|ul_carrier_id |Uplink carrier used for Msg1 transmission (0 for NUL carrier, and 1 for SUL carrier)|

## PDCCH DCI Format 1_0

gNB ➔ UE

[TS 38.212](#5g-specifications)

DCI Format 1_0 is used to assign downlink resources. 

### Format 1_0 - CRC Scrambled with RA-RNTI

In response to a PRACH transmission, a UE attempts to detect a DCI Format 1_0 with PDCCH CRC scrambled by  
the RA-RNTI corresponding to the RACH transmission. The UE looks for message during a configured window 
of length ra-ResponseWindow.

The RA-RNTI scrambled DCI message signals the frequency and time resources assigned for the transmission of the Transport Block containing
the Random Access Response message.

The following information is transmitted by means of the RA-RNTI scrambled DCI Format 1_0:

>| Field | Bits |
>|-------|:------:|
>|Frequency domain resource assignment |  ⌈log<sub>2</sub>(N<sub>RB</sub><sup>DL,BWP</sup>(N<sub>RB</sub><sup>DL,BWP</sup> + 1)/2)⌉<br>N<sub>RB</sub><sup>DL,BWP</sup> is the size of CORESET 0 | 
>|Time domain resource assignment | 4 
>|VRB-to-PRB mapping | 1 
>|Modulation and coding scheme | 5 
>| TB scaling | 2
>|Reserved bits | 16 

### Format 1_0 - CRC Scrambled with C-RNTI

The following information is transmitted by a DCI Format 1_0 with PDCCH CRC scrambled by the assigned C-RNTI:

>| Field | Bits |
>|-------|------|
>|Identifier of DCI formats | 1
>|Frequency domain resource assignment |  ⌈log<sub>2</sub>(N<sub>RB</sub><sup>DL,BWP</sup>(N<sub>RB</sub><sup>DL,BWP</sup> + 1)/2)⌉<br>N<sub>RB</sub><sup>DL,BWP</sup> is the size of the active DL bandwidth part in case DCI format 1_0<br>is monitored in the UE specific search space if DCH sizes <= 4 and DCI size with<br> C-RNTI <= 3. Otherwise N<sub>RB</sub><sup>DL,BWP</sup> is the size of CORESET 0| 
>|Time domain resource assignment | 4 
>|VRB-to-PRB mapping | 1 
>|Modulation and coding scheme | 5 
>| New data indicator | 1
>| Redundancy version | 2
>| HARQ process number | 4
>| Downlink assignment index | 2
>| TPC command for scheduled PUCCH | 2
>| PUCCH resource indicator | 3
>| PDSCH-to-HARQ_feedback timing indicator | 3

## Random Access Response

gNB ➔ UE

[TS 38.213](#5g-specifications), [TS 38.321](#5g-specifications)

1. The UE listens on the PDCCH addressed by the RA-RNTI.
1. Once the PDCCH with the RA-RNTI is decoded, the UE uses the RB resources in the message to receive the downlink transport block.
1. The downlink transport block contains the MAC PDU. 
    - The UE MAC PDU consists of one or more MAC subPDUs. 
    - Since multiple UEs may send a Preamble in the same RACH opportunity, they will all be addressed by the same RA-RNTI.
    - Thus, multiple Random Access Responses (RAR) may be carried in a single MAC PDU (They correspond to different UEs that initiated the random access procedure in the same RACH opportunity). 
    - Each RAR in the MAC PDU is addressed to a different UE via RAPID value.

### MAC PDU

>| subPDU | 1 bit | 1 bit | 6-bit | MAC subPDU payload |
>|:------:|:-----:|:-----:|:-----:|:------------------:|
>| MAC subPDU 1 | E | T | RAPID 1 | [MAC payload for Random Access Response](#mac-payload-for-random-access-response)|
>| MAC subPDU 2 | E | T | RAPID 2 | [MAC payload for Random Access Response](#mac-payload-for-random-access-response)|
>| MAC subPDU 3 | E | T | RAPID 3 | [MAC payload for Random Access Response](#mac-payload-for-random-access-response)|
>| ⋮  |  | | | |
>| MAC subPDU n |  | | | |
>| Padding (optional) |  | | | |

### E/T/RAPID MAC subheader

>|1 bit|1 bit|6-bit|
>|:---:|:---:|:-----:|
>|  E  |  T  | RAPID |

### MAC Payload for Random Access Response

>|Field | Description | Bits |
>|------|-------------|:------:|
>|R| Reserved bit (set to "0")| 1 
>|Timing Advance Command| The Timing Advance Command field indicates the index value TA used to control the amount of timing adjustment that the MAC entity must apply in TS 38.213. |12
>|[RAR UL Grant](#rar-ul-grant)| The Uplink Grant field indicates the resources to be used on the uplink in TS 38.213| 27
>|Temporary C-RNTI| The Temporary C-RNTI field indicates the temporary identity that is used by the MAC entity during Random Access.|16

#### RAR UL Grant

>|RAR grant field|	Number of bits  |
>|---------------|:-------------------:|
>|Frequency hopping flag	|1
>|Msg3 PUSCH frequency resource allocation|	14
>|Msg3 PUSCH time resource allocation|	4
>|MCS|	4
>|TPC command for Msg3 PUSCH|	3
>|CSI request	|1


## RRCSetupRequest

UE ➔ gNB

[38.331](#5g-specifications)

The RRC Setup Request is sent with the random ue-Identity and an establishment cause. The following establishment causes are defined:

>|Establishment cause | Description |
>|--------------------|-------------|
>|emergency| Emergency call
>|highPriorityAccess| High priority access
>|mt-Access| Mobile terminated access
>|mo-Signalling| Mobile originated signaling
>|mo-Data| Mobile Originated data
>|mo-VoiceCall| Mobile originated voice call
>|mo-VideoCall| Mobile originated video call
>|mo-SMS| Mobile originated SMS (Text)
>|mps-PriorityAccess|Multimedia priority service - priority access
>|mcs-PriorityAccess|Mission critical service - priority access

```
RRCSetupRequest ::=                 SEQUENCE {
    rrcSetupRequest                     RRCSetupRequest-IEs
}

RRCSetupRequest-IEs ::=             SEQUENCE {
    ue-Identity                         InitialUE-Identity,
    establishmentCause                  EstablishmentCause,
    spare                               BIT STRING (SIZE (1))
}

InitialUE-Identity ::=              CHOICE {
    ng-5G-S-TMSI-Part1                  BIT STRING (SIZE (39)),
    randomValue                         BIT STRING (SIZE (39))
}

EstablishmentCause ::=              ENUMERATED {
                                        emergency, highPriorityAccess, 
                                        mt-Access, mo-Signalling,
                                        mo-Data, mo-VoiceCall, 
                                        mo-VideoCall, mo-SMS, mps-PriorityAccess,
                                        mcs-PriorityAccess,
                                        spare6, spare5, spare4, 
                                        spare3, spare2, spare1}
```

## RRCSetup

gNB ➔ UE

[38.331](#5g-specifications)

The RRC Setup message is sent to setup SRB1 and the master cell. The message carries the [radioBearerConfig](#radiobearerconfig) and [masterCellGroup](#cellgroupconfig) information elements.

```
RRCSetup ::=                        SEQUENCE {
    rrc-TransactionIdentifier           RRC-TransactionIdentifier,
    criticalExtensions                  CHOICE {
        rrcSetup                            RRCSetup-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

RRCSetup-IEs ::=                    SEQUENCE {
    radioBearerConfig                   RadioBearerConfig,
    masterCellGroup                     OCTET STRING (CONTAINING CellGroupConfig),
    lateNonCriticalExtension            OCTET STRING   OPTIONAL,
    nonCriticalExtension                SEQUENCE{}     OPTIONAL
}
```

### RadioBearerConfig
```
RadioBearerConfig ::=                   SEQUENCE {
    srb-ToAddModList                        SRB-ToAddModList                                        OPTIONAL,   -- Cond HO-Conn
    srb3-ToRelease                          ENUMERATED{true}                                        OPTIONAL,   -- Need N
    drb-ToAddModList                        DRB-ToAddModList                                        OPTIONAL,   -- Cond HO-toNR
    drb-ToReleaseList                       DRB-ToReleaseList                                       OPTIONAL,   -- Need N
    securityConfig                          SecurityConfig                                          OPTIONAL,   -- Need M
    ...
}

SRB-ToAddModList ::=                    SEQUENCE (SIZE (1..2)) OF SRB-ToAddMod
SRB-ToAddMod ::=                        SEQUENCE {
    srb-Identity                            SRB-Identity,
    reestablishPDCP                         ENUMERATED{true}                                        OPTIONAL,   -- Need N
    discardOnPDCP                           ENUMERATED{true}                                        OPTIONAL,   -- Need N
    pdcp-Config                             PDCP-Config                                             OPTIONAL,   -- Cond PDCP
    ...
}

DRB-ToAddModList ::=                    SEQUENCE (SIZE (1..maxDRB)) OF DRB-ToAddMod
DRB-ToAddMod ::=                        SEQUENCE {
    cnAssociation                           CHOICE {
        eps-BearerIdentity                      INTEGER (0..15),                                    -- EPS-DRB-Setup
        sdap-Config                             SDAP-Config                                         -- 5GC
    }                                       OPTIONAL, -- Cond DRBSetup
    drb-Identity                            DRB-Identity,
    reestablishPDCP                         ENUMERATED{true}                                        OPTIONAL,   -- Need N
    recoverPDCP                             ENUMERATED{true}                                        OPTIONAL,   -- Need N
    pdcp-Config                             PDCP-Config                                             OPTIONAL,   -- Cond PDCP
    ...
}
DRB-ToReleaseList ::=                   SEQUENCE (SIZE (1..maxDRB)) OF DRB-Identity

SecurityConfig ::=                      SEQUENCE {
    securityAlgorithmConfig                 SecurityAlgorithmConfig                                 OPTIONAL,   -- Cond RBTermChange
    keyToUse                                ENUMERATED{master, secondary}                           OPTIONAL,   -- Cond RBTermChange
    ...
}
```

### CellGroupConfig

```
CellGroupConfig ::=                         SEQUENCE {
    cellGroupId                                 CellGroupId,

    rlc-BearerToAddModList                      SEQUENCE (SIZE(1..maxLC-ID)) OF RLC-BearerConfig                OPTIONAL,   -- Need N
    rlc-BearerToReleaseList                     SEQUENCE (SIZE(1..maxLC-ID)) OF LogicalChannelIdentity          OPTIONAL,   -- Need N

    mac-CellGroupConfig                         MAC-CellGroupConfig                                             OPTIONAL,   -- Need M

    physicalCellGroupConfig                     PhysicalCellGroupConfig                                         OPTIONAL,   -- Need M

    spCellConfig                                SpCellConfig                                                    OPTIONAL,   -- Need M
    sCellToAddModList                           SEQUENCE (SIZE (1..maxNrofSCells)) OF SCellConfig               OPTIONAL,   -- Need N
    sCellToReleaseList                          SEQUENCE (SIZE (1..maxNrofSCells)) OF SCellIndex                OPTIONAL,   -- Need N
    ...,
    [[
    reportUplinkTxDirectCurrent-v1530           ENUMERATED {true}                                               OPTIONAL    -- Cond BWP-Reconfig
    ]]
}

-- Serving cell specific MAC and PHY parameters for a SpCell:
SpCellConfig ::=                        SEQUENCE {
    servCellIndex                       ServCellIndex                                                           OPTIONAL,   -- Cond SCG
    reconfigurationWithSync             ReconfigurationWithSync                                                 OPTIONAL,   -- Cond ReconfWithSync
    rlf-TimersAndConstants              SetupRelease { RLF-TimersAndConstants }                                 OPTIONAL,   -- Need M
    rlmInSyncOutOfSyncThreshold         ENUMERATED {n1}                             OPTIONAL,   -- Need S
    spCellConfigDedicated               ServingCellConfig                                                       OPTIONAL,   -- Need M
    ...
}

ReconfigurationWithSync ::=         SEQUENCE {
    spCellConfigCommon                  ServingCellConfigCommon                                                 OPTIONAL,   -- Need M
    newUE-Identity                      RNTI-Value,
    t304                                ENUMERATED {ms50, ms100, ms150, ms200, ms500, ms1000, ms2000, ms10000},
        rach-ConfigDedicated                CHOICE {
            uplink                              RACH-ConfigDedicated,
            supplementaryUplink             RACH-ConfigDedicated
    }                                           OPTIONAL,   -- Need N
    ...,
    [[
    smtc                                SSB-MTC OPTIONAL    -- Need S
    ]]
}

SCellConfig ::=                     SEQUENCE {
    sCellIndex                          SCellIndex,
    sCellConfigCommon                   ServingCellConfigCommon                                                 OPTIONAL,   -- Cond SCellAdd
    sCellConfigDedicated                ServingCellConfig                                                       OPTIONAL,   -- Cond SCellAddMod
    ...,
    [[
    smtc                                SSB-MTC OPTIONAL    -- Need S
    ]]
}
```
## PDCCH DCI Format 0_0

gNB ➔ UE

[TS 38.212](#5g-specifications)

DCI Format 0_0 is used to assign uplink resources to the UE.

### Format 0_0 - CRC Scrambled with C-RNTI

The following information is transmitted by a DCI Format 0_0 with PDCCH CRC scrambled by the assigned C-RNTI:

>| Field | Bits |
>|-------|------|
>|Identifier of DCI formats | 1
>|Frequency domain resource assignment |  ⌈log<sub>2</sub>(N<sub>RB</sub><sup>UL,BWP</sup>(N<sub>RB</sub><sup>UL,BWP</sup> + 1)/2)⌉<br>N<sub>RB</sub><sup>UL,BWP</sup> is the size of the active UL bandwidth part in case DCI format 0_0 is monitored in the UE specific search space if DCH sizes <= 4 and DCI size with C-RNTI <= 3. Otherwise N<sub>RB</sub><sup>UL,BWP</sup> is the size of the initial UL bandwidth part.| 
>|Time domain resource assignment | 4
>| Frequency hopping flag | 1 
>|Modulation and coding scheme | 5 
>| New data indicator | 1
>| Redundancy version | 2
>| HARQ process number | 4
>| Downlink assignment index | 2
>| TPC command for scheduled PUSCH | 2
>| UL/SUL indicator | 1

## RRCSetupComplete

UE ➔ gNB

[38.331](#5g-specifications)

The UE sends the RRC Setup Complete message with a [Registration Request](#registration-request) in the dedicatedNAS-Message field.

```
RRCSetupComplete ::=                SEQUENCE {
    rrc-TransactionIdentifier           RRC-TransactionIdentifier,
    criticalExtensions                  CHOICE {
        rrcSetupComplete                    RRCSetupComplete-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

RRCSetupComplete-IEs ::=            SEQUENCE {
    selectedPLMN-Identity               INTEGER (1..maxPLMN),
    registeredAMF                       RegisteredAMF                                   OPTIONAL,
    guami-Type                          ENUMERATED {native, mapped}                     OPTIONAL,
    s-nssai-List                        SEQUENCE (SIZE (1..maxNrofS-NSSAI)) OF S-NSSAI  OPTIONAL,
    dedicatedNAS-Message                DedicatedNAS-Message,
    ng-5G-S-TMSI-Value                  CHOICE {
        ng-5G-S-TMSI                        NG-5G-S-TMSI,
        ng-5G-S-TMSI-Part2                  BIT STRING (SIZE (9))
    }                   OPTIONAL,
    lateNonCriticalExtension            OCTET STRING                                    OPTIONAL,
    nonCriticalExtension                SEQUENCE{}                                      OPTIONAL
}

RegisteredAMF ::=                   SEQUENCE {
    plmn-Identity                       PLMN-Identity                                   OPTIONAL,
    amf-Identifier                      AMF-Identifier
}
```

### Registration Request

UE ➔ [RRCSetupComplete](#rrcsetupcomplete) ➔ gNB ➔ [NGAP Initial UE Message](#initial-ue-message) ➔ New AMF ➔ [Namf_Communication_UEContextTransfer Request](#namfcommunicationuecontexttransfer-request) ➔ Old AMF

[TS 24.501](#5g-specifications)

The Registration Request NAS message is carried from the UE to the newly assigned AMF. The message will also be passed to the old AMF to retrieve the AMF context for the UE. 

>| Field |  Type  |
>|-----|----|
>| Extended protocol discriminator |  |
>| Security header type |  |
>| Spare half octet |  |
>| Registration request message identity | Message type |
>| 5GS registration type | <ul><li>initial registration</li><li>mobility registration updating</li><li>periodic registration updating</li><li>emergency registration</li></ul>  |
>| ngKSI | NAS key set identifier |
>| Spare half octet |  |
>| 5GS mobile identity |  |
>| Non-current native NAS key set identifier | NAS key set identifier |
>| 5GMM capability |  |
>| UE security capability |  |
>| Requested NSSAI |  NSSAI|
>| Last visited registered TAI | 5GS tracking area identity |
>| S1 UE network capability |  |
>| Uplink data status |  |
>| PDU session status |  |
>| MICO indication |  |
>| UE status |  |
>| Additional GUTI | 5GS mobile identity |
>| Allowed PDU session status |  |
>| UE's usage setting |  |
>| Requested DRX parameters | DRX parameters |
>| EPS NAS message container |  |
>| LADN indication |  |
>| Payload container |  |

## Initial UE Message

gNB ➔ New AMF

[TS 38.413](#5g-specifications)

The gNB sends the Initial UE Message to the selected AMF. The message carries the [Registration Request](#registration-request) that was received from the UE in the RRC Setup Complete message. The "RAN UE NGAP ID" and the "RRC Establishment Cause" are also included in the message.

The AMF will use the "RAN UE NGAP ID" to address the UE context on the gNB.


>| Field | Description |
>|-------|------|
>|Message Type|   |
>|RAN UE NGAP ID|   |
>|NAS-PDU|  [Registration Request](#registration-request) |
>|User Location Information|   |
>|RRC Establishment Cause|  OCTET STRING |
>|[5G-S-TMSI](#5g-identifiers)|   |
>|AMF Set ID|   |
>|UE Context Request| Indicates that a UE context including security information needs to be setup at the NG-RAN. |
>|Allowed NSSI|   |

## Namf_Communication_UEContextTransfer Request

New AMF ➔ Old AMF

[29.502](#5g-specifications), [29.518](#5g-specifications)

New AMF requests context transfer from the Old AMF. The complete [NAS registration request message](#registration-request) received from the UE is included in the context request.

>| Field |  Description  |
>|-----|----|
>| [5G-GUTI](#5g-identifiers)| |
>| Reason| |
>| [Registration Request](#registration-request)| Integrity protected message from the UE that triggers the context transfer.|


## Namf_Communication_UEContextTransfer Response

Old AMF ➔ New AMF

[29.502](#5g-specifications), [29.518](#5g-specifications)

The Old AMF passes the [AMF UE Context](#ue-context-in-amf) to the new AMF.

>| Field |  Description  |
>|-----|----|
>| [UE Context in AMF](#ue-context-in-amf)| Integrity protected message from the UE that triggers the context transfer.|
>|Mobile Equipment Identifier|Optional|
>|Allowed NSSAI||
>|Mapping Of Allowed NSSAI||

### UE Context in AMF

The complete UE context maintained at the AMF. The AMF passes this context to a "New AMF" if the UE attempts registration in the "New AMF".

>| Field |  Description  |
>|-----|----|
>|[SUPI](#5g-identifiers)|	SUPI (Subscription Permanent Identifier) is the subscriber's permanent identity in 5GS.|
>|SUPI-unauthenticated-indicator	| This indicates whether the SUPI is unauthenticated.|
>|[GPSI](#5g-identifiers) | The GPSI(s) of the UE. The presence is dictated by its storage in the UDM.|
>|[5G-GUTI](#5g-identifiers)|5G Globally Unique Temporary Identifier.|
>|[PEI](#5g-identifiers)|	Mobile Equipment Identity |
>|Internal Group ID-list	|List of the subscribed internal group(s) that the UE belongs to.|
>|UE Specific DRX Parameters	| UE specific DRX parameters.|
>|UE MM Network Capability|	Indicates the UE MM network capabilities.|
>|5GMM Capability|	Includes other UE capabilities related to 5GCN or interworking with EPS.|
>|Events Subscription|List of the event subscriptions by other CP NFs. Indicating the events being subscribed as well as any information on how to send the corresponding notifications|
>**AM Policy Association Information includes the AM Policy Information and the PCF ID(s) below**
>>| Field |  Description  |
>>|-----|----|
>>|AM Policy Information| Information on AM policy provided by PCF. Includes the Policy Control Request Triggers and the Policy Control Request Information. Includes the authorized RFSP and the authorized Service Area Restrictions.|
>>|PCF ID(s)|	The identifier of the PCF for AM Policy. In roaming, the identifier of V-PCF and H-PCF.|
>>|Subscribed RFSP Index|	An index to specific RRM configuration in the NG-RAN that is received from the UDM.|
>>|RFSP Index in Use|	An index to specific RRM configuration in the NG-RAN that is currently in use.|
>>|MICO Mode Indication|Indicates the MICO Mode for the UE.|
>>|Voice Support Match Indicator|	An indication whether the UE radio capabilities are compatible with the network configuration. The AMF uses it as an input for setting the IMS voice over PS Session Supported Indication over 3GPP access.|
>>|Homogenous Support of IMS Voice over PS Sessions |	Indicates per UE if "IMS Voice over PS Sessions" is homogeneously supported in all TAs in the serving AMF or homogeneously not supported, or, support is non-homogeneous/unknown.|
>>|UE Radio Capability for Paging Information	| Information used by the NG-RAN to enhance the paging towards the UE.|
>>|Information on Recommended Cells And RAN nodes For Paging|	Information sent by the NG-RAN, and used by the AMF when paging the UE to help determining the NG-RAN nodes to be paged as well as to provide the information on recommended cells to each of these NG-RAN nodes, in order to optimize the probability of successful paging while minimizing the signaling load on the radio path.|
>>|UE Radio Capability Information|	Information sent by the NG-RAN node and stored in the AMF. The AMF sends this information to the NG-RAN node within the UE context during transition to CM-CONNECTED state.|
>>|SMSF Identifier |The Identifier of the SMSF serving the UE in RM REGISTERED state.|
>>|SMSF Address	|The Address of the SMSF serving the UE in RM-REGISTERED state.|
>>|SMS Subscription|	Indicates subscription to any SMS delivery service over NAS irrespective of access type.|
>>|SEAF data	|Master security information received from AUSF|
>>|Last used EPS PLMN ID|	The identifier of the last used EPS PLMN|
>**For each access type level context within the UE access and mobility context:**
>>| Field |  Description  |
>>|-----|----|
>>|Access Type|	Indicates the access type for this context.|
>>|RM State|	Registration management state.|
>>|Registration Area|	Current Registration Area (a set of tracking areas in TAI List).|
>>|TAI of last Registration Update|	TAI of the TA in which the last registration request was initiated.|
>>|User Location Information|	Information on user location.|
>>|Mobility Restrictions|	Mobility Restrictions restrict mobility handling or service access of a UE. It consists of RAT restriction, Forbidden area, Service area restrictions and Core Network type restriction.|
>>|Expected UE Behavior Parameters for AMF|	Indicates per UE the Expected UE Behavior Parameters and their corresponding validity times.|
>>|Security Information for CP|	Control plane security information.|
>>|Security Information for UP|	User plane security information.|
>>|Allowed NSSAI	|Allowed NSSAI consisting of one or more S-NSSAIs for serving PLMN in the present Registration Area.|
>>|Mapping Of Allowed NSSAI	|Mapping Of Allowed NSSAI is the mapping of each S-NSSAI of the Allowed NSSAI to the S-NSSAIs of the Subscribed S-NSSAIs.|
>>|AMF UE NGAP ID	|Identifies the UE association over the NG interface within the AMF as defined in TS 38.413.|
>>|RAN UE NGAP ID	|Identifies the UE association over the NG interface within the NG-RAN node as defined in TS 38.413.|
>>|Network Slice Instance(s)	|The Network Slice Instances selected by 5GC for this UE.|
>**For each PDU Session level context:**
>>| Field |  Description  |
>>|-----|----|
>>|S-NSSAI(s)|	The S-NSSAI(s) associated to the PDU Session.|
>>|DNN|	The associated DNN for the PDU Session.|
>>|Network Slice Instance id|	The network Slice Instance information for the PDU Session|
>>|PDU Session ID	|The identifier of the PDU Session.|
>>|SMF Information|	The associated SMF identifier and SMF address for the PDU Session.|
>>|Access Type|	The current access type for this PDU Session.|
>>|EBI-ARP list|	The allocated EBI and associated ARP pairs for this PDU session.|
>>|5GSM Core Network Capability|	The UEs 5GSM Core Network Capability as defined in TS 23.501.|


## Identity Request

New AMF ➔ [DL NAS Transport](#dl-nas-transport) ➔ gNB ➔ [DLInformationTransfer](#dlinformationtransfer) ➔ UE

[TS 24.501](#5g-specifications)

The New AMF requests UE identity ([SUCI](#5g-identifiers)) from the UE via a NAS message.

>| Field |  Type  |
>|-----|----|
>| Extended protocol discriminator| |
>| Security header type| |
>| Spare half octet| |
>| Identity request message identity| Message type|
>| Identity type|5GS identity type |
>| Spare half octet| |


## Identity Response

UE ➔ [ULInformationTransfer](#ulinformationtransfer) ➔ gNB ➔ [UL NAS Transport](#ul-nas-transport) ➔ New AMF

[TS 24.501](#5g-specifications)

The UE responds to the Identity Request with [SUCI](#5g-identifiers). The [SUCI](#5g-identifiers) is derived from the public key of the Home PLMN.

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Identity response message identity|Message type|
>|Mobile identity|5GS mobile identity|


## Nausf_UEAuthenticate_authenticate Request

New AMF ➔ AUSF

[TS 33.501](#5g-specifications)

The AMF requests UE authentication vectors and algorithm information from the AUSF - Authentication Server Function.

Resource URI: `{apiRoot}/nausf-auth/v1/ue-authentications` 

>| Scenario | Authentication Method | Inputs |
>|-----|----|----|
>|Initial authentication request| | [SUPI](#5g-identifiers) (Subscription Permanent Identifier) or [SUCI](#5g-identifiers) (Subscription Concealed Identifier) |
>|Subsequent authentication request| 5G AKA| Authentication confirmation message with RES* |
>|Subsequent authentication request | EAP-AKA’| 	EAP packet as described in RFC 4187 and RFC 5448 |
 
## Nudm_UEAuthenticate_Get Request

AUSF ➔ UDM

[TS 29.503](#5g-specifications)

The Authentication Server Function (AUSF) requests authentication vectors from the UDM - Unified Data Management function.

>| Field | Presence | Description |
>|-------|----------|-------------|
>|[SUPI](#5g-identifiers) or [SUCI](#5g-identifiers), serving network name|Required| Subscriber Permanent Identifier ([SUPI](#5g-identifiers)) or Subscriber Concealed Identifier ([SUCI](#5g-identifiers))|
>|Synchronization Failure | Optional | Synchronization Failure indication and related information (i.e. RAND/AUTS). |

## Nudm_UEAuthenticate_Get Response

UDM ➔ AUSF

[TS 29.503](#5g-specifications), [TS 33.501](#5g-specifications)

The UDM returns the authentication vectors to the AUSF.

>| Field | Presence | Description |
>|-------|----------|-------------|
>| Authentication method and data| Required | Authentication method and corresponding authentication data for a certain UE as identified by SUPI or SUCI input. |
>|[SUPI](#5g-identifiers)|Optional| Subscriber Permanent Identifier. Present if SUPI was specified in the input.|

## Nausf_UEAuthenticate_authenticate Response

AUSF ➔ New AMF

[TS 33.501](#5g-specifications)

The response returns the master key which is used by AMF to derive NAS security keys and other security key(s).

>| Field | Authentication Method | Outputs |
>|-----|----|----|
>|Authentication response| 5G AKA| Authentication vector, or Authentication confirmation acknowledge message.  |
>|Authentication response | EAP-AKA’| 	EAP packet as described in RFC 4187 and RFC 5448 |
>|Authentication result| | Master key which is used by AMF to derive NAS security keys and other security key(s). |

## Authentication Request

New AMF ➔ [DL NAS Transport](#dl-nas-transport) ➔ gNB ➔ [DLInformationTransfer](#dlinformationtransfer) ➔ UE

[TS 24.501](#5g-specifications)

Initiate the authentication procedure with the UE. Send the key selector, RAND and AUTN to the UE.

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Authentication request message identity|Message type|
>|ngKSI |NAS key set identifier|
>|Spare half octet||
>|Authentication parameter RAND (5G authentication challenge)|Authentication parameter RAND|
>|Authentication parameter AUTN (5G authentication challenge)|Authentication parameter AUTN|
>|ABBA||
>|EAP message||


## Authentication Response

UE ➔ [ULInformationTransfer](#ulinformationtransfer) ➔ gNB ➔ [UL NAS Transport](#ul-nas-transport) ➔ New AMF

[TS 24.501](#5g-specifications)

The UE responds to the authentication challenge.

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Authentication response message identity||
>|Authentication response parameter||
>|EAP message||


## NAS Security Mode Command

New AMF ➔ [DL NAS Transport](#dl-nas-transport) ➔ gNB ➔ [DLInformationTransfer](#dlinformationtransfer) ➔ UE

[TS 24.501](#5g-specifications)

The AMF signals the selected NAS security algorithm to the UE. The AMF also requests the IMEISV from the UE.

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Security mode command message identity||
>|Selected NAS security algorithms||
>|ngKSI||
>|Spare half octet||
>|Replayed UE security capabilities||
>|IMEISV request||
>|HashAMF||
>|Selected EPS NAS security algorithms||
>|Additional 5G security information||
>|EAP message||

## NAS Security Mode Complete

UE ➔ [ULInformationTransfer](#ulinformationtransfer) ➔ gNB ➔ [UL NAS Transport](#ul-nas-transport) ➔ New AMF

[TS 24.501](#5g-specifications)

The UE signals the completion of the NAS security procedure. The message contains the IMEISV.

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Security mode complete message identity|Message type|
>|IMEISV|5G mobility identity|
>|NAS message container||

## N5g-eir_EquipmentIdentityCheck Request

New AMF ➔ 5G-EIR

[TS 23.502](#5g-specifications)

This service is provided by the 5G-EIR to check the PEI and determine whether the PEI is blacklisted. 

| Inputs | Outputs |
|--------|---------|
| [PEI](#5g-identifiers) and [SUPI](#5g-identifiers)| PEI checking result

## N5g-eir_EquipmentIdentityCheck Response

5G-EIR ➔ New AMF

[TS 23.502](#5g-specifications)

5G-EIR responds to the PEI blacklisting check. 

| Inputs | Outputs |
|--------|---------|
| [PEI](#5g-identifiers) and [SUPI](#5g-identifiers)| PEI checking result

## Namf_Communication_RegistrationCompleteNotify 

New AMF ➔ Old AMF

[29.518](#5g-identifiers), [23.502](#5g-identifiers)

>| Field | Presence | Description|
>|-------|----------|------------|
>|[5G-GUTI](#5g-identifiers)|Required|5G Globally Unique Temporary Identity|
>|PDU Session ID(s) |Optional|Indicates the PDU Session(s) to be released|
>|PCF ID|Optional|Indicates that the PCF ID that handles the AM Policy association has changed|

## Nudm_UEContextManagement_Registration Request

New AMF ➔ UDM

[TS 29.503](#5g-specifications)

Resource URI for 3GPP access:
```
//{apiRoot}/nudm_uecm/v1/{ueid}/registrations/amf-3gpp-access
```
Here:

**{ueid}** Represents the Subscription Identifier SUPI or GPSI (see 3GPP TS 23.501) 
[SUPI](#5g-identifiers) (i.e. imsi or nai) is used with the PUT and PATCH methods; GPSI (i.e. msisdn or extid) is used with the GET method. The ueid pattern is:


```
"(imsi-[0-9]{5,15}|nai-.+|msisdn-[0-9]{5,15}|extid-.+|.+)"
```
>|HTTP/Custom method | Description|Body datastructure|
>|--------------------------------|------------|----------|
>|PUT	|Update the AMF registration for 3GPP access| [Amf3GppAccessRegistration](#amf3gppaccessregistration)|
>|PATCH	|Modify the AMF registration for 3GPP access|Amf3GppAccessRegistrationModification|
>|GET	|Retrieve the AMF registration information for 3GPP access.||


### Amf3GppAccessRegistration

>|Attribute name|	Data type|	Presence |	Cardinality	| Description|
>|--------------|-------------|:---------:|-----------------|---------------|
>|amfInstanceId|	NfInstanceId|	M|	1	T|The identity the AMF uses to register in the NRF.|
>|supportedFeatures|	SupportedFeatures|	O	|0..1	||
>|purgeFlag	|PurgeFlag|	O|	0..1|	This flag indicates whether or not the AMF has deregistered. It shall not be included in the Registration service operation.|
>|pei|	[Pei](#5g-identifiers)	|O|	0..1|	[Permanent Equipment Identifier](#5g-identifiers).|
>|imsVoPS|	ImsVoPS|	O	|0..1	|Indicates per UE if "IMS Voice over PS Sessions" is homogeneously supported in all TAs in the serving AMF, or homogeneously not supported.|
>|deregCallbackUri|	Uri	|M|	1	|A URI provided by the AMF to receive (implicitly subscribed) notifications on deregistration.|
>|pcscfRestorationCallbackUri|	Uri|	O	|0..1|	A URI provided by the AMF to receive (implicitly subscribed) notifications on the need for P-CSCF Restoration.|
>|guami|	Guami|	C	|0..1|	This IE shall contain the serving AMF's GUAMI.|It shall be included if the NF service consumer is an AMF.|
>|backupAmfInfo|	array(BackupAmfInfo)|	C	|0..N	|This IE shall be included if the NF service consumer is an AMF and the AMF supports the AMF management without UDSF for the first interaction with UDM. The UDM uses this attribute to do an NRF query in order to invoke later services in a backup AMF, e.g. Namf_EventExposure.|


## Nudm_UEContextManagement_Registration Response

UDM ➔ New AMF

[TS 29.503](#5g-specifications)

>|Data type|	Presence|	Cardinality	| Response codes|	Description|
>|:---------:|:---------:|:---------------:|:----------------:|:-------------|
>|n/a		|||	204 No Content|	Upon success, an empty response body shall be returned |
>|ProblemDetails	|M|	1|	404 Not Found|	The "cause" attribute shall be set to the following application error:<ul><li>USER_NOT_FOUND</li></ul>	|
>|ProblemDetails	|M|	1	|403 Forbidden|	The "cause" attribute shall be set to one of the following application errors:<ul><li> UNKNOWN_5GS_SUBSCRIPTION<li> NO_PS_SUBSCRIPTION</li><li>ROAMING_NOT_ALLOWED</li><li>ACCESS_NOT_ALLOWED</li><li>RAT_NOT ALLOWED</li><li>REAUTHENTICATION_REQUIRED</li></ul>|


## Nudm_SubscriberDataManagement_Get Request

New AMF ➔ UDM

[TS 29.503](#5g-specifications)

>| Requested Data | HTTP Verb | URI |
>|----------------|:----------:|------|
>| Access and Mobility Subscription data | GET | ../{supi}/am-data |
>| SMF Selection Subscription data | GET | ../{supi}/smf-select-data |
>| UE Context In SMF Data Retrieval | GET | ../{supi}/ue-context-in-smf-data |


## Nudm_SubscriberDataManagement_Get Response

UDM ➔ New AMF

[TS 29.503](#5g-specifications)

>| Provided Data | HTTP Verb | Provided Data Type |
>|----------------|:----------:|------|
>| Access and Mobility Subscription data | 200 OK | [AccessAndMobilitySubscriptionData](#accessandmobilitysubscriptiondata)|
>| SMF Selection Subscription data | 200 OK | [SmfSelectionSubscriptionData](#smfselectionsubscriptiondata)|
>| UE Context In SMF Data Retrieval | 200 OK | [UeContextInSmfData](#uecontextinsmfdata) | 


### AccessAndMobilitySubscriptionData

>|Attribute name|	Data type|	Presence | 	Cardinality | 	Description|
>|--------------|-------------|:---------:|--------------|---------------|
>|supportedFeatures|	SupportedFeatures|	O	| 0..1	|
>|gpsis|	array(Gpsi)	|O|	0..N	|List of Generic Public Subscription Identifier; see 3GPP TS 29.571|
>|internalGroupIds|	array(InternalGroupId)|	O	| 0..N	|List of internal group identifier; see 3GPP TS 23.501 |
>|subscribedUeAmbr|	Ambr|	O	|0..1|	|
>|nssai|	Nssai	|O|	0..1|	Network Slice Selection Assistance Information|
>|ratRestrictions|	array(RatType)|	O|	0..N|	List of RAT Types that are restricted; see 3GPP TS 29.571|
>|forbiddenAreas	|array(Area)|	O|	0..N|	List of forbidden areas|
>|serviceAreaRestrictions	|ServiceAreaRestriction|	O|	0..1	|Subscribed Service Area Restriction|
>|coreNetworkTypeRestrictions	|array(CoreNetworkType)	|O|	0..N	|List of Core Network Types that are restricted|
>|rfspIndex|	RfspIndex|	O	|0..1|	Index to RAT/Frequency Selection Priority|
>|subsRegTimer|	DurationSec|	O|	0..1|	Subscribed periodic registration timer; see 3GPP TS 29.571|
>|ueUsageType|	UeUsageType|	O|	0..1|	|
>|mpsPriority|	MpsPriorityIndicator|	O	|0..1|	|
>|activeTime	|DurationSec|	O|	0..1|	subscribed active time for PSM UEs|
>|dlPacketCount	|DlPacketCount|	O|	0..1|	DL Buffering Suggested Packet Count indicates whether extended buffering of downlink packets for High Latency Communication is requested.|
>|sorInfo|	SorInfo	|O|	0..1|	This IE shall be present if the UDM shall send the information for Steering of Roaming during registration or the subscription data update to the UE.|
>|micoAllowed	|MicoAllowed|	O|	0..1|	Indicates whether the UE subscription allows MICO mode.|
>|sharedDataIds	|array(SharedDataId)	|O	|0..N|	Identifier of shared data|

```
/{supi}/am-data:
    get:
      summary: retrieve a UE's Access and Mobility Subscription Data
      operationId: Get
      tags:
        - Access and Mobility Subscription Data Retrieval
      parameters:
        - name: supi
          in: path
          description: Identifier of the UE
          required: true
          schema:
            $ref: 'TS29571_CommonData.yaml#/components/schemas/Supi'
        - name: supported-features
          in: query
          description: Supported Features
          schema:
             $ref: 'TS29571_CommonData.yaml#/components/schemas/SupportedFeatures'
        - name: plmn-id
          in: query
          description: serving PLMN ID
          content:
            application/json:
              schema:
                $ref: 'TS29571_CommonData.yaml#/components/schemas/PlmnId'
      responses:
        '200':
          description: Expected response to a valid request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AccessAndMobilitySubscriptionData'
        '404':
          description: User (SUPI) does not exist
        default:
          description: Unexpected error
          content:
            application/problem+json:
              schema:
                $ref: 'TS29571_CommonData.yaml#/components/schemas/ProblemDetails'
```

### SmfSelectionSubscriptionData

>|Attribute name|	Data type|	Presence | 	Cardinality | 	Description|
>|--------------|-------------|:---------:|--------------|---------------|
>|supportedFeatures|	SupportedFeatures	|O	|0..1||
>|subscribedSnssaiInfos	|array(SnssaiInfo)|	O|	0..N	|List of S-NSSAIs and associated information (DNN Info); see 3GPP TS 23.501 |

```
/{supi}/smf-select-data:
    get:
      summary: retrieve a UE's SMF Selection Subscription Data
      operationId: Get
      tags:
        - SMF Selection Subscription Data Retrieval
      parameters:
        - name: supi
          in: path
          description: Identifier of the UE
          required: true
          schema:
            $ref: 'TS29571_CommonData.yaml#/components/schemas/Supi'
        - name: supported-features
          in: query
          description: Supported Features
          schema:
             $ref: 'TS29571_CommonData.yaml#/components/schemas/SupportedFeatures'
        - name: plmn-id
          in: query
          description: serving PLMN ID
          content:
            application/json:
              schema:
                $ref: 'TS29571_CommonData.yaml#/components/schemas/PlmnId'
      responses:
        '200':
          description: Expected response to a valid request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/SmfSelectionSubscriptionData'
        '404':
          description: User (SUPI) does not exist
        default:
          description: Unexpected error
          content:
            application/problem+json:
              schema:
                $ref: 'TS29571_CommonData.yaml#/components/schemas/ProblemDetails'
```

### UeContextInSmfData

>|Attribute name|	Data type|	Presence | 	Cardinality | 	Description|
>|--------------|-------------|:---------:|--------------|---------------|
>|pduSessions|	map(PduSession)|	O	|0..N|	A map (list of key-value pairs where pduSessionId converted from integer to string serves as key) of PduSessions.|
>|pgwInf	|array(PgwInfo)|	O	|0..N|	Information about the DNNs/APNs and PGW-C+SMF FQDNs used in interworking with EPS|

```
  /{supi}/ue-context-in-smf-data:
    get:
      summary: retrieve a UE's UE Context In SMF Data
      operationId: Get
      tags:
        - UE Context In SMF Data Retrieval
      parameters:
        - name: supi
          in: path
          description: Identifier of the UE
          required: true
          schema:
            $ref: 'TS29571_CommonData.yaml#/components/schemas/Supi'
        - name: supported-features
          in: query
          description: Supported Features
          schema:
             $ref: 'TS29571_CommonData.yaml#/components/schemas/SupportedFeatures'
      responses:
        '200':
          description: Expected response to a valid request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UeContextInSmfData'
        '404':
          description: User (SUPI) does not exist
        default:
          description: Unexpected error
          content:
            application/problem+json:
              schema:
                $ref: 'TS29571_CommonData.yaml#/components/schemas/ProblemDetails'
```

## Nudm_UEContextManagement_Deregistration_Notify

UDM ➔ Old AMF

[TS 29.503](#5g-specifications)

The following procedure using the DeregistrationNotification service operation is supported:
-	UDM initiated NF Deregistration

1. The UDM sends a POST request to the callbackReference as provided by the Old AMF during the registration (See [Amf3GppAccessRegistration](#amf3gppaccessregistration) deregCallbackUri field) . 
2. The Old AMF service consumer responds with "204 No Content". 

## Nsmf_PDUSession_ReleaseSMContext

Old AMF ➔ SMF

[TS 23.502](#5g-specifications)

This message allows to release the AMF-SMF association for a certain PDU Session because the PDU Session has been released.

>|Input | Presence|
>|------|---------|
>|SUPI | Required |
>|PDU Session ID | Required | 
>|UE location information | Optional
>|AN type | Optional
>|UE Time Zone| Optional

## Npcf_AMPolicyControl_Create Request

New AMF ➔ PCF

[29.513](#5g-specifications), [29.507](#5g-specifications)

URI organization:
```
{apiRoot}/{apiName}/{apiVersion}/{apiSpecificResourceUriPart}
```
-	The `{apiRoot}` shall be set as described in 3GPP TS 29.501.
-	The `{apiName}` shall be "npcf-am-policy-control".
-	The `{apiVersion}` shall be "v1".
-	The `{apiSpecificResourceUriPart}` specifies the API specific string.


>|Resource name|	Resource URI|	HTTP method or custom operation|	Description|
>|-------------|-------------|----------------------------------|---------------|
>|AM Policies	|{apiRoot}/npcf-am-policy-control/v1/policies/ |	POST|	Create a new Individual AM Policy| resource.|
>|Individual AM Policy	|{apiRoot}/npcf-am-policy-control/v1/policies/{polAssoId}|	GET|	Read the Individual AM Policy resource.|
>|Individual AM Policy	|{apiRoot}/npcf-am-policy-control/v1/policies/{polAssoId}|	DELETE|	Delete the Individual AM Policy resource.|
>|Individual AM Policy	|{apiRoot}/npcf-am-policy-control/v1/policies/{polAssoId}/update|	update (POST)|Report observed event trigger and obtain updated policies.|


## Npcf_AMPolicyControl_Create Response

PCF ➔ New AMF

[29.513](#5g-specifications), [29.507](#5g-specifications)

|Data type|	Presence|	Cardinality	|Response codes	| Description|
|-------------|-------------|-------------------|---------------|---------------|
|[PolicyAssociation](#policyassociation)	|M|	1	|200 OK|	


### PolicyAssociation

>| Attribute name | Data type                | Presence | Cardinality | Description   |
>|----------------|--------------------------|---|-------------|------------------------------|
>| request        | [PolicyAssociationRequest](#policyassociationrequest) | O | 0..1        | The information provided by the NF service consumer when requesting the creation of a policy association|
>| uePolicy       | FFF                      | O | 0..1        | The UE policy as determined by the PCF.|
>| triggers       | array(RequestTrigger)    | O | 1..N        | Request Triggers that the PCF subscribes. Only values "LOC_CH" and "PRA_CH" are permitted.              |
>| servAreaRes    | FFS                      | O | 0..1        | Service Area Restriction as part of the AMF Access and Mobility Policy as determined by the PCF         |
>| rfsp           | RfspIndex                | O | 0..1        | RFSP Index as part of the AMF Access and Mobility Policy as determined by the PCF.                    |
>| pras           | map(PresenceInfo)        | C | 1..N        | If the Trigger "PRA_CH" is provided, the presence reporting area(s) for which reporting is requested shall be provided. The praId attribute within the PresenceInfo data type shall also be the key of the map. The praStatus attribute within the PresenceInfo data type shall not be supplied.                |
>| suppFeat       | SupportedFeatures        | M | 1           | Indicates the negotiated supported features. |


#### PolicyAssociationRequest

>|Attribute name	|Data type|	Presence|	Cardinality|	Description	|
>|---------------|---------|---------|--------------|-------------|
>|notificationUri|	Uri	|M	|1|	Identifies the recipient of Notifications sent by the PCF.	|
>|altNotifIpv4Addrs|	array(Ipv4Addr)	|O|	1..N|	Alternate or backup IPv4 Addess(es) where to send Notifications.	|
>|altNotifIpv6Addrs	|array(Ipv6Addr)	|O	|1..N|	Alternate or backup IPv6 Addess(es) where to send Notifications.	|
>|supi|	[Supi](#5g-identifiers)|	C|	0..1|	Subscription Permanent Identifier (~IMSI in 4G).	|
>|gpsi|	[Gpsi](#5g-identifiers)|	C|	0..1|	Generic Public Subscription Identifier.	|
>|accessType	|AccessType|	C|	0..1|	The Access Type where the served UE is camping.	|
>|pei|	[Pei](#5g-identifiers)	|C|	0..1|	The [Permanent Equipment Identifier](#5g-identifiers) of the served UE.	|
>|userLoc	|UserLocation|	C|	0..1|	The location of the served UE.	|
>|timeZone	|TimeZone|	C	|0..1	|The time zone where the served UE is camping.	|
>|servingPlmn|	NetworkId|	C|	0..1|	The serving PLMN where the served UE is camping.	|
>|ratType	|RatType	|C|	0..1	|The RAT Type where the served UE is camping.	|
>|groupId|	GroupId|	C|	0..1|	Internal Group Identifier of the served UE.	|
>|hPcfId	|string|	C|	0..1|	H-PCF Identifier.	|
>|servAreaRes	|ServiceAreaRestriction|	C|	0..1|	Service Area Restriction as part of the AMF Access and Mobility Policy.	|
>|rfsp	|RfspIndex	|C|	0..1|	RFSP Index as part of the AMF Access and Mobility Policy.	|
>|uePolReq|	UePolicyRequest| 	C	|0..1	|A request for UE Policies. Shall be provided when the AMF receives an "UPSI LIST TRANSPORT" message.	|
>|guami|	Guami|	C|	0..1|	The Globally Unique AMF Identifier (GUAMI) shall be provided by an AMF as service consumer.	|
>|serviceName	|string|	O|	0..1|	If the NF service consumer is an AMF, it should provide the name of a service produced by the AMF that makes use of information received within the Npcf_AMPolicyControl_UpdateNotify service operation.	|
>|suppFeat	|SupportedFeatures	|M|	1|	Indicates the features supported by the service consumer.	|
>|traceReq	|TraceData|	C|	0..1|	Trace control and configuration parameters information defined in 3GPP TS 32.422 shall be included if trace is required to be activated.|	


## Namf_EventExpose_Subscribe Request

PCF ➔ New AMF

[29.518](#5g-identifiers), [23.502](#5g-identifiers)

Applications can subscribe to AMF events by sending a Subscription Request.

Resource URI: `{apiRoot}/namf-evts/v1/subscriptions`

The PCF can register for the following events:

>| Event | Description |
>|-------|--------------|
>|Location-Report | A NF subscribes to this event to receive the Last Known Location of a UE or a group of UEs, and Updated Location of the UE or any UE in the group when AMF becomes aware of a location change of the UE.|
>|Presence-In-AOI-Report|A NF subscribe to this event to receive the current present state of a UE in a specific Area of Interest (AOI), and notification when a specified UE enters or leaves the specified area. The area could be identified by a TA list, an area ID or specific interested area name like "LADN".|
>|Time-Zone-Report|A NF subscribes to this event to receive the current time zone of a UE or a group of UEs, and updated time zone of the UE or any UE in the group when AMF becomes aware of a time zone change of the UE.|
>| Access-Type-Report |	A NF subscribes to this event to receive the current access type(s) of a UE or a group of UEs, and updated access type(s) of the UE or any UE in the group when AMF becomes aware of the access type change of the UE.|
>|Registration-State-Report|	A NF subscribes to this event to receive the current registration state of a UE or a group of UEs, and report for updated registration state of a UE or any UE in the group when AMF becomes aware of a registration state change of the UE.|
>|Connectivity-State-Report|	A NF subscribes to this event to receive the current connectivity state of a UE or a group of UEs, and report for updated connectivity state of a UE or any UE in the group when AMF becomes aware of a connectivity state change of the UE.|
>|Reachability-Report|	A NF subscribes to this event to receive the current reachability of a UE or a group of UEs, and report for updated reachability of a UE or any UE in the group when AMF becomes aware of a reachability change of the UE.|
>|Subscribed-Data-Report|A NF subscribes to this event to receive the current Subscribed Data for the UE(s) received from UDM, and notification when AMF received updated subscribed data for the UE(s) from UDM.|
>|Communication-Failure-Report|A NF subscribes to this event to receive the Communication failure report of a UE or group of UEs or any UE.|
>|UEs-In-Area-Report|A NF subscribes to this event to receive the number of UEs in a specific area. A NF may ask AMF for the UEs within the area based on Last Known Location or it may request AMF to actively look for the UEs within the area based on Current Location.|

URI: .../subscriptions ([AmfCreateEventSubscription](#amfcreateeventsubscription))

### AmfCreateEventSubscription

>|Attribute name	|Data type|	Presence|	Cardinality	|Description|
>|---------------|----------|:---------:|--------------|-----------|
>|subscription	|[AmfEventSubscription](#amfeventsubscription)|	M|	1|	Represents the AMF Event Subscription resource to be created.|
>|supportedFeatures|	SupportedFeatures|	C|	0..1	|This IE shall be present if at least one optional feature is supported. |

#### AmfEventSubscription

>|Attribute name	|Data type|	Presence|	Cardinality	|Description|
>|---------------|----------|:---------:|--------------|-----------|
>|eventList|	array(AmfEvent)|	M|	1..N|	Describes the events to be subscribed for this subscription.
>|notifyUri|	Uri|	M|	1|	Identifies the recipient of notifications sent by AMF for this subscription (NOTE 1)
>|notifyCorrelationId|	string	|M|	1	|Identifies the notification correlation ID. The AMF shall include this ID in the notifications.
>|nfId|	NfInstanceId|	M	|1|	Indicates the instance identity of the network function creating the subscription.
>|subsChangeNotifyUri|	Uri|	C|	0..1|	This IE shall be present if the subscription is created by an NF service consumer on behalf of another NF (e.g UDM creating event subscription at AMF for event notifications towards NEF). When present, this IE Identifies the recipient of notifications sent by AMF for change of subscription ID (e.g during mobility procedures involving AMF change).
>|subsChangeNotifyCorelationId	|string|	C|	0..1	|This IE shall be present when an NF Service Consumer (e.g. UDM) is subscribing for events on behalf of another NF Service Consumer (e.g. NEF). When present, this IE shall contain the notification correlation ID. The AMF shall include it in the notifications for change of subscription ID.
>|supi	|[Supi](#5g-identifiers)|	C|	0..1|	[Subscription Permanent Identifier](#5g-identifiers)
>|groupId	|GroupId	|C|	0..1|	Identifies a group of UEs.
>|gpsi	|[Gpsi](#5g-identifiers)|	C|	0..1|	[Generic Public Subscription Identifier](#5g-identifiers)
>|pei	|[Pei](#5g-identifiers)|	C	|0..1|	[Permanent Equipment Identifier](#5g-identifiers)
>|anyUE|	boolean|	C|	0..1	|This IE shall be present if the event subscription is applicable to any UE.  Default value "FALSE" is used, if not present (NOTE 2)
>|options|	AmfEventMode|	O|	0..1|	This IE may be included if the NF service consumer wants to describe how the reports of the event to be generated.


## Namf_EventExpose_Subscribe Response

New AMF ➔ PCF

[29.518](#5g-identifiers), [23.502](#5g-identifiers)

Response code: `201 Created` is returned with [AmfCreatedEventSubscription](#amfcreatedeventsubscription)

A "201 Created" code signals successful subscription.

### AmfCreatedEventSubscription

>|Attribute name	|Data type|	Presence|	Cardinality	|Description|
>|---------------|----------|:---------:|--------------|-----------|
>|subscription	|AmfEventSubscription|	M|	1	|Represents the newly created AMF Event Subscription resource.|
>|reportList	|array(AmfEventReport)	|O|	0..N|	Represents the immediate event reports (i.e. the current value |/ status of the events subscribed).|
>|supportedFeatures|	SupportedFeatures|	C	|0..1|	This IE shall be present if at least one optional feature is supported. |


## Npcf_AMPolicyControl_Delete Request

Old AMF ➔ PCF

[29.513](#5g-specifications), [29.507](#5g-specifications)

The Old AMF requests that the policy association is deleted as the corresponding UE context is terminated.

The old AMF will initiate the delete using the following URI:
```
{apiRoot}/npcf-am-policy-control/v1/policies/{polAssoId}
```

## Npcf_AMPolicyControl_Delete Response

PCF ➔ Old AMF

[29.513](#5g-specifications), [29.507](#5g-specifications)

PCF signals successful delete with `204 No Content` cause code.

>|Data type|	Presence|	Cardinality	| Response codes|	Description|
>|:---------:|:---------:|:---------------:|:----------------:|:-------------|
>|n/a		|||	204 No Content|	Upon success, an empty response body shall be returned |


## Initial Context Setup Request

AMF  ➔  eNB

[38.413](#5g-specifications)

The purpose of the Initial Context Setup procedure is to establish the necessary overall initial UE Context at the NG-RAN node, when required, including PDU session context, the Security Key, Mobility Restriction List, UE Radio Capability and UE Security Capabilities, etc. 

The AMF initiates a session setup with the gNB. The message typically contains the [Registration Accept](#registration-accept) NAS message. The message carries one or more PDU Session setup requests. Each PDU session is addressed with the "PDU Session ID".


>| Field |  Type  |
>|:-----|----|
>|Message Type||
>|AMF UE NGAP ID||
>|RAN UE NGAP ID||
>|Old AMF|AMF Name|
>|UE Aggregate Maximum Bit Rate||
>|Core Network Assistance Information||
>|GUAMI||
>|**PDU Session Resource Setup Request List**||
>> **PDU Session Resource Setup Request Item [PDU Session Id]**
>>| Field |  Type  |
>>|:-----|----|
>>|NAS-PDU||
>>|PDU Session ID||
>>|S-NSSAI ||
>>|PDU Session Resource Setup Request Transfer|OCTET STRING|
>| Field |  Type  |
>|:-----|----|
>|Allowed NSSAI||
>|UE Security Capabilities||
>|Security Key||
>|Trace Activation||
>|Mobility Restriction List||
>|UE Radio Capability||
>|Index to RAT/Frequency Selection Priority||
>|Masked IMEISV||
>|NAS-PDU||
>|Emergency Fallback Indicator||
>|RRC Inactive Transition Report Request||


### Registration Accept

New AMF ➔ [Initial Context Setup Request](#initial-context-setup-request) ➔ gNB ➔ [RRCReconfiguration](#rrcreconfiguration) ➔ UE

[TS 24.501](#5g-specifications)

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Registration accept message identity||
>|5GS registration result||
>|[5G-GUTI](#5g-identifiers)|5GS mobile identity|
>|Equivalent PLMNs|PLMN list|
>|TAI list|5GS tracking area identity list|
>|Allowed NSSAI|NSSAI|
>|Rejected NSSAI||
>|Configured NSSAI|NSSAI|
>|5GS network feature support||
>|PDU session status||
>|PDU session reactivation result||
>|PDU session reactivation result error cause||
>|LADN information||
>|MICO indication||
>|Network slicing indication||
>|Service area list||
>|T3512 value|GPS timer 3|
>|Non-3GPP de-registration timer value|GPRS timer 2|
>|T3502 value|GPRS timer 2|
>|Emergency number list||
>|Extended emergency number list||
>|SOR transparent container||
>|EAP message||

## SecurityModeCommand

gNB ➔ UE

[38.331](#5g-specifications)

The SecurityModeCommand message is used to command the activation of AS security.

The UE performs the following actions on receiving the Security Mode Command:

- Derive the K-gNB key. K-gNB is a key derived by UE and AMF from K-AMF.
- Derive K-RRC-int key associated with the Integrity Protection Algorithm.
- Verify the integrity protection of the Security Mode Command message.
- Derive K-UP-int key associated with the Integrity Protection Algorithm.
- Start SRB Integrity Protect.

Reference: 3GPP TS 33.501 V15.2.0 (2018-09)

```
SecurityModeCommand ::=             SEQUENCE {
    rrc-TransactionIdentifier           RRC-TransactionIdentifier,
    criticalExtensions                  CHOICE {
        securityModeCommand                 SecurityModeCommand-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

SecurityModeCommand-IEs ::=         SEQUENCE {
    securityConfigSMC                   SecurityConfigSMC,

    lateNonCriticalExtension            OCTET STRING         OPTIONAL,
    nonCriticalExtension                SEQUENCE{}           OPTIONAL
}

SecurityConfigSMC ::=               SEQUENCE {
    securityAlgorithmConfig             SecurityAlgorithmConfig,
    ...
}
```

## SecurityModeComplete

UE ➔ gNB

[38.331](#5g-specifications)

The SecurityModeComplete message is used to confirm the successful completion of a security mode command. Ciphering will be enabled after sending this message. The Security Mode Complete message is itself not ciphered.
The message is however integrity protected.

```
SecurityModeComplete ::=            SEQUENCE {
    rrc-TransactionIdentifier           RRC-TransactionIdentifier,
    criticalExtensions                  CHOICE {
        securityModeComplete                SecurityModeComplete-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

SecurityModeComplete-IEs ::=        SEQUENCE {
    lateNonCriticalExtension            OCTET STRING         OPTIONAL,
    nonCriticalExtension                SEQUENCE{}           OPTIONAL
}
```

## RRCReconfiguration

gNB ➔ UE

[38.331](#5g-specifications)

The purpose of this message is to modify an RRC connection, e.g. to establish/modify/release RBs, to perform reconfiguration with sync, to setup/modify/release measurements, to add/modify/release SCells and cell groups. As part of the procedure, NAS dedicated information may be transferred from the Network to the UE.

The message carries the following fields:
- [Registration Accept](#registration-accept)
- [masterCellGroup](#cellgroupconfig)
- [secondaryCellGroup](#cellgroupconfig)
- [radioBearerConfig](#radiobearerconfig)
- [MeasConfig](#measconfig)

```
RRCReconfiguration ::=              SEQUENCE {
    rrc-TransactionIdentifier           RRC-TransactionIdentifier,
    criticalExtensions                  CHOICE {
        rrcReconfiguration                  RRCReconfiguration-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

RRCReconfiguration-IEs ::=          SEQUENCE {
    radioBearerConfig                       RadioBearerConfig                                      OPTIONAL, -- Need M
    secondaryCellGroup                      OCTET STRING (CONTAINING CellGroupConfig)              OPTIONAL, -- Need M
    measConfig                              MeasConfig                                             OPTIONAL, -- Need M
    lateNonCriticalExtension                OCTET STRING                                           OPTIONAL,
    nonCriticalExtension                    RRCReconfiguration-v1530-IEs                           OPTIONAL
}

RRCReconfiguration-v1530-IEs ::=            SEQUENCE {
    masterCellGroup                         OCTET STRING (CONTAINING CellGroupConfig)              OPTIONAL, -- Need M
    fullConfig                              ENUMERATED {true}                                      OPTIONAL, -- Cond FullConfig
    dedicatedNAS-MessageList                SEQUENCE (SIZE(1..maxDRB)) OF DedicatedNAS-Message     OPTIONAL, -- Cond nonHO
    masterKeyUpdate                         MasterKeyUpdate                                        OPTIONAL, -- Cond MasterKeyChange
    dedicatedSIB1-Delivery                  OCTET STRING (CONTAINING SIB1)                         OPTIONAL, -- Need N
    dedicatedSystemInformationDelivery      OCTET STRING (CONTAINING SystemInformation)            OPTIONAL, -- Need N
    otherConfig                             OtherConfig                                            OPTIONAL,   -- Need N
    nonCriticalExtension                    SEQUENCE {}                                            OPTIONAL
}

MasterKeyUpdate ::=                 SEQUENCE {
    keySetChangeIndicator           BOOLEAN,
    nextHopChainingCount            NextHopChainingCount,
    nas-Container                   OCTET STRING                                                   OPTIONAL,    -- Cond securityNASC
    ...
}
```

### MeasConfig

```
MeasConfig ::=                      SEQUENCE {
    measObjectToRemoveList              MeasObjectToRemoveList                OPTIONAL,   -- Need N
    measObjectToAddModList              MeasObjectToAddModList                OPTIONAL,   -- Need N

    reportConfigToRemoveList            ReportConfigToRemoveList              OPTIONAL,   -- Need N
    reportConfigToAddModList            ReportConfigToAddModList              OPTIONAL,   -- Need N

    measIdToRemoveList                  MeasIdToRemoveList                    OPTIONAL,   -- Need N
    measIdToAddModList                  MeasIdToAddModList                    OPTIONAL,   -- Need N

    s-MeasureConfig                     CHOICE {
        ssb-RSRP                            RSRP-Range,
        csi-RSRP                            RSRP-Range
    }         OPTIONAL,   -- Need M

    quantityConfig                      QuantityConfig                        OPTIONAL,   -- Need M

    measGapConfig                       MeasGapConfig                         OPTIONAL,   -- Need M
    measGapSharingConfig                    MeasGapSharingConfig              OPTIONAL,   -- Need M
    ...
}

MeasObjectToRemoveList ::=              SEQUENCE (SIZE (1..maxNrofObjectId)) OF MeasObjectId

MeasIdToRemoveList ::=                  SEQUENCE (SIZE (1..maxNrofMeasId)) OF MeasId

ReportConfigToRemoveList ::=            SEQUENCE (SIZE (1..maxReportConfigId)) OF ReportConfigId
```

## RRCReconfigurationComplete

gNB ➔ New AMF

[38.331](#5g-specifications)

The RRC Reconfiguration Complete message is used to confirm the successful completion of an RRC connection reconfiguration.

```
RRCReconfigurationComplete ::=              SEQUENCE {
    rrc-TransactionIdentifier                   RRC-TransactionIdentifier,
    criticalExtensions                          CHOICE {
        rrcReconfigurationComplete                  RRCReconfigurationComplete-IEs,
        criticalExtensionsFuture                    SEQUENCE {}
    }
}

RRCReconfigurationComplete-IEs ::=          SEQUENCE {
    lateNonCriticalExtension                    OCTET STRING                              OPTIONAL,
    nonCriticalExtension                        RRCReconfigurationComplete-v1530-IEs      OPTIONAL
}

RRCReconfigurationComplete-v1530-IEs ::=    SEQUENCE {
    uplinkTxDirectCurrentList                   UplinkTxDirectCurrentList                 OPTIONAL,
    nonCriticalExtension                        SEQUENCE {}                               OPTIONAL
}
```

### UplinkTxDirectCurrentList

```
UplinkTxDirectCurrentList ::=           SEQUENCE (SIZE (1..maxNrofServingCells)) OF UplinkTxDirectCurrentCell

UplinkTxDirectCurrentCell ::=           SEQUENCE {
    servCellIndex                           ServCellIndex,
    uplinkDirectCurrentBWP                  SEQUENCE (SIZE (1..maxNrofBWPs)) OF UplinkTxDirectCurrentBWP,
    ...
}

UplinkTxDirectCurrentBWP ::=            SEQUENCE {
    bwp-Id                                  BWP-Id,
    shift7dot5kHz                           BOOLEAN,
    txDirectCurrentLocation             INTEGER (0..3301)
}
```
## Initial Context Setup Response

eNB  ➔  AMF

[38.413](#5g-specifications)

This message is sent by the NG-RAN node to confirm the setup of a UE context.

>| Field |  Description  |
>|:-----|----|
>|Message Type|
>|AMF UE NGAP ID| Identifes the UE context on the AMF.
>|RAN UE NGAP ID| Identifies the UE context on the RAN (gNB)
>|**PDU Session Resource Setup Response List**| 
>>**PDU Session Resource Setup Response Item [PDU Session Id]** 
>>| Field |  Description  |
>>|:-----|----|
>>|PDU Session ID| Identifies a PDU session
>>|PDU Session Resource Setup Response Transfer|
>**PDU Session Resource Failed to Setup List** 
>>**PDU Session Resource Failed to Setup Item [PDU Session ID]** 
>>| Field |  Description  |
>>|:-----|----|
>>|PDU Session ID| Identifies PDU session
>>|PDU Session Resource Setup Unsuccessful Transfer|
>Criticality Diagnostics

## Registration Complete

UE ➔ [ULInformationTransfer](#ulinformationtransfer) ➔ gNB ➔ [UL NAS Transport](#ul-nas-transport) ➔ New AMF

[TS 24.501](#5g-specifications)

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|Registration complete message identity|Message type|
>|SOR transparent container||

## Nsmf_PDUSession_UpdateSMContext Request

New AMF ➔ SMF

[TS 23.502](#5g-specifications)

This message updates the AMF-SMF association to support a PDU Session. The message also provides SMF with N1/N2 SM information received from the UE or from the AN.

>|Input | Presence |
>|------|----------|
>|SUPI| Required |
>|Operation Type | <ul><li>UP activate</li> <li>UP deactivate</li>  <li>UP To Be Switched</li></ul>
>| PDU Session ID| Optional
>| N1 SM container received from the UE| Optional
>| N2 SM information received from the AN | Optional
>|Serving GW Address(es) and Serving GW DL TEID(s) <br>for data forwarding during HO from 5GS to EPS. | Optional
>|UE location information| Optional
>|AN type| Optional
>|UE Time Zone| Optional
>|H-SMF identifier/address| Optional
>|EBI(s) to be revoked, PDU Session(s) to be re-activated| Optional
>|Direct Forwarding Flag| Optional
>|ARP list| Optional
>|S-NSSAI| Optional
>|Data Forwarding Tunnel (setup/release)| Optional
>|UE presence in LADN service area| Optional
>|Target ID| Optional
>|Target AMF ID| Optional
>|GUAMI| Optional
>|Backup AMF(s) (if NF Type is AMF)| Optional

## PFCP Session Modification Request

SMF ➔ UPF

[TS 29.244](#5g-specifications)

The [PFCP](#pfcp) Session Modification Request is used over the Sxa, Sxb, Sxc and N4 interface by the CP function to request the UP function to modify the [PFCP](#pfcp) session.

>| Information Element | Description |
>|---------------------|-------------|
>|CP F-SEID| Change the fully qualified Session Id 
>| Remove PDR | Remove Packet Detection Rule
>| Remove FAR | Remove Forwarding Action Rule 
>| Remove URR | Remove Usage Reporting Rule
>| Remove QER | Remove QoS Enforcement Rule
>| Remove BAR | Remove Buffering Action Rule
>| Remove Traffic Endpoint | 
>| Create PDR | Create Packet Detection Rule
>| Create FAR | Create Forwarding Action Rule 
>| Create URR | Create Usage Reporting Rule
>| Create QER | Create QoS Enforcement Rule
>| Create BAR | Create Buffering Action Rule
>| Create Traffic Endpoint | 
>| Update PDR | Update Packet Detection Rule
>| Update FAR | Update Forwarding Action Rule 
>| Update URR | Update Usage Reporting Rule
>| Update QER | Update QoS Enforcement Rule
>| Update BAR | Update Buffering Action Rule
>| Update Traffic Endpoint | 
>| PFCPSMReq-Flags| Update flags: <ul><li>DROBU (Drop Buffered Packets)</li><li>QAURR (Query All URRs)</li> </ul>
>| Query URR | Query Usage Reporting Rule
>| User Plane Inactivity Timer |
>| Query URR Reference | Query Usage Reporting Rule Reference
>| Trace Information |

## PFCP Session Modification Response

UPF ➔ SMF

[TS 29.244](#5g-specifications)

The [PFCP](#pfcp) Session Modification Response shall be sent over the Sxa, Sxb, Sxc and N4 interface by the UP function to the CP function as a reply to the [PFCP](#pfcp) Session Modification Request.

>| Information Element | Description |
>|---------------------|-------------|
>| Cause | Cause of acceptance or rejection of request 
>| Offending IE | Included if rejecting due to an error in a specific IE of the request.
>| Create PDR | Create Packet Detection Rule
>| Load Control Information | 
>| Overload Control Information |
>| Usage Report | 
>| Failed Rule ID| This IE shall be included if the Cause IE indicates a rejection due to a rule creation or modification failure.
>| Additional Usage Reports Information |
>| Created/Updated Traffic Endpoint |

## Nsmf_PDUSession_UpdateSMContext Response

SMF ➔ New AMF

[TS 23.502](#5g-specifications)


>| Output | Presence
>|--------|----------
>|Result Indication | Required
>|PDU Session ID| Optional
>|Cause| Optional
>|released EBI list| Optional
>|allocated EBI information| Optional
>|N2 SM information | Optional
>|N1 SM container to be transferred to the AN/UE| Optional

## NAS Transport

NAS traffic between the UE and the AMF is carried over NAS carrier messages in downlink and uplink.

### DL NAS Transport

New AMF ➔ gNB

[TS 24.501](#5g-specifications)

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|DL NAS TRANSPORT message identity|Message type|
>|Payload container type||
>|Spare half octet||
>|Payload container||
>|PDU session ID|PDU session identity 2|
>|Additional information||
>|5GMM cause||
>|Back-off timer value|GPRS Timer 3|

### DLInformationTransfer

gNB ➔ UE

[38.331](#5g-specifications)

```
DLInformationTransfer ::=           SEQUENCE {
    rrc-TransactionIdentifier           RRC-TransactionIdentifier,
    criticalExtensions                  CHOICE {
        dlInformationTransfer           DLInformationTransfer-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

DLInformationTransfer-IEs ::=   SEQUENCE {
    dedicatedNAS-Message                DedicatedNAS-Message    OPTIONAL,   -- Need N
    lateNonCriticalExtension            OCTET STRING            OPTIONAL,
    nonCriticalExtension                SEQUENCE {} OPTIONAL
}
```
### ULInformationTransfer

UE ➔ gNB

[38.331](#5g-specifications)


```
ULInformationTransfer ::=           SEQUENCE {
    criticalExtensions                  CHOICE {
        ulInformationTransfer           ULInformationTransfer-IEs,
        criticalExtensionsFuture            SEQUENCE {}
    }
}

ULInformationTransfer-IEs ::=   SEQUENCE {
    dedicatedNAS-Message                DedicatedNAS-Message                OPTIONAL,
    lateNonCriticalExtension            OCTET STRING                        OPTIONAL,
    nonCriticalExtension                SEQUENCE {}                         OPTIONAL
}
```

### UL NAS Transport

gNB ➔ New AMF

[TS 24.501](#5g-specifications)

>| Field |  Type  |
>|-----|----|
>|Extended protocol discriminator||
>|Security header type||
>|Spare half octet||
>|UL NAS TRANSPORT message identity|Message type|
>|Payload container type||
>|Spare half octet||
>|Payload container||
>|PDU session ID|PDU session identity 2|
>|Old PDU session ID|PDU session identity 2|
>|Request type||
>|S-NSSAI||
>|DNN||
>|Additional information||

## 5G Identifiers

|Identifier | 4G Equivalent | Description |
|----------|---------------|-------------|
| SUPI     | IMSI | Subscription Permanent Identifier is assigned to each subscriber accessing the 5G network.
| SUCI     | P-TMSI + MCC + MNC  | Subscription Concealed Identifier is a global identifier that can keep the UE identity concealed. SUCI can also be used by visiting networks to get authentication vectors from the home network.
| PEI      | IMEI | Permanent Equipment Identifier is assigned to each UE accessing the 5G network.
| GPSI     |    | Generic Public Subscription Identifier is used for addressing a 3GPP subscription in non-3GPP networks.
| 5G-GUTI  | GUTI | Unique global identifier for the UE that does not reveal the SUPI.
|5G-S-TMSI| S-TMSI| Shortened form of 5G-GUTI that is used in radio signaling procedures.<br>`<5G-S-TMSI> = <AMF Set ID><AMF Pointer><5G-TMSI>`

# PFCP

[TS 29.244](#5g-specifications)

The Packet Forwarding Control Protocol (PFCP) standardizes the signaling between control plane and the user plane functions. PDCP is used on the N4 interface between the Session Management Function (SMF) and the User Plane Function (UPF).

### PFCP Header

>|Field | Length (Octets) |
>|------|------------------|
>|Version/MP/S | 1
>|Message type | 1
>|Session Endpoint Identifier | 8
>|Sequence Number | 3
>|Message Priority/Spare| 1

### PFCP Messages

Packet Forwarding Control Protocol defines the following messages for Sxa, Sxb,	Sxc and	N4 interfaces. 

|Value| Message |Sxa|	Sxb|	Sxc|	N4|
|-----|--------------|---|------|-------|------|
|0|	Reserved				
||	**PFCP Node related messages**				
|1	|PFCP Heartbeat Request	|X|	X	|X|	X
|2	|PFCP Heartbeat Response	|X|	X	|X|	X
|3	|PFCP PFD Management Request	|-|	X	|X|	X
|4	|PFCP PFD Management Response	|-|	X	|X|	X
|5	|PFCP Association Setup Request	|X|	X	|X|	X
|6	|PFCP Association Setup Response	|X|	X	|X|	X
|7	|PFCP Association Update Request	|X|	X	|X|	X
|8	|PFCP Association Update Response	|X|	X	|X|	X
|9	|PFCP Association Release Request	|X|	X	|X|	X
|10	|PFCP Association Release Response	|X|	X	|X|	X
|11	|PFCP Version Not Supported Response	|X|	X	|X|	X
|12	|PFCP Node Report Request	|X|	X	|X|	X
|13	|PFCP Node Report Response	|X|	X	|X|	X
|14	|PFCP Session Set Deletion Request|	X|	X|	-| -	
|15	|PFCP Session Set Deletion Response	|X|	X|	-| -	
|16 to 49|	For future use				
|	|**PFCP Session related messages**				
|50	|PFCP Session Establishment Request	|X	|X	|X	|X|
|51	|PFCP Session Establishment Response	|X	|X	|X	|X|
|52	|PFCP Session Modification Request	|X	|X	|X	|X|
|53	|PFCP Session Modification Response	|X	|X	|X	|X|
|54	|PFCP Session Deletion Request	|X	|X	|X	|X|
|55	|PFCP Session Deletion Response	|X	|X	|X	|X|
|56	|PFCP Session Report Request	|X	|X	|X	|X|
|57	|PFCP Session Report Response	|X	|X	|X	|X|
|58 to 99|	For future use				
|	|**Other messages**				
|100 to 255 	|For future use	

## 5G specifications
 
|Specification | Version | Description |
|--------------|---------|-------------|
|[TS 23.502](https://www.3gpp.org/dynareport/23502.htm) | V15.3.0 (2018-09)| Procedures for the 5G System
|[TS 24.501](https://www.3gpp.org/dynareport/24501.htm) | V15.1.0 (2018-09)| Non-Access-Stratum (NAS) protocol for 5G System (5GS); Stage 3
|[TS 29.244](https://www.3gpp.org/dynareport/29244.htm) | V15.3.0 (2018-09)| Interface between the Control Plane and the User Plane nodes
|[TS 29.503](https://www.3gpp.org/dynareport/29503.htm) | V15.1.0 (2018-09)| 5G System; Unified Data Management Services; Stage 3
|[TS 29.507](https://www.3gpp.org/dynareport/29507.htm) | V15.1.0 (2018-09)| 5G System; Access and Mobility Policy Control Service; Stage 3
|[TS 29.513](https://www.3gpp.org/dynareport/29513.htm) | V15.1.0 (2018-09)| 5G System; Policy and Charging Control signalling flows and QoS parameter mapping; Stage 3
|[TS 29.514](https://www.3gpp.org/dynareport/29514.htm) | V15.1.0 (2018-09)| 5G System; Policy Authorization Service; Stage 3
|[TS 29.518](https://www.3gpp.org/dynareport/29518.htm) | V15.1.0 (2018-09)| 5G System; Access and Mobility Management Services; Stage 3
|[TS 33.501](https://www.3gpp.org/dynareport/33501.htm) | V15.2.0 (2018-09)| Security architecture and procedures for 5G System
|[TS 38.211](https://www.3gpp.org/dynareport/38211.htm) | V15.3.0 (2018-09)| NR; Physical channels and modulation
|[TS 38.212](https://www.3gpp.org/dynareport/38212.htm) | V15.3.0 (2018-09)| NR; Multiplexing and channel coding
|[TS 38.213](https://www.3gpp.org/dynareport/38213.htm) | V15.3.0 (2018-09)| NR; Physical layer procedures for control
|[TS 38.321](https://www.3gpp.org/dynareport/38321.htm) | V15.3.0 (2018-09)| NR; Medium Access Control (MAC) protocol specification
|[TS 38.331](https://www.3gpp.org/dynareport/38331.htm) | V15.3.0 (2018-09)| NR; Radio Resource Control (RRC); Protocol specification
|[TS 38.413](https://www.3gpp.org/dynareport/38413.htm) | V15.1.0 (2018-09)| NG-RAN; NG Application Protocol (NGAP)

			


<footer style="position: fixed; left:0; bottom: 0; width: 100%;">
  <a href="#5g-standalone-access-registration-signaling-messages" style="float:right; font-size:1.5em;">🡩top</a>
</footer>