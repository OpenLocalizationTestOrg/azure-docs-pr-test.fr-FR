---
title: solutions aaaCreate B2B - Azure Logic Apps | Documents Microsoft
description: "Recevoir des données dans les applications de la logique à l’aide des fonctionnalités de hello B2B Bonjour Pack d’intégration Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Recevoir des données dans les applications logique avec les fonctionnalités de B2B hello Bonjour Pack d’intégration Enterprise

Après avoir créé un compte d’intégration qui a des partenaires et des accords, vous êtes prêt toocreate un workflow toobusiness (B2B) d’entreprise pour votre application logique avec hello [Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Composants requis

toouse hello AS2 et X12 actions, vous devez disposer d’un compte d’intégration d’entreprise. En savoir plus [comment toocreate une intégration compte](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Créer une application logique avec des connecteurs B2B

Suivez ces étapes toocreate un B2B logique application utilise hello AS2 et X12 données de tooreceive d’actions à partir d’un partenaire commercial :

1. Créer une application logique, puis [lier votre compte d’intégration application tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Ajouter un **demande - HTTP lors de la demande est reçue** application logique de tooyour déclencheur.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. tooadd hello **AS2 de décoder** action, sélectionnez **ajouter une action**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter tous les toohello actions une que vous le souhaitez, entrez le mot de hello **as2** dans la zone de recherche hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Sélectionnez hello **AS2 - message AS2 de décoder** action.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Ajouter hello **corps** que vous souhaitez toouse en tant qu’entrée. Dans cet exemple, sélectionnez hello le corps de requête HTTP de hello que déclencheurs hello application logique. Ou entrez une expression qui transmet les en-têtes hello Bonjour **en-têtes** champ :

    @triggerOutputs()['headers']

7. Ajouter hello requis **en-têtes** pour AS2, que vous pouvez trouver dans les en-têtes de demande hello HTTP. Dans cet exemple, sélectionnez les en-têtes de requête HTTP de hello hello cette application de la logique de déclencheur hello.

8. À présent ajouter l’action du message Decode X12 hello. Sélectionnez **Ajouter une action**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter tous les toohello actions une que vous le souhaitez, entrez le mot de hello **x12** dans la zone de recherche hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Sélectionnez hello **X12-décoder X12 message** action.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Maintenant, vous devez spécifier hello toothis d’entrée action. Cette entrée est sortie hello à partir de l’action de AS2 hello précédente.

    Hello contenu réel du message est dans un objet JSON et encodage base64, vous devez spécifier une expression en tant qu’entrée de hello. 
    Entrez hello expression Bonjour suivante **X12 plats tooDECODE MESSAGE de fichier** champ d’entrée :
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    Maintenant ajouter des étapes, les données de salutation X12 toodecode reçu hello partenaire commercial et les éléments dans un objet JSON de sortie. 
    partenaire hello toonotify hello de données a été reçu, vous pouvez envoyer une réponse contenant hello AS2 Notification MDN (Message Disposition) dans une Action de réponse HTTP.

12. tooadd hello **réponse** action, choisissez **ajouter une action**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter tous les toohello actions une que vous le souhaitez, entrez le mot de hello **réponse** dans la zone de recherche hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Sélectionnez hello **réponse** action.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello MDN à partir de la sortie de hello Hello **message de décodage X12** action, réponse hello **corps** champ avec cette expression :

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Enregistrez votre travail.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

Vous avez maintenant terminé la configuration de votre application logique B2B. Dans une application réelle, vous souhaiterez toostore hello décodée X12 les données dans un magasin de données ou d’application (LOB) de line-of-business. tooconnect vos propres applications métier et utilisez ces API dans votre application logique, vous pouvez ajouter d’autres actions ou écrire des API personnalisées.

## <a name="features-and-use-cases"></a>Fonctionnalités et cas d’usage

* X12 Hello AS2 décoder et encoder les actions permettent d’échanger des données entre les partenaires commerciaux à l’aide de protocoles standard dans les applications de la logique.
* tooexchange des données avec des partenaires commerciaux, vous pouvez utiliser AS2 et X12 avec ou sans eux.
* actions de B2B Hello vous aider à créer facilement des partenaires et des accords dans votre compte d’intégration et de les utiliser dans une application logique.
* En étendant votre application logique avec d’autres actions, vous pouvez envoyer et recevoir des données vers et depuis d’autres applications et services tels que SalesForce.

## <a name="learn-more"></a>En savoir plus
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md)
