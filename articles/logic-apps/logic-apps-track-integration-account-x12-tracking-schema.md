---
title: "schémas de suivi aaaX12 pour l’analyse de B2B - Azure Logic Apps | Documents Microsoft"
description: "Utilisez X12 le suivi des messages toomonitor B2B de schémas à partir des transactions dans votre compte de l’intégration d’Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Démarrer ou activer le suivi de X12 messages toomonitor réussite, les erreurs et les propriétés de message
Vous pouvez utiliser ces X12 suivi des schémas votre toohelp de compte d’intégration d’Azure vous permet de surveiller les transactions d’entreprise-entreprise (B2B) :

* Schéma de suivi de document informatisé X12
* Schéma de suivi d’accusé de réception de document informatisé X12
* Schéma de suivi d’échange X12
* Schéma de suivi d’accusé de réception d’échange X12
* Schéma de suivi de groupe fonctionnel X12
* Schéma de suivi d’accusé de réception de groupe fonctionnel X12

## <a name="x12-transaction-set-tracking-schema"></a>Schéma de suivi de document informatisé X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message X12. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message X12. (facultatif) |
| senderQualifier | String | Qualificateur du partenaire d’envoi. (obligatoire) |
| senderIdentifier | String | Identificateur du partenaire d’envoi. (obligatoire) |
| receiverQualifier | String | Qualificateur du partenaire de réception. (obligatoire) |
| receiverIdentifier | String | Identificateur du partenaire de réception. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich hello X12 accord sont résolus. (facultatif) |
| direction | Enum | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| interchangeControlNumber | String | Numéro de contrôle de l’échange. (facultatif) |
| functionalGroupControlNumber | String | Numéro de contrôle fonctionnel. (facultatif) |
| transactionSetControlNumber | String | Numéro de contrôle de document informatisé. (facultatif) |
| CorrelationMessageId | String | ID de message de corrélation. Correspond à {AgreementName}*{GroupControlNumber}*{TransactionSetControlNumber}. (facultatif) |
| messageType | String | Type de document ou de document informatisé. (facultatif) |
| isMessageFailed | Boolean | Indique si les messages hello X12 a échoué. (obligatoire) |
| isTechnicalAcknowledgmentExpected | Boolean | Si les accusé de réception technique hello est configuré dans l’accord de hello X12. (obligatoire) |
| isFunctionalAcknowledgmentExpected | Boolean | Si les accusé de réception fonctionnel hello est configuré dans l’accord de hello X12. (obligatoire) |
| needAk2LoopForValidMessages | Boolean | Indique si la boucle de hello AK2 est requis pour un message valide. (obligatoire) |
| segmentsCount | Entier  | Nombre de segments dans le jeu de transactions hello X12. (facultatif) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>Schéma de suivi d’accusé de réception de document informatisé X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message X12. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message X12. (facultatif) |
| senderQualifier | String | Qualificateur du partenaire d’envoi. (obligatoire) |
| senderIdentifier | String | Identificateur du partenaire d’envoi. (obligatoire) |
| receiverQualifier | String | Qualificateur du partenaire de réception. (obligatoire) |
| receiverIdentifier | String | Identificateur du partenaire de réception. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich hello X12 accord sont résolus. (facultatif) |
| direction | Enum | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| interchangeControlNumber | String | Numéro de contrôle d’accusé de réception fonctionnel hello l’échange. Valeur remplit uniquement pour l’envoi hello où fonctionnelle d’accusé de réception pour toopartner de messages envoyés hello. (facultatif) |
| functionalGroupControlNumber | String | Numéro de contrôle de groupe fonctionnel d’accusé de réception fonctionnel hello. Valeur remplit uniquement pour l’envoi hello où fonctionnelle d’accusé de réception pour toopartner de messages envoyés hello. (facultatif) |
| isaSegment | String | Segment ISA de message de type hello. Valeur remplit uniquement pour l’envoi hello où fonctionnelle d’accusé de réception pour toopartner de messages envoyés hello. (facultatif) |
| gsSegment | String | Segment GS de message de type hello. Valeur remplit uniquement pour l’envoi hello où fonctionnelle d’accusé de réception pour toopartner de messages envoyés hello. (facultatif) |
| respondingfunctionalGroupControlNumber | String | Numéro de contrôle de l’échange de réponse. (facultatif) |
| respondingFunctionalGroupId | String | ID du groupe fonctionnel de la réponse, qui mappe tooAK101 dans l’accusé de réception hello. (facultatif) |
| respondingtransactionSetControlNumber | String | Numéro de contrôle de document informatisé de réponse. (facultatif) |
| respondingTransactionSetId | String | ID, qui mappe les tooAK201 dans l’accusé de réception hello du jeu de transactions ne répondre. (facultatif) |
| statusCode | Boolean | Code d’état de l’accusé de réception du document informatisé. (obligatoire) |
| segmentsCount | Enum | Code d’état de l’accusé de réception. Les valeurs autorisées sont **Accepted**, **Rejected** et **AcceptedWithErrors**. (obligatoire) |
| processingStatus | Enum | État du traitement de l’accusé de réception hello. Les valeurs autorisées sont **Received**, **Generated** ou **Sent**. (obligatoire) |
| CorrelationMessageId | String | ID de message de corrélation. Correspond à {AgreementName}*{GroupControlNumber}*{TransactionSetControlNumber}. (facultatif) |
| isMessageFailed | Boolean | Indique si les messages hello X12 a échoué. (obligatoire) |
| ak2Segment | String | Accusé de réception d’un document informatisé dans hello reçu groupe fonctionnel. (facultatif) |
| ak3Segment | String | Signale les erreurs dans un segment de données. (facultatif) |
| ak5Segment | String | Signale si hello informatisé identifié dans le segment de hello AK2 est accepté ou rejeté et pourquoi. (facultatif) |

