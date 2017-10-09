---
title: messages aaaEncode AS2 - Azure Logic Apps | Documents Microsoft
description: Comment toouse hello encodeur AS2 Bonjour Enterprise Integration Pack pour Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Encoder les messages AS2 pour Azure Logic Apps avec hello Pack d’intégration Enterprise

tooestablish sécurité et fiabilité lors de la transmission des messages, utilisez le connecteur de message AS2 d’encoder hello. Ce connecteur fournit une signature numérique, le chiffrement et les accusés de réception par le biais des Notifications MDN (Message Disposition), ce qui entraîne également des toosupport de Non répudiation.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un connecteur de message AS2 d’encoder hello intégration compte toouse.
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat AS2](logic-apps-enterprise-integration-as2.md) déjà défini dans votre compte d’intégration

## <a name="encode-as2-messages"></a>Encoder des messages AS2

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. connecteur de message AS2 d’encoder de Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande. Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.

3.  Dans la zone de recherche de hello, entrez « AS2 » pour votre filtre. Sélectionnez **AS2 - Encode AS2 Message**.
   
    ![Recherchez « AS2 »](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion. Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect. 
   
    ![créer le compte de connexion toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement. |

5.  Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire. toofinish création de votre connexion, choisissez **créer**.
   
    ![détails de la connexion d’intégration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Une fois que votre connexion est créée, comme indiqué dans cet exemple, fournissez les informations relatives **AS2-de**, **AS2-tooidentifiers** tel que configuré dans votre contrat, et **corps**, qui est charge utile du message Hello.
   
    ![remplir les champs obligatoires](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Détails sur l’encodeur AS2

connecteur d’encoder un AS2 Hello effectue ces tâches : 

* Applique les en-têtes AS2/HTTP
* Signe les messages sortants (si configuré)
* Chiffre les messages sortants (si configuré)
* Compresse le message de type hello (si configuré)

## <a name="try-this-sample"></a>Testez cet exemple

tootry déploiement d’un scénario de AS2 logique entièrement opérationnelle application et des exemples, consultez hello [AS2 scénario et du modèle d’application logique](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/as2/). 

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

