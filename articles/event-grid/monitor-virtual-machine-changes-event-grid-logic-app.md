---
title: "modifications de machine virtuelle aaaMonitor - grille d’événement Azure & Logic Apps | Documents Microsoft"
description: "Vérifier les modifications de configuration dans des machines virtuelles (VM) à l’aide d’Azure Event Grid et Azure Logic Apps"
keywords: "applications logiques, grilles d’événements, machine virtuelle, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Surveiller les modifications d’une machine virtuelle avec Azure Event Grid et Azure Logic Apps

Vous pouvez démarrer un [flux de travail d’application logique](../logic-apps/logic-apps-what-are-logic-apps.md) automatisé lorsque des événements spécifiques se produisent dans des ressources Azure ou tierces. Ces ressources peuvent publier ces tooan événements [grille d’événement Azure](../event-grid/overview.md). À son tour, grille d’événement hello transmet ces toosubscribers les événements qui ont des files d’attente, webhooks, ou [concentrateurs d’événements](../event-hubs/event-hubs-what-is-event-hubs.md) comme points de terminaison. En tant qu’abonné, votre application logique peut attendre les événements à partir de la grille d’événement hello avant d’exécuter des flux de travail automatisés tooperform tâches - sans vous écrire de code.

Par exemple, Voici certains événements que toosubscribers via le service de grille d’événement Azure hello peuvent envoyer des serveurs de publication :

* Créer, lire, mettre à jour ou supprimer une ressource. Par exemple, vous pouvez surveiller les modifications susceptibles d’être facturées sur votre abonnement Azure. 
* Ajouter ou retirer une personne d’un abonnement Azure.
* Votre application effectue une action particulière.
* Un nouveau message apparaît dans une file d’attente.

Ce didacticiel crée une application de logique qui surveille les modifications tooa virtual machine et envoie des messages électroniques sur ces modifications. Lorsque vous créez une application logique avec un abonnement aux événements pour une ressource Azure, les événements de flux à partir de cette ressource via une application de logique toohello événement grille. didacticiel de Hello vous guide tout au long de la création de cette application logique :

