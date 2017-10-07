---
title: aaaCreate votre premier flux de travail entre les applications cloud et les services de cloud computing - Azure Logic Apps | Documents Microsoft
description: "Automatisez les processus d’entreprise dans le cas de scénarios d’intégration des systèmes et des Applications d’Entreprise (IAE) en créant et en exécutant des flux de travail dans Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "flux de travail, applications cloud, services cloud, processus d’entreprise, intégration de systèmes, intégration d’applications d’entreprise, IAE"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Créer votre première application logique tooautomate processus entre les applications cloud et les services de cloud computing

Vous pouvez automatiser des processus métier plus facilement et rapidement lorsque vous créez et exécutez des flux de travail et ce, sans avoir besoin d’écrire la plus petite ligne de code, grâce à [Azure Logic Apps](logic-apps-what-are-logic-apps.md). Ce premier exemple montre comment toocreate un workflow d’application logique de base qui vérifie un RSS flux pour le nouveau contenu sur un site Web. Lorsque de nouveaux éléments s’affichent dans les flux du site Web de hello, hello logique application envoie par courrier électronique à partir d’un compte Outlook ou Gmail.

toocreate et exécuter une application logique, vous avez besoin de ces éléments :

* Un abonnement Azure. Si vous ne disposez d’aucun abonnement, vous pouvez [commencer par créer gratuitement un compte Azure](https://azure.microsoft.com/free/). Sinon, vous pouvez souscrire à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/).

  Votre abonnement Azure est utilisé pour la facturation relative à l’utilisation des applications logiques. Découvrez le fonctionnement du [contrôle de l’utilisation](../logic-apps/logic-apps-pricing.md) et de la [tarification](https://azure.microsoft.com/pricing/details/logic-apps) pour les applications logiques Azure.

En outre, cet exemple nécessite les éléments suivants :

* Un compte Gmail, Office 365 Outlook ou Outlook.com

    > [!TIP]
    > Si vous disposez d’un [compte Microsoft](https://account.microsoft.com/account) personnel, vous possédez un compte Outlook.com. Sinon, si vous disposez d’un compte Azure professionnel ou scolaire, vous possédez un compte **Office 365 Outlook**.

* Un tooa lien du site Web flux RSS. Cet exemple utilise hello [flux RSS pour les récits supérieur à partir du site Web de CNN.com hello](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Ajouter un déclencheur qui démarre votre flux de travail

A [ *déclencheur* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) est un événement qui démarre le workflow d’application logique et hello premier élément qui a besoin votre application logique.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").

2. Dans le menu de gauche hello, choisissez **nouveau** > **intégration** > **application logique** comme indiqué ici :

     ![portail Azure, nouveau, intégration d’entreprise, application logique](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > Vous pouvez également choisir **nouveau**, puis dans la zone de recherche de hello, tapez `logic app`, puis appuyez sur ENTRÉE. Ensuite, choisissez **Application logique** > **Créer**.

3. Nommez votre application logique et sélectionnez votre abonnement Azure. Créez ou sélectionnez un groupe de ressources Azure, qui permet d’organiser et de gérer des ressources Azure liées. Enfin, sélectionnez emplacement du centre de données hello pour l’hébergement de votre application logique. Lorsque vous êtes prêt, choisissez **code confidentiel toodashboard** , puis **créer**.

     ![Détails de l’application logique](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Lorsque vous sélectionnez **toodashboard du code confidentiel**, votre application logique apparaît sur hello du tableau de bord Azure après le déploiement et s’ouvre automatiquement. Si votre application logique n’apparaît pas dans le tableau de bord hello sur hello **toutes les ressources** vignette, choisissez **consultez plus**, puis sélectionnez votre application logique. Ou, dans le menu de gauche hello, choisissez **davantage de services**. Sous **Intégration d’entreprise**, choisissez **Applications logiques** et sélectionnez votre application logique.

4. Lorsque vous ouvrez votre logique d’application pour hello première fois, hello Concepteur de logique d’application affiche les modèles que vous pouvez utiliser tooget a démarré. Pour l’instant, choisissez **Application logique vide**, afin de développer votre application logique à partir de zéro.

    Hello Concepteur d’application logique s’ouvre et affiche les services disponibles et *déclencheurs* que vous pouvez utiliser dans votre application logique.

5. Dans la zone de recherche de hello, tapez `RSS`, puis sélectionnez ce déclencheur : **RSS - lorsqu’un élément de flux est publié.** 

    ![Déclencheur RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Entrez un lien de hello pour les flux RSS du site Web de hello que vous souhaitez tootrack. 

     Vous pouvez également modifier la **fréquence** et l’**intervalle**. 
     Ces paramètres déterminent la fréquence à laquelle votre application logique recherche de nouveaux éléments et renvoie tous les éléments détectés pendant cet intervalle de temps.

     Pour cet exemple, nous allons vérifier tous les jours pour les récits supérieur publiées du site Web CNN toohello.

     ![Définir un déclencheur avec le flux RSS, la fréquence et l’intervalle](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Enregistrez votre travail pour commencer (Dans la barre de commandes du concepteur hello, choisissez **enregistrer**.)

   ![Enregistrer votre application logique](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Lorsque vous enregistrez, votre application logique soit disponible, mais actuellement, votre application logique vérifie uniquement les nouveaux éléments dans hello spécifié flux RSS. 
   toomake cet exemple plus utile, que nous ajoutons une action de votre application de la logique s’exécute après votre déclencheur est activé.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Ajouter une action qui répond tooyour déclencheur

Une [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) est une tâche effectuée par le flux de travail de votre application logique. Après avoir ajouté une application de la logique de déclencheur tooyour, vous pouvez ajouter un opérateur de tooperform action avec les données générées par ce déclencheur. Dans notre exemple, nous permet maintenant d’ajouter une action qui envoie un e-mail lorsque de nouveaux éléments s’affichent dans le flux RSS du site Web de hello.

1. Dans le Concepteur de hello, sous votre déclencheur, choisissez **nouvelle étape** > **ajouter une action** comme indiqué ici :

   ![Ajouter une action](media/logic-apps-create-a-logic-app/add-new-action.png)

   Hello concepteur affiche [connecteurs disponibles](../connectors/apis-list.md) afin que vous puissiez sélectionner une action tooperform lorsque le déclencheur est activé.

2. En fonction de votre compte de messagerie, les étapes hello pour Outlook ou Gmail.

   * messagerie toosend à partir de votre compte Outlook, dans la zone de recherche de hello, entrez `outlook`. Sous **Services**, choisissez **Outlook.com** pour les comptes Microsoft personnels, ou **Office 365 Outlook** pour les comptes Azure professionnels ou scolaires. 
   Sous **Actions**, sélectionnez **Envoi d’un courrier électronique**.

       ![Sélectionner l’action Envoi d’un courrier électronique d’Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * messagerie toosend à partir de votre compte Gmail, dans la zone de recherche de hello, entrez `gmail`. 
   Sous **Actions**, sélectionnez **Envoyer un e-mail**.

       ![Choisissez Gmail - Envoyer un e-mail.](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Lorsque vous êtes invité à entrer les informations d’identification, connectez-vous à hello username et password pour votre compte de messagerie. 

4. Fournir des détails de hello pour cette action, comme l’adresse de messagerie de destination hello et choisir les paramètres hello pour hello données tooinclude par courrier électronique de hello, par exemple :

   ![Sélectionnez les données tooinclude par courrier électronique](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Ainsi, si vous avez choisi Outlook, votre application logique peut ressembler à cet exemple :

    ![Application logique terminée](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Enregistrez vos modifications. (Dans la barre de commandes du concepteur hello, choisissez **enregistrer**.)

6. Vous pouvez maintenant exécuter votre application logique manuellement, à des fins de test. Dans la barre de commandes du concepteur hello, choisissez **exécuter**. Sinon, vous pouvez laisser votre application logique vérifier hello spécifié selon une planification hello que vous définissez des flux RSS.

   Si votre application logique détecte les nouveaux éléments, hello logique application envoie par courrier électronique qui inclut vos données sélectionnées. 
   Si aucun nouvel élément n’est trouvé, votre application logique ignore action hello qui envoie le courrier électronique.

7. toomonitor et vérification de votre application de la logique de l’exécuter et déclencher l’historique, dans le menu Application logique, choisissent **vue d’ensemble**.

   ![Surveiller et afficher l’historique de déclencheur et d’exécution de votre application logique](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Si vous ne trouvez pas les données de salutation que vous attendez, sur la barre de commandes hello, essayez de choisir **Actualiser**.

   toolearn plus en détail l’état de l’application de votre logique ou exécutez et déclencher l’historique ou toodiagnose votre application logique, consultez [dépanner votre application logique](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > Votre application logique poursuit son exécution jusqu’à ce que vous la désactiviez. tooturn hors de votre application pour l’instant, dans le menu Application logique, choisissez **vue d’ensemble**. Dans la barre de commandes hello, choisissez **désactiver**.

Félicitations ! Vous venez de configurer et d’exécuter votre première application logique de base. Vous avez également appris comment créer des flux de travaux qui automatisent les processus et intégrer des services cloud et applications cloud, aisément et sans rédiger la moindre ligne de code.

## <a name="manage-your-logic-app"></a>Gérer votre application logique

toomanage votre application, vous pouvez effectuer des tâches telles que vérifier l’état de hello, modifier, afficher l’historique, désactiver ou supprimer votre application logique.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").

2. Dans le menu de gauche hello, choisissez **davantage de services**. Sous **Intégration d’entreprise**, choisissez **Applications logiques**. Sélectionnez votre application logique. 

   Dans le menu d’application hello logique, vous pouvez trouver ces tâches de gestion d’application logique :

   |Task|Étapes| 
   |:---|:---| 
   | Afficher l’historique d’exécution et l’état de votre application, ainsi que des informations générales| Choisissez **Vue d’ensemble**.| 
   | Modifier votre application | Choisissez **Concepteur d’application logique**. | 
   | Afficher la définition JSON du flux de travail de votre application | Choisissez **Affichage du code de l’application logique**. | 
   | Afficher les opérations effectuées sur votre application logique | Choisissez **Journal d’activité**. | 
   | Afficher les anciennes versions de votre application logique | Choisissez **Versions**. | 
   | Désactiver votre application temporairement | Choisissez **vue d’ensemble**, puis dans la barre de commandes hello, choisissez **désactiver**. | 
   | Supprimer votre application | Choisissez **vue d’ensemble**, puis dans la barre de commandes hello, choisissez **supprimer**. Entrez le nom de votre application logique et choisissez **Supprimer**. | 

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Étapes suivantes

*  [Ajouter des conditions et exécuter des flux de travail](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Configuration d’un flux de travail à l’aide d’un modèle prédéfini pour démarrer rapidement](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Créer une application logique à l’aide d’un modèle](../logic-apps/logic-apps-arm-provision.md)
