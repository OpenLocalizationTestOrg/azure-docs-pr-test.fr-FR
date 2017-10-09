---
title: messages aaaEncode X12 - Azure Logic Apps | Documents Microsoft
description: "Validation EDI et convertir encodé en XML messages avec X12 message encodeur Bonjour Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Encoder X12 messages pour Azure Logic Apps avec hello Pack d’intégration Enterprise

Avec le connecteur de message hello Encode X12, vous pouvez valider EDI et des propriétés spécifiques aux partenaires, convertir des messages encodés en XML en documents informatisés dans l’échange de hello et demander un accusé de réception technique, l’accusé de réception fonctionnel ou les deux.
toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un connecteur d’intégration compte toouse hello Encode X12 message.
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration

## <a name="encode-x12-messages"></a>Encoder des messages X12

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. connecteur de message d’encodage X12 Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande. Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.

3.  Dans la zone de recherche de hello, entrez « x12 » pour votre filtre. Sélectionnez **X12-Encoder tooX12 message par le nom de l’accord** ou **X12-Encoder tooX12 message par identités**.
   
    ![Recherchez « x12 »](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion. Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect. 
   
    ![connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement. |

5.  Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire. toofinish création de votre connexion, choisissez **créer**.

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    Votre connexion est maintenant créée.

    ![détails de connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Encode X12 message par nom de contrat

Si vous avez choisi de messages de tooencode X12 par le nom de l’accord, ouvrez hello **nom de X12 accord** liste, entrez ou sélectionnez votre X12 existant accord. Entrez tooencode de message XML hello.

![Entrez X12 tooencode de message XML et le nom de contrat](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Encode X12 message par identités

Si vous choisissez les messages tooencode X12 d’identités, entrez identificateur de l’expéditeur hello, qualificateur de l’expéditeur, identificateur du récepteur et qualificateur du récepteur tel que configuré dans votre X12 accord. Sélectionnez tooencode de message XML hello.
   
![Fournir des identités d’expéditeur et récepteur, sélectionnez tooencode de message XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>Détails sur X12 Encode

connecteur d’encodage Hello X12 effectue ces tâches :

* Résolution du contrat en faisant correspondre les propriétés de contexte de l’expéditeur et du récepteur.
* Sérialise l’échange EDI de hello, convertir des messages encodés en XML dans les documents informatisés dans l’échange de hello.
* Applique les segments d’en-tête et de code de fin du document informatisé
* Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant
* Remplace les séparateurs dans les données de charge utile de hello
* Valide l’EDI et les propriétés spécifiques au partenaire
  * Validation du schéma des éléments de données de document informatisé hello contre le schéma de message de type hello
  * Validation EDI effectuée sur les éléments de données du document informatisé.
  * Validation étendue effectuée sur les éléments de données du document informatisé
* Demande un accusé de réception fonctionnel et/ou technique (si configuré).
  * Suite à la validation de l’en-tête, un accusé de réception technique est généré. accusé de réception technique Hello signale les États hello du traitement hello d’un en-tête de l’échange et le code de fin par le récepteur d’adresse hello
  * Suite à la validation du corps, un accusé de réception fonctionnel est généré. Hello accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement hello a reçu de document

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/x12/). 

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