![Vue d’ensemble - surveiller une machine virtuelle avec une grille d’événements et une application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * créer une application logique qui surveille les événements d’une grille d’événements ;
> * ajouter une condition qui recherche spécifiquement les modifications apportées à la machine virtuelle ;
> * envoyer un e-mail en cas de modification de la machine virtuelle.

## <a name="prerequisites"></a>Composants requis

* Un compte de messagerie sur [n’importe quel fournisseur de messagerie pris en charge par Azure Logic Apps](../connectors/apis-list.md), par exemple Outlook Office 365, Outlook.com ou Gmail, pour envoyer les notifications. Ce didacticiel utilise Outlook Office 365.

* Une [machine virtuelle](https://azure.microsoft.com/services/virtual-machines). Si ce n’est pas déjà fait, créez une machine virtuelle en suivant le [didacticiel Créer une machine virtuelle](https://docs.microsoft.com/azure/virtual-machines/). machine virtuelle de hello toomake publier des événements, vous [n’avez pas besoin de toodo n’importe quel autre](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Créer une application logique qui surveille les événements d’une grille d’événements

Tout d’abord, créez une application de la logique et ajout d’un déclencheur de grille d’événement qui surveille le groupe de ressources hello pour votre machine virtuelle. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com). 

2. Hello coin supérieur gauche du menu Azure principal de hello, choisissez **nouveau** > **intégration** > **application logique**.

   ![Créer une application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Créer votre application logique avec les paramètres de hello spécifiés dans hello tableau suivant :

   ![Spécifier les détails de l’application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Paramètre | Valeur suggérée | Description | 
   | ------- | --------------- | ----------- | 
   | **Name** | *{nom-de-votre-application-logique}* | Donnez un nom unique à l’application logique. | 
   | **Abonnement** | *{votre-abonnement-Azure}* | Sélectionnez hello même abonnement Azure pour tous les services dans ce didacticiel. | 
   | **Groupe de ressources** | *{votre-groupe-de-ressources-Azure}* | Sélectionnez hello même groupe de ressources Azure pour tous les services dans ce didacticiel. | 
   | **Emplacement** | *{votre-région-Azure}* | Sélectionnez hello même région pour tous les services dans ce didacticiel. | 
   | | | 

4. Lorsque vous êtes prêt, sélectionnez **code confidentiel toodashboard**, puis choisissez **créer**.

   Vous venez de créer une ressource Azure pour votre application logique. 
   Une fois Azure déploie votre application logique, hello logique de concepteur d’applications affiche modèles pour les modèles courants commencer plus rapidement.

   > [!NOTE] 
   > Lorsque vous sélectionnez **toodashboard du code confidentiel**, votre application logique s’ouvre automatiquement dans le Concepteur d’applications logique. Sinon, vous pouvez manuellement rechercher et ouvrir votre application logique.

5. Déployez maintenant un modèle d’application logique. Sous **Modèles**, choisissez **Application logique vide**, afin de développer votre application logique à partir de zéro.

   ![Choisir le modèle d’application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   Hello logique applications concepteur affiche maintenant vous [ *connecteurs* ](../connectors/apis-list.md) et [ *déclencheurs* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) que vous pouvez utiliser toostart votre application logique et également les actions Vous pouvez ajouter après un tooperform déclencher les tâches. Un déclencheur est un événement qui crée une instance d’application logique et démarre le flux de l’application logique. 
   Votre application logique a besoin d’un déclencheur en tant que premier élément de hello.

6. Dans la zone de recherche de hello, entrez « grille de l’événement » comme filtre. Sélectionner le déclencheur : **Azure Event Grid - On a resource event**

   ![Sélectionner le déclencheur : « Azure Event Grid - On a resource event »](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. Lorsque vous y êtes invité, connectez-vous tooAzure grille d’événement avec vos informations d’identification Azure.

   ![Se connecter avec des informations d’identification Azure](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Si vous êtes connecté avec un compte Microsoft personnel, tel que @outlook.com ou @hotmail.com, déclencheur de grille d’événement hello peuvent ne pas apparaît correctement. Pour résoudre ce problème, choisissez [connexion avec Principal du Service](/azure-resource-manager/resource-group-create-service-principal-portal.md), ou de s’authentifier en tant que membre de hello Azure Active Directory qui est associé à votre abonnement Azure, par exemple, *nom d’utilisateur* @emailoutlook.onmicrosoft.com.

8. Maintenant vous abonner les événements de toopublisher de votre application logique. Fournissent des détails de hello pour votre abonnement d’événement comme spécifié dans hello tableau suivant :

   ![Spécifier les détails de l’abonnement aux événements](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Paramètre | Valeur suggérée | Description | 
   | ------- | --------------- | ----------- | 
   | **Abonnement** | *{abonnement-Azure-de-la-machine-virtuelle}* | Sélectionnez un abonnement Azure de hello événements du serveur de publication. Pour ce didacticiel, sélectionnez hello abonnement Azure pour votre machine virtuelle. | 
   | **Type de ressource** | Microsoft.Resources.resourceGroups | Sélectionnez le type de ressource hello événements du serveur de publication. Pour ce didacticiel, sélectionnez hello la valeur spécifiée pour votre application logique surveille uniquement les groupes de ressources. | 
   | **Nom de la ressource** | *{nom-du-groupe-de-ressources-de-la-machine-virtuelle}* | Sélectionnez le nom de la ressource du serveur de publication hello. Pour ce didacticiel, sélectionnez le nom hello hello du groupe de ressources pour votre machine virtuelle. | 
   | Pour les paramètres facultatifs, choisissez **Afficher les options avancées**. | *{voir les descriptions}* | * **Filtre de préfixe** : pour ce didacticiel, laissez ce paramètre vide. comportement par défaut de Hello correspond à toutes les valeurs. Vous pouvez cependant spécifier une chaîne de préfixe en tant que filtre, par exemple, un chemin d’accès et un paramètre pour une ressource spécifique. <p>* **Filtre de suffixe** : pour ce didacticiel, laissez ce paramètre vide. comportement par défaut de Hello correspond à toutes les valeurs. Vous pouvez cependant spécifier une chaîne de suffixe en tant que filtre, par exemple, une extension de nom de fichier, si vous ne souhaitez utiliser que des types de fichiers spécifiques.<p>* **Nom de l’abonnement** : indiquez un nom unique pour votre abonnement aux événements. |
   | | | 

   Une fois que vous avez terminé, votre déclencheur Event Grid peut se présenter ainsi :
   
   ![Détails d’un exemple de déclencheur de grille d’événements](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Enregistrez votre application logique. Dans la barre d’outils Concepteur hello, choisissez **enregistrer**. toocollapse et masquer les détails d’une action dans votre logique d’application, choisissez barre de titre de l’action hello.

   ![Enregistrer votre application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Lorsque vous enregistrez votre application logique avec un déclencheur de grille d’événement, Azure crée automatiquement un abonnement aux événements pour votre ressource de tooyour sélectionné d’application logique. Par conséquent, lorsque les ressources hello publie une grille d’événement événements toohello, cette grille d’événement transmet automatiquement hello événement tooyour logique application. Cet événement déclenche votre application logique, puis crée et exécute une instance de flux de travail hello que vous définissez dans les étapes suivantes.

Votre application logique est désormais en ligne et écoute tooevents à partir de la grille d’événement hello, mais n’a aucun effet sauf si vous ajoutez des flux de travail toohello actions. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Ajouter une condition qui recherche les modifications apportées à la machine virtuelle

toorun votre workflow d’application logique uniquement quand un événement spécifique se produit, ajoutez une condition qui vérifie pour la machine virtuelle « opérations d’écriture ». Lorsque cette condition est true, votre application logique envoie à qu'envoyer par courrier électronique avec des détails sur l’ordinateur virtuel de hello mis à jour.

1. Dans le Concepteur d’application logique, avec un déclencheur d’événements grille hello, choisissez **nouvelle étape** > **ajouter une condition**.

   ![Ajouter une application de la logique de condition tooyour](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Concepteur d’application logique de Hello ajoute une condition vide tooyour du flux de travail, y compris toofollow de chemins d’accès d’action selon si la condition de hello est true ou false.

   ![Condition vide](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. Bonjour **Condition** , choisissez **modifier en mode avancé**.
Entrez cette expression :

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   Votre condition ressemble maintenant à cet exemple :

   ![Condition vide](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   Cette expression vérifie les événements hello `body` pour un `data` objet où hello `operationName` propriété est hello `Microsoft.Compute/virtualMachines/write` opération. 
   En savoir plus sur le [schéma d’un événement Event Grid](../event-grid/event-schema.md).

3. tooprovide une description de la condition de hello, choisissez hello **ellipses** (**...** ) sur la forme de condition hello bouton, puis choisissez **renommer**.

   > [!NOTE] 
   > Hello exemples plus loin dans ce didacticiel également fournissent une description des étapes de flux de travail application hello logique.

4. Choisissez maintenant **modifier en mode de base** afin que l’expression de hello résout automatiquement comme indiqué :

   ![Condition d’application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Enregistrez votre application logique.

## <a name="send-email-when-your-virtual-machine-changes"></a>Envoyer un courrier électronique lorsque votre machine virtuelle change

Ajoutez maintenant un [ *action* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) afin que vous obtenez un message électronique lorsque hello spécifié la condition a la valeur true.

1. Dans la condition de hello **Si true** , choisissez **ajouter une action**.

   ![Ajouter une action lorsque la condition est true](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. Dans la zone de recherche de hello, entrez « email » comme filtre. Selon votre fournisseur de messagerie, recherchez et sélectionnez le connecteur correspondant de hello. Sélectionnez hello « envoyer le message électronique » action de votre connecteur. Par exemple : 

   * Pour Azure compte professionnel ou scolaire, sélectionnez hello Office 365 Outlook connector. 
   * Pour les comptes Microsoft personnels, sélectionnez le connecteur du Outlook.com hello. 
   * Pour les comptes Gmail, sélectionnez le connecteur du Gmail hello. 

   Nous allons toocontinue hello Office 365 Outlook Connector. 
   Si vous utilisez un autre fournisseur, hello étapes restent hello identiques, mais votre interface utilisateur peut apparaître différent. 

   ![Sélectionner l’action « Envoyer un courrier électronique »](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. Si vous ne disposez pas d’une connexion pour votre fournisseur de messagerie, compte de connexion tooyour par courrier électronique lorsque vous êtes invité pour l’authentification.

4. Fournissent des détails pour la messagerie hello comme spécifié dans hello tableau suivant :

   ![Action E-mail vide](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > tooselect à partir des champs disponibles dans votre flux de travail, cliquez dans une zone d’édition ainsi que hello **contenu dynamique** liste s’ouvre, ou choisissez **ajouter du contenu dynamique**. Pour davantage de champs, choisissez **plus** pour chaque section dans la liste de hello. tooclose hello **contenu dynamique** , choisissez **ajouter du contenu dynamique**.

   | Paramètre | Valeur suggérée | Description | 
   | ------- | --------------- | ----------- | 
   | **To** | *{adresse-e-mail-du-destinataire}* |Entrez l’adresse de messagerie du destinataire hello. À des fins de test, vous pouvez utiliser votre propre adresse e-mail. | 
   | **Objet** | Mise à jour de la ressource : **Subject**| Entrez le contenu hello pour l’objet de le du e-mail de hello. Pour ce didacticiel, entrez hello suggéré texte et l’événement hello sélectionnez **sujet** champ. Ici, l’objet du message électronique comprend nom hello pour la ressource de hello mis à jour (machine virtuelle). | 
   | **Corps** | Groupe de ressources : **Topic** <p>Type d’événement : **Event Type**<p>ID d’événement : **ID**<p>Heure : **Event Time** | Entrer du contenu de hello pour les corps de messagerie hello. Pour ce didacticiel, entrez hello suggéré texte et l’événement hello sélectionnez **rubrique**, **Type d’événement**, **ID**, et **heure de l’événement** champs afin que votre adresse de messagerie inclut le nom de groupe de ressources hello, type d’événement, événement timestamp et l’ID d’événement de mise à jour hello. <p>tooadd des lignes vides dans votre contenu, appuyez sur MAJ + ENTRÉE. | 
   | | | 

   > [!NOTE] 
   > Si vous sélectionnez un champ qui représente un tableau, hello concepteur ajoute automatiquement une **pour chaque** boucle autour d’action hello qui fait référence à hello tableau. De cette façon, votre application logique effectue cette action sur chaque élément du tableau.

   Votre action d’e-mail peut maintenant se présenter ainsi :

   ![Sélectionnez les sorties tooinclude par courrier électronique](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   Et votre application logique terminée peut se présenter ainsi :

   ![Application logique terminée](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Enregistrez votre application logique. toocollapse et masquer les détails de chaque action dans votre logique d’application, choisissez barre de titre de l’action hello.

   ![Enregistrer votre application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   Votre application logique est désormais en ligne, mais il attend pour l’ordinateur virtuel de tooyour modifications avant de faire quoi que ce soit. 
   tootest votre application logique se poursuivre maintenant, toohello la prochaine section.

## <a name="test-your-logic-app-workflow"></a>Tester le flux de travail d’une application logique

1. toocheck que votre application logique est mise en route hello des événements spécifiés, mettez à jour de votre machine virtuelle. 

   Par exemple, vous pouvez redimensionner votre machine virtuelle dans hello portail Azure ou [redimensionner votre machine virtuelle avec Azure PowerShell](../virtual-machines/windows/resize-vm.md). 

   Après quelques instants, vous devriez recevoir un courrier électronique. Par exemple :

   ![Courrier électronique à propos de la mise à jour de la machine virtuelle](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. tooreview hello s’exécute et l’historique de déclencheur pour votre application logique, dans le menu Application logique, choisissez **vue d’ensemble**. tooview plus de détails sur l’exécution, choisissez les lignes hello pour cette exécution.

   ![Historique d’exécutions de l’application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. entrées de hello tooview et des sorties pour chaque étape, développez étape hello que vous souhaitez tooreview. Ces informations peuvent vous aider à diagnostiquer et déboguer les problèmes de votre application logique.
 
   ![Détails de l’historique des exécutions d’une application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Félicitations, vous avez créé et exécuté une application logique qui surveille les événements liés aux ressources grâce à une grille d’événements et vous envoie un e-mail lorsque ces événements se produisent. Vous avez également appris comment créer facilement des flux de travaux qui automatisent les processus et intégrer des systèmes et des services cloud.

## <a name="clean-up-resources"></a>Supprimer des ressources

Ce didacticiel utilise des ressources et effectue des actions qui peuvent entraîner des frais sur votre abonnement Azure. Par conséquent, lorsque vous avez terminé avec le didacticiel de hello et de test, assurez-vous de désactiver ou de supprimer les ressources où vous souhaitez éviter les frais tooincur.

Vous pouvez arrêter votre application logique en cours d’exécution et l’envoi de courrier électronique sans supprimer l’application hello. Dans le menu de votre application logique, **Vue d’ensemble**. Dans la barre d’outils de hello, choisissez **désactiver**.

![Désactiver votre application logique](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>Forum Aux Questions

**Q** : quelles autres tâches de surveillance de machine virtuelle puis-je effectuer avec des grilles d’événements et des applications logiques ? </br>
**R** : vous pouvez surveiller d’autres modifications de configuration, par exemple :

* Une machine virtuelle se voit attribuer des droits de contrôle d’accès en fonction du rôle (RBAC).
* Modifications tooa groupe de sécurité réseau (NSG) sur une interface réseau (NIC).
* Des disques d’une machine virtuelle ont été ajoutés ou supprimés.
* Une adresse IP publique est affectée tooa carte réseau de machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble d’Event Grid](../event-grid/overview.md)
* [Concepts d’Event Grid](../event-grid/concepts.md)
* [Démarrage rapide : Créer et acheminer des événements personnalisés avec Event Grid](../event-grid/custom-event-quickstart.md)
* [Schéma d’événement Event Grid](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Créer des workflows d’application logique avec des modèles prédéfinis](../logic-apps/logic-apps-use-logic-app-templates.md)