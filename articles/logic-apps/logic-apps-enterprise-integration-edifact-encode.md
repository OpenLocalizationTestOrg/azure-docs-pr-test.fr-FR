---
title: les messages EDIFACT aaaEncode - Azure Logic Apps | Documents Microsoft
description: "Valider EDI et de générer du code XML avec l’encodeur de message EDIFACT Bonjour Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Encoder les messages EDIFACT pour Azure Logic Apps avec hello Pack d’intégration Enterprise

Avec le connecteur de message EDIFACT d’encoder hello, vous pouvez valider EDI et des propriétés spécifiques aux partenaires, générer un document XML pour chaque document informatisé et demander un accusé de réception technique, l’accusé de réception fonctionnel ou les deux.
toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un connecteur de message EDIFACT d’encoder hello intégration compte toouse. 
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration

## <a name="encode-edifact-messages"></a>Encoder des messages EDIFACT

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. connecteur de message EDIFACT d’encoder de Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande. Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.

3.  Dans la zone de recherche de hello, entrez « EDIFACT » comme filtre. Sélectionnez **encoder le Message EDIFACT par nom de l’accord** ou **Encode tooEDIFACT message identités**.
   
    ![recherche EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion. Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.

    ![créer une connexion de compte d’intégration](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement. |

5.  Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire. toofinish création de votre connexion, choisissez **créer**.

    ![détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    Votre connexion est maintenant créée.

    ![connexion de compte d’intégration créée](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Encode EDIFACT Message par nom de contrat

Si vous choisissez des messages EDIFACT tooencode par le nom de l’accord, ouvrez hello **accord nom de EDIFACT** liste, entrez ou sélectionnez le nom de votre accord EDIFACT. Entrez tooencode de message XML hello.

![Entrez le nom de l’accord EDIFACT et tooencode de message XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Encode EDIFACT Message par identités

Si vous choisissez des messages EDIFACT tooencode par des identités, entrez l’identificateur de l’expéditeur hello, qualificateur de l’expéditeur, identificateur du récepteur et qualificateur du récepteur tel que configuré dans votre accord EDIFACT. Sélectionnez tooencode de message XML hello.

![Fournir des identités d’expéditeur et récepteur, sélectionnez tooencode de message XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Détails sur l’encodage EDIFACT

connecteur d’encoder un EDIFACT Hello effectue ces tâches : 

* Accord de hello en hello expéditeur qualificateur et identificateur et qualificateur du récepteur et l’identificateur de correspondance
* Sérialise l’échange EDI de hello, convertir des messages encodés en XML dans les documents informatisés dans l’échange de hello.
* Applique les segments d’en-tête et de code de fin du document informatisé
* Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant
* Remplace les séparateurs dans les données de charge utile de hello
* Valide l’EDI et les propriétés spécifiques au partenaire
  * Validation du schéma des éléments de données de document informatisé hello contre le schéma de message hello.
  * Validation EDI effectuée sur les éléments de données du document informatisé.
  * Validation étendue effectuée sur les éléments de données du document informatisé
* Génère un document XML pour chaque document informatisé.
* Demande un accusé de réception fonctionnel et/ou technique (si configuré).
  * En tant qu’un accusé de réception technique, message de type hello CONTRL indique la réception d’un échange.
  * Comme un accusé de réception fonctionnel, message de type hello CONTRL indique l’acceptation ou rejet de l’échange de salutation reçue, groupe ou les messages, avec une liste d’erreurs ou des fonctionnalités non prises en charge

## <a name="view-swagger-file"></a>Afficher le fichier Swagger
Détails de Swagger tooview hello pour le connecteur d’EDIFACT hello, consultez [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

