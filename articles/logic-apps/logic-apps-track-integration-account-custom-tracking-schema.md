---
title: "aaaCustom suivi des schémas pour B2B analyse - Azure Logic Apps | Documents Microsoft"
description: "Créer des schémas de suivi personnalisé toomonitor B2B messages à partir des transactions dans votre compte de l’intégration d’Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Activer le suivi des toomonitor votre flux de travail terminée, bout en bout
Vous pouvez activer un suivi intégré pour les différentes parties de votre flux de travail d’entreprise à entreprise, notamment le suivi des messages AS2 ou X12. Lorsque vous créez des workflows, qui inclut une application logique, BizTalk Server, SQL Server ou toutes les autres couches, vous pouvez activer le suivi personnalisé qui enregistre les événements à partir de hello début toohello à la fin du flux de travail. 

Cette rubrique fournit un code personnalisé que vous pouvez utiliser dans les couches de hello en dehors de votre application logique. 

## <a name="custom-tracking-schema"></a>Schéma de suivi personnalisé
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Propriété | Type | Description |
| --- | --- | --- |
| sourceType |   | Type de source de hello exécuter. Les valeurs autorisées sont **Microsoft.Logic/workflows** et **custom**. (obligatoire) |
| Source |   | Si le type de source de hello est **Microsoft.Logic/workflows**, informations de source de hello doivent toofollow ce schéma. Si le type de source de hello est **personnalisé**, schéma de hello est un JToken. (obligatoire) |
| systemId | String | ID système d’application logique. (obligatoire) |
| runId | String | ID d’exécution d’application logique. (obligatoire) |
| operationName | String | Nom de l’opération hello (par exemple, action ou déclencheur). (obligatoire) |
| repeatItemScopeName | String | Répétez le nom de l’élément si l’action de hello est à l’intérieur d’un `foreach` / `until` boucle. (obligatoire) |
| repeatItemIndex | Entier  | Si l’action de hello est à l’intérieur d’un `foreach` / `until` boucle. Indique l’index de l’élément répété hello. (obligatoire) |
| trackingId | String | ID de suivi de messages de type hello toocorrelate. (facultatif) |
| correlationId | String | ID de corrélation de messages de type hello toocorrelate. (facultatif) |
| clientRequestId | String | Client peut remplir toocorrelate messages. (facultatif) |
| eventLevel |   | Niveau d’événement de hello. (obligatoire) |
| eventTime |   | Heure de l’événement hello, dans le format UTC AAAA-MM-DDTHH:MM:SS.00000Z. (obligatoire) |
| recordType |   | Type d’enregistrement de suivi hello. La valeur autorisée est **Custom**. (obligatoire) |
| record |   | Type d'enregistrement personnalisé. Le format autorisé est JToken. (obligatoire) |

## <a name="b2b-protocol-tracking-schemas"></a>Schémas de suivi de protocole B2B
Pour plus d’informations sur les schémas de suivi de protocole B2B, consultez :
* [Schémas de suivi AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Schémas de suivi X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le [suivi des messages B2B](logic-apps-monitor-b2b-message.md).   
* En savoir plus sur [le suivi des messages B2B dans le portail Operations Management Suite de hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* En savoir plus sur hello [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).
