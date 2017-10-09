---
title: "aaaLogic B2B applications edifact décoder résoudre UNH2.5 - Azure Logic Apps | Documents Microsoft"
description: "Décodage EDIFACT B2B contenant un segment UNH2.5 - Azure Logic Apps"
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
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Comment toohandle EDIFACT documents ayant UNH2.5 segment
Lorsque UNH2.5 est présent dans le document de hello EDIFACT, il est utilisé pour la recherche de schéma. 

Exemple : champ UNH de hello est **EAN008** dans le message de salutation EDIFACT  
UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'  

Message de type hello toohandle toofollow étapes 
1. Mettre à jour le schéma de hello
2. Vérifiez les paramètres de l’accord hello  

## <a name="update-hello-schema"></a>Mettre à jour le schéma de hello
message de type hello tooprocess, vous devez toodeploy un schéma avec le nom de nœud racine hello UNH2.5.  Pour obtenir un exemple, nom racine du schéma hello serait **EFACT_D03B_ORDERS_EAN008**  

Pour chaque D03B_ORDERS avec un segment UNH2.5 différent, vous devriez toodeploy un schéma individuel.  

## <a name="add-schema-toohello-edifact-agreement"></a>Ajouter un accord EDIFACT toohello schéma
### <a name="edifact-decode"></a>Décodage EDIFACT
tooDecode hello message entrant, configurer hello schéma Bonjour EDIFACT les paramètres de réception de contrat
1. Ajouter le compte d’intégration hello schéma toohello    
2. Configurer le schéma de hello Bonjour EDIFACT les paramètres de réception de contrat. 
3. Sélectionnez un accord EDIFACT et cliquez sur **Modifier au format JSON**.  Ajouter la valeur UNH2.5 Bonjour accord de réception **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>Encodage EDIFACT
tooEncode hello message entrant, configurer le schéma de hello dans les paramètres d’envoi hello EDIFACT accord
1. Ajouter le compte d’intégration hello schéma toohello    
2. Configurer le schéma de hello dans les paramètres d’envoi un accord EDIFACT hello. 
3. Sélectionnez un accord EDIFACT et cliquez sur **Modifier au format JSON**.  Ajouter la valeur UNH2.5 Bonjour envoyer l’accord **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les contrats de compte d’intégration](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  