## <a name="x12-interchange-tracking-schema"></a>Schéma de suivi d’échange X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message X12. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message X12. (facultatif) |
| senderQualifier | String | Qualificateur du partenaire d’envoi. (obligatoire) |
| senderIdentifier | String | Identificateur du partenaire d’envoi. (obligatoire) |
| receiverQualifier | String | Qualificateur du partenaire de réception. (obligatoire) |
| receiverIdentifier | String | Identificateur du partenaire de réception. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich hello X12 accord sont résolus. (facultatif) |
| direction | Enum | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| interchangeControlNumber | String | Numéro de contrôle de l’échange. (facultatif) |
| isaSegment | String | Segment ISA du message. (facultatif) |
| isTechnicalAcknowledgmentExpected | Boolean | Si les accusé de réception technique hello est configuré dans l’accord de hello X12. (obligatoire) |
| isMessageFailed | Boolean | Indique si les messages hello X12 a échoué. (obligatoire) |
| isa09 | String | Date d’échange du document X12. (facultatif) |
| isa10 | String | Heure d’échange du document X12. (facultatif) |
| isa11 | String | Identificateur des normes de contrôle d’échange X12. (facultatif) |
| isa12 | String | Numéro de version du contrôle d’échange X12. (facultatif) |
| isa14 | String | Un accusé de réception X12 est exigé. (facultatif) |
| isa15 | String | Indicateur de test ou de production. (facultatif) |
| isa16 | String | Séparateur d'éléments. (facultatif) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>Schéma de suivi d’accusé de réception d’échange X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message X12. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message X12. (facultatif) |
| senderQualifier | String | Qualificateur du partenaire d’envoi. (obligatoire) |
| senderIdentifier | String | Identificateur du partenaire d’envoi. (obligatoire) |
| receiverQualifier | String | Qualificateur du partenaire de réception. (obligatoire) |
| receiverIdentifier | String | Identificateur du partenaire de réception. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich hello X12 accord sont résolus. (facultatif) |
| direction | Enum | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| interchangeControlNumber | String | Numéro de contrôle d’hello technique accusés de réception provenant de partenaires de l’échange. (facultatif) |
| isaSegment | String | Segment ISA hello technique un accusé de réception reçu de partenaires. (facultatif) |
| respondingInterchangeControlNumber |String | Numéro de contrôle hello technique un accusé de réception reçu de partenaires de l’échange. (facultatif) |
| isMessageFailed | Boolean | Indique si les messages hello X12 a échoué. (obligatoire) |
| statusCode | Enum | Code d’état de l’accusé de réception de l’échange. Les valeurs autorisées sont **Accepted**, **Rejected** et **AcceptedWithErrors**. (obligatoire) |
| processingStatus | Enum | État de l’accusé de réception. Les valeurs autorisées sont **Received**, **Generated** ou **Sent**. (obligatoire) |
| ta102 | String | Date de l’échange. (facultatif) |
| ta103 | String | Heure de l’échange. (facultatif) |
| ta105 | String | Code de note de l’échange. (facultatif) |

