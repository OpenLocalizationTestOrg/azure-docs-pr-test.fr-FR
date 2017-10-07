---
title: aaaCreate des alertes pour les services Azure - portail Azure | Documents Microsoft
description: "Déclencher des messages électroniques, les notifications, les URL de sites Web d’appel (webhooks) ou automation lorsque les conditions hello spécifiées sont remplies."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Créer des alertes dans Azure Monitor pour les services Azure - Portail Azure
> [!div class="op_single_selector"]
> * [Portail](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment tooset des alertes de métrique Azure à l’aide de hello portail Azure.   

Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.

* **Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens. Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.    
* **Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit. toolearn plus d’informations sur les alertes de journal d’activité [cliquez ici](monitoring-activity-log-alerts.md)

Vous pouvez configurer un hello métrique toodo alerte suivant lorsqu’il déclenche :

* envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs
* envoyer des e-mails tooadditional que vous spécifiez.
* appeler un webhook
* Démarrer l’exécution d’un runbook Azure (uniquement à partir de hello portail Azure)

Vous pouvez configurer et obtenir des informations sur les règles d’alerte de métrique via

* [Portail Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interface de ligne de commande (CLI)](insights-alerts-command-line-interface.md)
* [API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Créer une règle d’alerte sur une mesure avec hello portail Azure
1. Bonjour [portal](https://portal.azure.com/), recherchez des ressources hello vous intéressez dans l’analyse et sélectionnez-le.

2. Sélectionnez **alertes** ou **règles d’alerte** sous la section analyse de hello. icône et texte hello peuvent varier légèrement en fonction des ressources différentes.  

    ![Surveillance](./media/insights-alerts-portal/AlertRulesButton.png)

3. Sélectionnez hello **ajouter une alerte** commande et renseignez les champs hello.

    ![Ajouter une alerte](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. **Nommez** votre règle d’alerte, puis choisissez une **Description** qui indique également les adresses électroniques de notification.

5. Sélectionnez hello **métrique** toomonitor de souhaité, puis choisissez un **Condition** et **seuil** valeur pour métrique de hello. Sélectionnez également l’option hello **période** de temps qui hello métrique règle doit être satisfaite avant de déclencheurs d’alerte hello. Par exemple, si vous utilisez hello point « PT5M », votre alerte recherche du processeur supérieure à 80 %, hello alerte se déclenche lorsque hello du processeur a été constamment ci-dessus 80 % pendant 5 minutes. Une fois le premier déclencheur de hello se produit, elle déclenche à nouveau lorsque hello UC reste inférieur à 80 % pendant 5 minutes. mesure du processeur de Hello se produit toutes les minutes.   

6. Vérifiez **propriétaires de messagerie...**  si vous souhaitez que les administrateurs et coadministrateurs toobe envoyé par courrier électronique lorsque hello alerte se déclenche.

7. Si vous souhaitez que les messages électroniques supplémentaires tooreceive une notification lorsque hello l’alerte se déclenche, ajoutez-les dans hello **administrateur supplémentaire email(s)** champ. Séparez les adresses e-mails par des points-virgules : *email@contoso.com;email2@contoso.com*

8. Placez dans un URI valide Bonjour **Webhook** champ si vous souhaitez qu’il est appelé lorsque hello alerte se déclenche.

9. Si vous utilisez Azure Automation, vous pouvez sélectionner un toobe Runbook exécuter lors du déclenche de l’alerte de hello.

10. Sélectionnez **OK** lorsque toocreate terminé hello alerte.   

Dans quelques minutes, alerte de hello est actif et déclenche comme décrit précédemment.

## <a name="managing-your-alerts"></a>Gestion de vos alertes
Une fois que vous avez créé une alerte, vous pouvez la sélectionner et :

* Permet d’afficher un graphique indiquant de seuil de métrique hello et les valeurs actuelles hello hello jour précédent.
* La modifier ou la supprimer.
* **Désactiver** ou **activer** si vous souhaitez tootemporarily arrêter ou reprenez la réception de notifications qui.

## <a name="next-steps"></a>Étapes suivantes
* [Obtenir une vue d’ensemble de la surveillance Azure](monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.
* Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).
* Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).
* Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).
* Consultez une [vue d’ensemble des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) et collecter des métriques détaillées à fréquence élevée sur votre service.
* Obtenir un [vue d’ensemble de la collecte de métriques](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
