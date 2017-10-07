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
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Liste des erreurs et des solutions Logic Apps B2B  
Cet article vous aide à comprendre les erreurs qui peuvent se produire dans le cadre des scénarios Logic Apps B2B et suggère des actions appropriées pour corriger ces erreurs.


## <a name="agreement-resolution"></a>Résolution d’accord

### <a name="no-agreement-found"></a>* Aucun accord trouvé 

|   |   |  
|---|---|
| Description de l’erreur | Aucun accord trouvé avec les paramètres de résolution d’accord|    
| Action requise | accord de Hello doit être ajouté toohello compte d’intégration avec des identités d’entreprise convenu.</br> les identités d’entreprise Hello doivent correspondre à l’ID de message d’entrée toohello|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Aucun accord trouvé avec les identités

|   |   | 
|---|---|
| Description de l’erreur | Aucun accord trouvé avec les identités : ’AS2Identity’::’Partner1’ et ’AS2Identity’::’Partner3’.| 
| Action requise | AS2 non valide-à partir d’ou AS2-tooconfigured pour l’accord. </br> Messages AS2 AS2-à partir d’ou en-têtes avec des configurations de contrat de message AS2-tooheaders ou contrat ID toomatch AS2 dans AS2 |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* En-têtes de message AS2 manquants  

|   |   |  
|---|---|
| Description de l’erreur| En-têtes AS2 non valides. L’en-tête « AS2-To » ou « AS2-From » est vide.| 
| Action requise | Réception d’un message AS2 ne contenant pas hello AS2-à partir d’ou AS2-tooor les deux en-têtes. </br> Vérifiez le message AS2 AS2-à partir d’et AS2-tooheaders et corrigez-les en fonction de la configuration de l’accord |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Corps et en-têtes de message AS2 manquants    

|   |   |  
|---|---|
| Description de l’erreur| contenu de la demande Hello est null ou vide | 
| Action requise | Réception d’un message AS2 ne contenant pas de corps de message hello |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* Échec du déchiffrement de message AS2

|   |   | 
|---|---|
| Description de l’erreur |  [processed/Error: decryption-failed] | 
| Action requise | Ajouter @base64ToBinary tooAS2Message avant d’envoyer toopartner 
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
| Action requise | Ajouter @base64ToBinary tooMDN avant d’envoyer toopartner 
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
| Description de l’erreur| Hello certificat de signature n'a pas été configuré pour le tiers AS2. </br> AS2-From : partner1 AS2-To : partner2 | 
| Action requise | Configurez les paramètres d’accord AS2 avec le certificat approprié pour la signature. |
|  |  | 

## <a name="x12-and-edifact"></a>X12 et EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Espace de début ou de fin trouvé    
    
|   |   | 
|---|---|
| Description de l’erreur | Erreur rencontrée lors de l’analyse. Hello document informatisé Edifact avec l’id ' 123456 'contenu dans l’échange (sans groupe) avec l’id ' 987654', id d’expéditeur 'Partner1', id de destinataire 'Partner2' est interrompu avec les erreurs suivantes : début à la fin de séparateur trouvé |
| Action requise | toobe de paramètres d’accord Hello configuré tooallow de début et de fin d’espace. </br> Modifier le contrat paramètres tooallow début et de fin d’espace |
|   |   |

![Autoriser l’espace](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Check en double a activé dans l’accord de hello

|   |   | 
|---|---| 
| Description de l’erreur | Numéro de contrôle en double |
| Action requise | Cette erreur indique que message de salutation reçu a des numéros de contrôle dupliqués. </br> Corrigez le numéro de contrôle hello et renvoyez le message de type hello |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Schéma manquant dans le contrat de hello

|   |   | 
|---|---| 
| Description de l’erreur | Erreur rencontrée lors de l’analyse. jeu de transactions Hello X12 avec l’id '564220001' contenue dans le groupe fonctionnel avec l’id '56422', dans l’échange avec l’id '000056422', id d’expéditeur ' 12345678', id de destinataire ' 87654321' est interrompu avec les erreurs suivantes « message de salutation a un type de document inconnu PE et n’a pas résolu tooany de schémas existants de hello configuré dans l’accord de hello » |
| Action requise | Configurer le schéma dans les paramètres de l’accord hello  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Schéma incorrect dans l’accord de hello

|   |   | 
|---|---| 
| Description de l’erreur | message de type Hello a un type de document inconnu et tooany de schémas existants de hello configurés dans hello accord n’a pas été résolue. |
| Action requise | Configurer le schéma correct dans les paramètres de l’accord hello  |
|   |   |

## <a name="flat-file"></a>Fichier plat

### <a name="-input-message-with-no-body"></a>* Message d’entrée sans corps

|   |   | 
|---|---|
| Description de l’erreur | Modèle non valide. Les expressions de langage de modèle tooprocess impossible dans les entrées d’action 'Flat_File_Decoding' à la ligne '1' et la colonne '1902' : ' requise de la propriété « content » attend une valeur, mais dispose null. Chemin d’accès « . ». |
| Action requise | Cette erreur indique le message d’entrée de type hello ne contient pas un corps |
|   |   | 

## <a name="learn-more"></a>En savoir plus
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md)