## <a name="x12-functional-group-tracking-schema"></a>Schéma de suivi de groupe fonctionnel X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message X12. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message X12. (facultatif) |
| senderQualifier | String | Qualificateur du partenaire d’envoi. (obligatoire) |
| senderIdentifier | String | Identificateur du partenaire d’envoi. (obligatoire) |
| receiverQualifier | String | Qualificateur du partenaire de réception. (obligatoire) |
| receiverIdentifier | String | Identificateur du partenaire de réception. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich hello X12 accord sont résolus. (facultatif) |
| direction | Enum | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| interchangeControlNumber | String | Numéro de contrôle de l’échange. (facultatif) |
| functionalGroupControlNumber | String | Numéro de contrôle fonctionnel. (facultatif) |
| gsSegment | String | Segment GS de message. (facultatif) |
| isTechnicalAcknowledgmentExpected | Boolean | Si les accusé de réception technique hello est configuré dans l’accord de hello X12. (obligatoire) |
| isFunctionalAcknowledgmentExpected | Boolean | Si les accusé de réception fonctionnel hello est configuré dans l’accord de hello X12. (obligatoire) |
| isMessageFailed | Boolean | Indique si les messages hello X12 a échoué. (obligatoire)|
| gs01 | String | Code d’identificateur fonctionnel. (facultatif) |
| gs02 | String | Code de l’expéditeur de l’application. (facultatif) |
| gs03 | String | Code du destinataire de l’application. (facultatif) |
| gs04 | String | Date du groupe fonctionnel. (facultatif) |
| gs05 | String | Heure du groupe fonctionnel. (facultatif) |
| gs07 | String | Code de l’agence responsable. (facultatif) |
| gs08 | String | Code identificateur de version/du secteur. (facultatif) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>Schéma de suivi d’accusé de réception de groupe fonctionnel X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message X12. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message X12. (facultatif) |
| senderQualifier | String | Qualificateur du partenaire d’envoi. (obligatoire) |
| senderIdentifier | String | Identificateur du partenaire d’envoi. (obligatoire) |
| receiverQualifier | String | Qualificateur du partenaire de réception. (obligatoire) |
| receiverIdentifier | String | Identificateur du partenaire de réception. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich hello X12 accord sont résolus. (facultatif) |
| direction | Enum | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| interchangeControlNumber | String | Numéro de contrôle, qui remplit le côté envoi de hello lors de la réception d’un accusé de réception technique des partenaires. (facultatif) |
| functionalGroupControlNumber | String | Numéro de contrôle de groupe fonctionnel de hello accusé de réception technique, qui remplit le hello côté d’envoi lors de la réception d’un accusé de réception technique des partenaires. (facultatif) |
| isaSegment | String | Identique au numéro de contrôle de l’échange, mais renseigné uniquement dans des cas spécifiques. (facultatif) |
| gsSegment | String | Identique au numéro de contrôle de groupe fonctionnel, mais renseigné uniquement dans des cas spécifiques. (facultatif) |
| respondingfunctionalGroupControlNumber | String | Numéro de contrôle de groupe fonctionnel d’origine de hello. (facultatif) |
| respondingFunctionalGroupId | String | Mappe tooAK101 dans l’ID de groupe fonctionnel hello accusé de réception (facultatif) |
| isMessageFailed | Boolean | Indique si les messages hello X12 a échoué. (obligatoire) |
| statusCode | Enum | Code d’état de l’accusé de réception. Les valeurs autorisées sont **Accepted**, **Rejected** et **AcceptedWithErrors**. (obligatoire) |
| processingStatus | Enum | État du traitement de l’accusé de réception hello. Les valeurs autorisées sont **Received**, **Generated** ou **Sent**. (obligatoire) |
| ak903 | String | Nombre maximal de documents informatisés reçus. (facultatif) |
| ak904 | String | Nombre de documents informatisés acceptés dans le groupe fonctionnel de hello identifié. (facultatif) |
| ak9Segment | String | Si le groupe fonctionnel de hello identifié dans le segment de hello AK1 est accepté ou rejeté et pourquoi. (facultatif) |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le [suivi des messages B2B](logic-apps-monitor-b2b-message.md).
* En savoir plus sur les [schémas de suivi AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* En savoir plus sur les [schémas de suivi personnalisé B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* En savoir plus sur [le suivi des messages B2B dans le portail Operations Management Suite de hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* En savoir plus sur hello [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).  
