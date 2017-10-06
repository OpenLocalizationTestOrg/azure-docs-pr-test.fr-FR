---
title: "schémas de suivi aaaAS2 pour l’analyse de B2B - Azure Logic Apps | Documents Microsoft"
description: "Utiliser AS2 le suivi des messages toomonitor B2B de schémas à partir des transactions dans votre compte de l’intégration d’Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Démarrer ou activer le suivi des messages AS2 et MDN toomonitor réussite, les erreurs et les propriétés de message
Vous pouvez utiliser ces schémas de suivi AS2 votre toohelp de compte d’intégration d’Azure vous permet de surveiller les transactions d’entreprise-entreprise (B2B) :

* Schéma de suivi de message AS2
* Schéma de suivi de MDN AS2

## <a name="as2-message-tracking-schema"></a>Schéma de suivi de message AS2
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message AS2. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message AS2. (facultatif) |
| as2To | String | Nom du destinataire du message AS2 dans les en-têtes de message de type hello AS2 hello. (obligatoire) |
| as2From | String | Nom de l’expéditeur du message AS2, des en-têtes de message de type hello AS2 de hello. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich accord AS2 hello sont résolus. (facultatif) |
| direction | String | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| messageId | String | ID du message AS2, à partir des en-têtes hello de message de type hello AS2 (facultatif) |
| dispositionType |String | Valeur de type de disposition MDN (notification de réception du message). (facultatif) |
| fileName | String | Nom de fichier, à partir de l’en-tête de hello du message de type hello AS2. (facultatif) |
| isMessageFailed |Boolean | Indique si les messages hello AS2 a échoué. (obligatoire) |
| isMessageSigned | Boolean | Si le message de type hello AS2 a été signé. (obligatoire) |
| isMessageEncrypted | Boolean | Indique si le message de type hello AS2 a été chiffré. (obligatoire) |
| isMessageCompressed |Boolean | Si le message de type hello AS2 a été compressé. (obligatoire) |
| correlationMessageId | String | ID du message AS2, messages toocorrelate avec MDN. (facultatif) |
| incomingHeaders |Dictionnaire de JToken | Détails de l’en-tête de message AS2 entrant. (facultatif) |
| outgoingHeaders |Dictionnaire de JToken | Détails de l’en-tête de message AS2 sortant. (facultatif) |
| isNrrEnabled | Boolean | Utilisez la valeur par défaut si la valeur de hello n’est pas connu. (obligatoire) |
| isMdnExpected | Boolean | Utilisez la valeur par défaut si la valeur de hello n’est pas connu. (obligatoire) |
| mdnType | Enum | Les valeurs autorisées sont **NotConfigured**, **Sync** ou **Async**. (obligatoire) |

## <a name="as2-mdn-tracking-schema"></a>Schéma de suivi de MDN AS2
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Propriété | Type | Description |
| --- | --- | --- |
| senderPartnerName | String | Nom de partenaire de l’expéditeur du message AS2. (facultatif) |
| receiverPartnerName | String | Nom de partenaire du destinataire du message AS2. (facultatif) |
| as2To | String | Nom du partenaire qui reçoit le message de type hello AS2. (obligatoire) |
| as2From | String | Nom du partenaire qui a envoyé le message de type hello AS2. (obligatoire) |
| agreementName | String | Nom de messages de type hello toowhich accord AS2 hello sont résolus. (facultatif) |
| direction |String | Direction de flux de messages hello, réception ou envoi. (obligatoire) |
| messageId | String | ID du message AS2. (facultatif) |
| originalMessageId |String | ID du message AS2 d’origine. (facultatif) |
| dispositionType | String | Valeur du type de disposition MDN. (facultatif) |
| isMessageFailed |Boolean | Indique si les messages hello AS2 a échoué. (obligatoire) |
| isMessageSigned |Boolean | Si le message de type hello AS2 a été signé. (obligatoire) |
| isNrrEnabled | Boolean | Utilisez la valeur par défaut si la valeur de hello n’est pas connu. (obligatoire) |
| statusCode | Enum | Les valeurs autorisées sont **Accepted**, **Rejected** et **AcceptedWithErrors**. (obligatoire) |
| micVerificationStatus | Enum | Les valeurs autorisées sont **NotApplicable**, **Succeeded** et **Failed**. (obligatoire) |
| correlationMessageId | String | ID de corrélation. Hello d’origine sollicités ID (ID du message hello pour lequel le MDN est configuré de hello). (facultatif) |
| incomingHeaders | Dictionnaire de JToken | Indique les détails de l’en-tête de message entrant. (facultatif) |
| outgoingHeaders |Dictionnaire de JToken | Indique les détails de l’en-tête de message sortant. (facultatif) |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* En savoir plus sur le [suivi des messages B2B](logic-apps-monitor-b2b-message.md).   
* En savoir plus sur les [schémas de suivi personnalisé B2B](logic-apps-track-integration-account-custom-tracking-schema.md).   
* En savoir plus sur le [schéma de suivi X12](logic-apps-track-integration-account-x12-tracking-schema.md).   
* En savoir plus sur [le suivi des messages B2B dans le portail Operations Management Suite de hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
