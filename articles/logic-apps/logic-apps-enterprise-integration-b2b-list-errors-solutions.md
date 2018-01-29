---
title: "Liste des erreurs et des solutions Logic Apps B2B : Azure App Service | Microsoft Docs"
description: Liste des erreurs et des solutions Logic Apps B2B
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Liste des erreurs et des solutions Logic Apps B2B  
Cet article vous aide à comprendre les erreurs qui peuvent se produire dans le cadre des scénarios Logic Apps B2B et suggère des actions appropriées pour corriger ces erreurs.


## <a name="agreement-resolution"></a>Résolution d’accord

### <a name="no-agreement-found"></a>* Aucun accord trouvé 

|   |   |  
|---|---|
| Description de l’erreur | Aucun accord trouvé avec les paramètres de résolution d’accord|    
| Action requise | L’accord doit être ajouté au compte d’intégration avec les identités commerciales convenues.</br> Les identités commerciales doivent correspondre aux ID de message entrant.|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Aucun accord trouvé avec les identités

|   |   | 
|---|---|
| Description de l’erreur | Aucun accord trouvé avec les identités : ’AS2Identity’::’Partner1’ et ’AS2Identity’::’Partner3’.| 
| Action requise | En-tête AS2-From ou AS2-To non valide configuré pour l’accord. </br> Corrigez les en-têtes de message AS2 AS2-From ou AS2-To de l’accord de manière à ce que les ID AS2 des en-têtes de message AS2 correspondent aux configurations de l’accord. |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* En-têtes de message AS2 manquants  

|   |   |  
|---|---|
| Description de l’erreur| En-têtes AS2 non valides. L’en-tête « AS2-To » ou « AS2-From » est vide.| 
| Action requise | Un message AS2 ne contenant pas d’en-tête AS2-From ou AS2-To a été reçu. </br> Vérifiez les en-têtes AS2-From et AS2-To de message AS2 et corrigez-les en fonction de la configuration de l’accord. |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Corps et en-têtes de message AS2 manquants    

|   |   |  
|---|---|
| Description de l’erreur| Le contenu de la requête est nul ou vide. | 
| Action requise | Un message AS2 ne comportant pas de corps de message a été reçu. |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* Échec du déchiffrement de message AS2

|   |   | 
|---|---|
| Description de l’erreur |  [processed/Error: decryption-failed] | 
| Action requise | Ajoutez @base64ToBinary au message AS2 avant de l’envoyer au partenaire. 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* Échec du déchiffrement du MDN

|   |   | 
|---|---|
| Description de l’erreur |  [processed/Error: decryption-failed] | 
| Action requise | Ajoutez @base64ToBinary au MDN avant de l’envoyer au partenaire. 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Certificat de signature manquant

|   |   |  
|---|---|
| Description de l’erreur| Le certificat de signature n’a pas été configuré pour le tiers AS2. </br> AS2-From : partner1 AS2-To : partner2 | 
| Action requise | Configurez les paramètres d’accord AS2 avec le certificat approprié pour la signature. |
|  |  | 

## <a name="x12-and-edifact"></a>X12 et EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Espace de début ou de fin trouvé    
    
|   |   | 
|---|---|
| Description de l’erreur | Erreur rencontrée lors de l’analyse. Le document informatisé EDIFACT ayant l’id ’123456’ contenu dans l’échange (sans groupe) ayant l’id ’987654’, l’id d’expéditeur ’Partner1’, l’id de destinataire ’Partner2’ est interrompu avec les erreurs suivantes : Séparateur de début trouvé. |
| Action requise | Les paramètres d’accord doivent être configurés de manière à autoriser les espaces de début et de fin. </br> Modifiez les paramètres d’accord de manière à autoriser les espaces de début et de fin. |
|   |   |

![Autoriser l’espace](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a>* La vérification de doublons a été activée dans l’accord

|   |   | 
|---|---| 
| Description de l’erreur | Numéro de contrôle en double |
| Action requise | Cette erreur indique que le message reçu contient des numéros de contrôle en double. </br> Corrigez le numéro de contrôle et renvoyez le message. |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a>* Schéma manquant dans l’accord

|   |   | 
|---|---| 
| Description de l’erreur | Erreur rencontrée lors de l’analyse. Le document informatisé X12 possédant l’id ’564220001’ contenu dans le groupe fonctionnel d’id ’56422’, dans l’échange possédant l’id ’000056422’, l’id d’expéditeur ’12345678       ’ et l’id de destinataire ’87654321       ’ est interrompu avec les erreurs suivantes : « Le type de document du message est inconnu, et n’a pas été résolu en l’un des schémas existants configurés dans l’accord. » |
| Action requise | Configurez le schéma dans les paramètres d’accord.  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a>* Schéma incorrect dans l’accord

|   |   | 
|---|---| 
| Description de l’erreur | Le type de document du message est inconnu, et n’a pas été résolu en l’un des schémas existants configurés dans l’accord. |
| Action requise | Configurez le schéma correct dans les paramètres d’accord.  |
|   |   |

## <a name="flat-file"></a>Fichier plat

### <a name="-input-message-with-no-body"></a>* Message d’entrée sans corps

|   |   | 
|---|---|
| Description de l’erreur | Modèle non valide. Impossible de traiter les expressions de langage de gabarit dans les entrées d’action ’Flat_File_Decoding’ à la ligne « 1 » et à la colonne « 1902 » : La propriété « content » requise attend une valeur, mais a reçu null. Chemin d’accès « . ». |
| Action requise | Cette erreur indique que le message d’entrée ne contient pas de corps. |
|   |   | 

## <a name="learn-more"></a>En savoir plus
[En savoir plus sur Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)