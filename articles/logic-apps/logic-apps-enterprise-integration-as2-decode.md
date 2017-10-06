---
title: messages aaaDecode AS2 - Azure Logic Apps | Documents Microsoft
description: "Comment toouse hello décodeur AS2 dans hello Enterprise Integration Pack pour Azure Logic Apps"
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
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Décoder les messages AS2 pour Azure Logic Apps avec hello Pack d’intégration Enterprise 

tooestablish sécurité et fiabilité lors de la transmission des messages, utilisez le connecteur de message AS2 de décoder hello. Ce connecteur fournit des fonctionnalités de signature numérique, de cryptage et d’accusés de réception par vérification des notifications de messages (Message Disposition Notifications, MDN).

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un connecteur de message AS2 de décoder hello intégration compte toouse.
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat AS2](logic-apps-enterprise-integration-as2.md) déjà défini dans votre compte d’intégration

## <a name="decode-as2-messages"></a>Décoder des messages AS2

1. [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

2. connecteur de message AS2 de décoder de Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande. Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.

3.  Dans la zone de recherche de hello, entrez « AS2 » pour votre filtre. Sélectionnez **AS2 - Decode AS2 Message**.
   
    ![Recherchez « AS2 »](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion. Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.
   
    ![Créer une connexion d’intégration](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement. |

5.  Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire. toofinish création de votre connexion, choisissez **créer**.

    ![détails de la connexion d’intégration](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. Une fois que votre connexion est créée, comme indiqué dans cet exemple, sélectionnez **corps** et **en-têtes** à partir de hello demander des sorties.
   
    ![connexion d’intégration créée](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    Par exemple :

    ![Sélectionnez le corps et les en-têtes à partir des sorties de requête.](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>Détails sur le décodeur AS2

connecteur de décoder les AS2 Hello effectue ces tâches : 

* Traite les en-têtes AS2/HTTP
* Vérifie la signature de hello (si configuré)
* Déchiffre les messages de type hello (si configuré)
* Décompresse le message de type hello (si configuré)
* Rapproche un MDN reçu avec le message sortant original de hello
* Met à jour et met en corrélation les enregistrements dans la base de données de non-répudiation hello
* Écrit les enregistrements pour le rapport d’état AS2
* contenu de charge utile de sortie Hello est codées en base64
* Détermine si un MDN est requis et si hello MDN doit être synchrone ou asynchrone basée sur la configuration dans l’accord AS2
* Génère un MDN synchrone ou asynchrone (basé sur les configurations de l’accord)
* Définit les propriétés et les jetons de corrélation hello sur hello MDN

## <a name="try-this-sample"></a>Testez cet exemple

tootry déploiement d’un scénario de AS2 logique entièrement opérationnelle application et des exemples, consultez hello [AS2 scénario et du modèle d’application logique](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/as2/). 

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md) 

