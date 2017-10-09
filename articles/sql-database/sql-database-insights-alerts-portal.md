---
title: "alertes de base de données SQL Azure toocreate portail aaaUse | Documents Microsoft"
description: "Utiliser les alertes de base de données SQL Azure toocreate portail hello, qui peuvent déclencher des notifications ou automation lorsque les conditions hello spécifiées sont remplies."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Utiliser les alertes de toocreate portail Azure pour la base de données SQL Azure et l’entrepôt de données

## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment tooset des alertes de base de données SQL Azure et l’entrepôt de données à l’aide de hello portail Azure. Il présente également les meilleures pratiques à adopter pour définir les périodes d’alerte.    

Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.

* **Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens. Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.    
* **Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou uniquement lorsqu’un certain nombre d’événements se produisent.

Vous pouvez configurer une alerte toodo hello de suivant lorsqu’il déclenche :

* envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs
* envoyer des e-mails tooadditional que vous spécifiez.
* appeler un webhook

Vous pouvez configurer et obtenir des informations sur les règles d’alerte avec

* [Portail Azure](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [interface de ligne de commande (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Créer une règle d’alerte sur une mesure avec hello portail Azure
1. Bonjour [portal](https://portal.azure.com/), recherchez des ressources hello vous intéressez dans l’analyse et sélectionnez-le.
2. Cette étape est différente pour SQL DS et les pools élastiques par rapport à SQL DW : 

   - **Base de données SQL et les Pools élastiques uniquement**: sélectionnez **alertes** ou **règles d’alerte** sous la section analyse de hello. icône et texte hello peuvent varier légèrement en fonction des ressources différentes.  
   
     ![Surveillance](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **Entrepôt de données SQL uniquement**: sélectionnez **analyse** sous hello section des tâches courantes. Cliquez sur hello **DWU utilisation** graphique.

     ![TÂCHES COURANTES](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Sélectionnez hello **ajouter une alerte** commande et renseignez les champs hello.
   
    ![Ajouter une alerte](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. **Nommez** votre règle d’alerte, puis choisissez une **Description** qui indique également les adresses électroniques de notification.
5. Sélectionnez hello **métrique** toomonitor de souhaité, puis choisissez un **Condition** et **seuil** valeur pour métrique de hello. Sélectionnez également l’option hello **période** de temps qui hello métrique règle doit être satisfaite avant de déclencheurs d’alerte hello. Par exemple, si vous utilisez hello point « PT5M », votre alerte recherche du processeur supérieure à 80 %, hello alerte se déclenche lorsque hello du processeur a été constamment ci-dessus 80 % pendant 5 minutes. Une fois le premier déclencheur de hello se produit, elle déclenche à nouveau lorsque hello UC reste inférieur à 80 % pendant 5 minutes. mesure du processeur de Hello se produit toutes les minutes.   
6. Vérifiez **propriétaires de messagerie...**  si vous souhaitez que les administrateurs et coadministrateurs toobe envoyé par courrier électronique lorsque hello alerte se déclenche.
7. Si vous souhaitez que les messages électroniques supplémentaires tooreceive une notification lorsque hello l’alerte se déclenche, ajoutez-les dans hello **administrateur supplémentaire email(s)** champ. Séparez les adresses e-mails par des points-virgules : *email@contoso.com;email2@contoso.com*
8. Placez dans un URI valide Bonjour **Webhook** champ si vous souhaitez qu’il est appelé lorsque hello alerte se déclenche.
9. Sélectionnez **OK** lorsque toocreate terminé hello alerte.   

Dans quelques minutes, alerte de hello est actif et déclenche comme décrit précédemment.

## <a name="managing-your-alerts"></a>Gestion de vos alertes
Une fois que vous avez créé une alerte, vous pouvez la sélectionner et :

* Permet d’afficher un graphique indiquant de seuil de métrique hello et les valeurs actuelles hello hello jour précédent.
* La modifier ou la supprimer.
* **Désactiver** ou **activer** si vous souhaitez tootemporarily arrêter ou reprenez la réception de notifications qui.


## <a name="sql-database-alert-values"></a>Valeurs d’alerte SQL Database

| Type de ressource | Nom de métrique | Nom convivial | Type d’agrégation | Fenêtre de temps minimale avant l’alerte|
| --- | --- | --- | --- | --- |
| Base de données SQL | cpu_percent | Pourcentage UC | Moyenne | 5 minutes |
| Base de données SQL | physical_data_read_percent | Pourcentage E/S des données | Moyenne | 5 minutes |
| Base de données SQL | log_write_percent | Pourcentage E/S du journal | Moyenne | 5 minutes |
| Base de données SQL | dtu_consumption_percent | Pourcentage DTU | Moyenne | 5 minutes |
| Base de données SQL | storage | Taille de base de données totale | Maximale | 30 minutes |
| Base de données SQL | connection_successful | Connexions réussies | Total | 10 minutes |
| Base de données SQL | connection_failed | Connexions ayant échoué | Total | 10 minutes |
| Base de données SQL | blocked_by_firewall | Bloqué par le pare-feu | Total | 10 minutes |
| Base de données SQL | deadlock | Blocages | Total | 10 minutes |
| Base de données SQL | storage_percent | Pourcentage de la taille de la base de données | Maximale | 30 minutes |
| Base de données SQL | xtp_storage_percent | Pourcentage de stockage OLTP en mémoire (aperçu) | Moyenne | 5 minutes |
| Base de données SQL | workers_percent | Pourcentage de travaux | Moyenne | 5 minutes |
| Base de données SQL | sessions_percent | Pourcentage sessions | Moyenne | 5 minutes |
| Base de données SQL | dtu_limit | Limite DTU | Moyenne | 5 minutes |
| Base de données SQL | dtu_used | DTU utilisé | Moyenne | 5 minutes |
||||||
| Pool élastique | cpu_percent | Pourcentage UC | Moyenne | 10 minutes |
| Pool élastique | physical_data_read_percent | Pourcentage E/S des données | Moyenne | 10 minutes |
| Pool élastique | log_write_percent | Pourcentage E/S du journal | Moyenne | 10 minutes |
| Pool élastique | dtu_consumption_percent | Pourcentage DTU | Moyenne | 10 minutes |
| Pool élastique | storage_percent | Pourcentage de stockage | Moyenne | 10 minutes |
| Pool élastique | workers_percent | Pourcentage de travaux | Moyenne | 10 minutes |
| Pool élastique | eDTU_limit | Limite eDTU | Moyenne | 10 minutes |
| Pool élastique | storage_limit | Limite de stockage | Moyenne | 10 minutes |
| Pool élastique | eDTU_used | eDTU utilisé | Moyenne | 10 minutes |
| Pool élastique | storage_used | Stockage utilisé | Moyenne | 10 minutes |
||||||               
| Entrepôt de données SQL | cpu_percent | Pourcentage UC | Moyenne | 10 minutes |
| Entrepôt de données SQL | physical_data_read_percent | Pourcentage E/S des données | Moyenne | 10 minutes |
| Entrepôt de données SQL | storage | Taille de base de données totale | Maximale | 10 minutes |
| Entrepôt de données SQL | connection_successful | Connexions réussies | Total | 10 minutes |
| Entrepôt de données SQL | connection_failed | Connexions ayant échoué | Total | 10 minutes |
| Entrepôt de données SQL | blocked_by_firewall | Bloqué par le pare-feu | Total | 10 minutes |
| Entrepôt de données SQL | service_level_objective | Objectif de niveau de service de base de données hello | Total | 10 minutes |
| Entrepôt de données SQL | dwu_limit | limite dwu | Maximale | 10 minutes |
| Entrepôt de données SQL | dwu_consumption_percent | Pourcentage DWU | Moyenne | 10 minutes |
| Entrepôt de données SQL | dwu_used | DWU utilisé | Moyenne | 10 minutes |
||||||


## <a name="next-steps"></a>Étapes suivantes
* [Obtenir une vue d’ensemble de la surveillance Azure](../monitoring-and-diagnostics/monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.
* Découvrez plus en détail la [configuration des webhooks dans les alertes](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Consultez une [vue d’ensemble des journaux de diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) et collecter des métriques détaillées à fréquence élevée sur votre service.
* Obtenir un [vue d’ensemble de la collecte de métriques](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
