---
title: traiter les messages aaaBatch comme un groupe ou de la collection - Azure Logic Apps | Documents Microsoft
description: "Envoyer et recevoir des messages à traiter par lots dans les applications logiques"
keywords: lot, traitement par lots
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Envoyer, recevoir et traiter par lots des messages dans les applications logiques

tooprocess les messages dans des groupes, vous pouvez envoyer tooa d’éléments, ou les messages, données *lot*, puis traite ces éléments en tant que lot. Cette approche est utile lorsque vous souhaitez toomake que l’option des éléments de données sont regroupés de manière spécifique et sont traitées ensemble. 

Vous pouvez créer des applications de la logique qui reçoivent des éléments en tant que lot à l’aide de hello **lot** déclencheur. Vous pouvez ensuite créer des applications de la logique qui envoient des éléments tooa lot à l’aide de hello **lot** action.

Cette rubrique montre comment créer une solution de traitement par lot en effectuant les tâches suivantes : 

* [Créer une application logique destinée à recevoir et collecter des éléments regroupés dans un lot](#batch-receiver). Cette application de la logique « récepteur lot » spécifie toomeet critères hello lot nom et la version avant application logique de récepteur hello libère et traite les éléments. 

* [Créer une application de la logique qui envoie des éléments tooa lot](#batch-sender). Cette application de la logique « expéditeur lot » Spécifie l’emplacement des éléments toosend, qui doivent être une application de la logique de récepteur lot existante. Vous pouvez également spécifier une clé unique, par exemple, un numéro de client, trop de « partition » ou divisez, lot cible de hello en sous-ensembles, en fonction de cette clé. De cette façon, tous les éléments associés à cette clé sont collectés et traités ensemble. 

## <a name="requirements"></a>Configuration requise

toofollow cet exemple, vous avez besoin de ces éléments :

* Un abonnement Azure. Si vous ne disposez d’aucun abonnement, vous pouvez [commencer par créer gratuitement un compte Azure](https://azure.microsoft.com/free/). Sinon, vous pouvez souscrire à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/).

* Connaissance de base [comment toocreate logique applications](../logic-apps/logic-apps-create-a-logic-app.md) 

* Un compte de courrier de n’importe quel [fournisseur de messagerie pris en charge par Azure Logic Apps](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Créer des applications logiques destinées à recevoir des messages regroupés dans un lot

Avant d’envoyer le traitement par lots de messages tooa, vous devez d’abord créer une application de logique « récepteur lot » avec hello **lot** déclencheur. De cette façon, vous pouvez sélectionner cette application logique de récepteur quand vous créez une application de logique hello expéditeur. Pour le récepteur hello, vous spécifiez le nom du lot hello, les critères de déclenchement et les autres paramètres. 

Applications de la logique de l’expéditeur doivent connaître où toosend éléments, tandis que les applications de la logique de récepteur n’avez pas besoin tooknow n’est pas défini sur les expéditeurs hello.

1. Bonjour [portail Azure](https://portal.azure.com), créez une application de logique avec ce nom : « BatchReceiver » 

2. Dans le Concepteur d’applications logique, ajouter hello **lot** déclencheur qui démarre le workflow d’application logique. Dans la zone de recherche de hello, entrez « batch » comme filtre. Sélectionnez le déclencheur **Lot – Traiter les messages par lots**.

   ![Ajout du déclencheur Lot](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Fournissez un nom pour le traitement par lots hello et spécifiez les critères pour libérer le lot de hello, par exemple :

   * **Nom du lot**: hello nom utilisé tooidentify hello lot, c'est-à-dire « TestBatch » dans cet exemple.
   * **Nombre de messages**: hello du nombre de messages toohold en tant que lot avant de libérer pour le traitement, qui est « 5 » dans cet exemple.

   ![Détails à fournir concernant le déclencheur Lot](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Ajouter une autre action qui envoie un message électronique au déclenchement de déclenchement du lot hello. Chaque lot de hello temps comporte cinq éléments, hello logique application envoie un message électronique.

   1. Sous le déclenchement du lot hello, choisissez **+ nouvelle étape** > **ajouter une action**.

   2. Dans la zone de recherche de hello, entrez « email » comme filtre.
   Sélectionnez un connecteur de messagerie en fonction de votre fournisseur de messagerie.
   
      Par exemple, si vous avez un compte professionnel ou scolaire, sélectionnez Connecteur Outlook Office 365 de hello. 
      Si vous avez un compte Gmail, sélectionnez le connecteur de Gmail hello.

   3. Sélectionnez cette action pour votre connecteur : **{*fournisseur de messagerie*} - Envoyer un message électronique**

      Par exemple :

      ![Sélection de l’action « Envoyer un message électronique » pour votre fournisseur de messagerie](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. Si vous n’avez pas déjà créé une connexion pour votre fournisseur de messagerie, entrez votre adresse e-mail et votre mot de passe lorsque vous êtes invité à vous authentifier. En savoir plus sur [l’authentification à l’aide d’une adresse e-mail et d’un mot de passe](../logic-apps/logic-apps-create-a-logic-app.md).

6. Définir les propriétés de hello pour action hello que vous venez d’ajouter.

   * Bonjour **à** , entrez l’adresse de messagerie du destinataire hello. 
   À des fins de test, vous pouvez utiliser votre propre adresse e-mail.

   * Bonjour **sujet** boîte lorsque hello **contenu dynamique** liste apparaît, sélectionnez hello **nom de la Partition** champ.

     ![Dans la liste « Contenu dynamique » hello, sélectionnez « Nom de Partition »](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     Dans une section ultérieure, vous pouvez spécifier une clé de partition unique que le divise hello lot cible dans la logique définit toowhere, vous pouvez envoyer des messages. 
     Chaque jeu possède un numéro unique qui est généré par l’application de la logique d’expéditeur hello. 
     Cette fonctionnalité vous permet d’utiliser un lot unique avec plusieurs sous-ensembles et définir chaque sous-ensemble avec nom hello que vous fournissez.

   * Bonjour **corps** boîte lorsque hello **contenu dynamique** liste apparaît, sélectionnez hello **Id de Message** champ.

     ![Pour « Corps », sélectionnez « ID de message »](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Étant donné que l’entrée hello pour l’action d’envoi de message hello est un tableau, hello concepteur ajoute automatiquement une **pour chaque** boucle autour hello **envoyer un courrier électronique** action. 
     Cette boucle effectue une action interne de hello sur chaque élément dans un lot de hello. 
     Par conséquent, avec hello lot déclencheur ensemble toofive éléments, vous obtenez des cinq messages électroniques que chaque déclencheur hello de temps est activé.

7.  Maintenant que vous avez créé l’application logique réceptrice de lots, enregistrez-la.

    ![Enregistrer votre application logique](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Créer des applications de la logique qui envoient le traitement par lots de messages tooa

À présent créer une ou plusieurs applications de logique qui envoient des éléments toohello lot est définie par l’application de la logique de récepteur hello. Pour un expéditeur hello, vous spécifiez application logique de récepteur hello et nom du lot, contenu du message et tous les autres paramètres. Vous pouvez éventuellement fournir un lot de hello de toodivide clé de partition unique dans éléments toocollect de sous-ensembles avec cette clé.

Applications de la logique de l’expéditeur doivent connaître où toosend éléments, tandis que les applications de la logique de récepteur n’avez pas besoin tooknow n’est pas défini sur les expéditeurs hello.

1. Créez une autre application logique et nommez-la « BatchSender ».

   1. Dans la zone de recherche de hello, entrez « recurrence » comme filtre. 
   Sélectionnez le déclencheur **Planification - Récurrence**

      ![Ajouter le déclencheur de hello « Planification Recurrence »](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Définir la fréquence de hello et intervalle toorun hello expéditeur logique application toutes les minutes.

      ![Définition de la fréquence et de l’intervalle pour le déclencheur Récurrence](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Ajouter une nouvelle étape pour l’envoi de lot tooa de messages.

   1. Sous le déclencheur de périodicité hello, choisissez **+ nouvelle étape** > **ajouter une action**.

   2. Dans la zone de recherche de hello, entrez « batch » comme filtre. 

   3. Sélectionnez cette action : **envoyer des messages toobatch : choisissez un flux de travail Logic Apps avec déclenchement du lot**

      ![Sélectionnez « Envoyer des messages toobatch »](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Maintenant, sélectionnez l’application logique « BatchReceiver » créée précédemment, qui s’affiche désormais en tant qu’action.

      ![Sélection de l’application logique « BatchReceiver »](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > liste de Hello montre également toutes les autres applications de la logique qui ont des déclencheurs de lot.

3. Définir les propriétés de lot hello.

   * **Nom du lot**: nom du lot hello défini par l’application hello récepteur logique, qui est « TestBatch » dans cet exemple est validée lors de l’exécution.

     > [!IMPORTANT]
     > Assurez-vous que vous ne pas modifier le nom du lot hello, qui doit correspondre au nom de lot hello spécifié par l’application de la logique de récepteur hello.
     > Modification du nom de lot hello provoque l’expéditeur de hello toofail d’application logique.

   * **Contenu du message**: hello du contenu du message que vous souhaitez toosend. 
   Pour cet exemple, ajoutez cette expression que les insertions hello date et heure actuelles dans le message de type hello contenu que vous envoyez un lot de toohello :

     1. Hello lorsque **contenu dynamique** liste apparaît, choisissez **Expression**. 
     2. Entrez l’expression de hello **utcnow()**, puis choisissez **OK**. 

        ![Dans « Contenu du message », choisissez « Expression ». Entrez « utcnow() ».](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Définir une partition pour le traitement par lots hello. Bonjour « BatchReceiver » action, choisissez **Show advanced options**.

   * **Nom de partition**: un toouse clé de partition unique facultatif permettant de diviser le traitement par lots de hello cible. Pour cet exemple, ajoutez une expression qui génère un nombre aléatoire compris entre 1 et 5.
   
     1. Hello lorsque **contenu dynamique** liste apparaît, choisissez **Expression**.
     2. Entrez l’expression **rand(1,6)**.

        ![Définition d’une partition pour le lot cible](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        Cette fonction **rand** génère un nombre compris entre 1 et 5. 
        Vous divisez donc ce lot en cinq partitions numérotées, définies dynamiquement par cette expression.

   * **ID du message** : identificateur de message facultatif. Lorsqu’il est vide, c’est un GUID généré. 
   Pour cet exemple, laissez cette zone vide.

5. Enregistrez votre application logique. Votre application de la logique d’expéditeur ressemble exemple toothis similaire :

   ![Enregistrement de l’application logique](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Tester les applications logiques

tootest votre solution, de traitement par lot laisser vos applications logiques en cours d’exécution pendant quelques minutes. Bientôt, vous commencez à recevoir des messages électroniques dans les groupes de cinq, toutes les données avec hello même clé de partition.

Votre application de la logique BatchSender s’exécute chaque minute, génère un nombre aléatoire compris entre 1 et 5 et utilise ce numéro généré en tant que clé de partition hello pour le traitement par lots de hello cible où les messages sont envoyés. Chaque fois que les commandes hello a cinq éléments par hello même clé de partition, votre application de la logique BatchReceiver se déclenche et envoie un message pour chaque message.

> [!IMPORTANT]
> Lorsque vous avez terminé de test, assurez-vous que vous désactivez hello BatchSender logique application toostop envoi de messages et évitez de surcharger votre boîte de réception.

## <a name="next-steps"></a>Étapes suivantes

* [Créer des définitions d’application logique à l’aide de JSON](../logic-apps/logic-apps-author-definitions.md)
* [Créer une application sans serveur dans Visual Studio avec Azure Logic Apps et Azure Functions](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Gestion des exceptions et journalisation des erreurs pour les applications logiques](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
