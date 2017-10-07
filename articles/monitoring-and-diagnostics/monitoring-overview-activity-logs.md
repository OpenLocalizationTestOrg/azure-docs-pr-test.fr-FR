---
title: "aaaOverview Hello journal des activités Azure | Documents Microsoft"
description: "Découvrez quels hello est de journal des activités Azure et comment vous pouvez l’utiliser toounderstand les événements qui se produisent dans votre abonnement Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Surveiller l’activité de l’abonnement avec hello journal des activités Azure
Hello **journal des activités Azure** est un journal d’abonnement qui permet de connaître les événements au niveau de l’abonnement qui se sont produites dans Azure. Cela inclut une plage de données, à partir de tooupdates de données opérationnelles Azure Resource Manager sur les événements de contrôle d’intégrité du Service. Hello journal d’activité était précédemment appelé « Journaux d’Audit » ou « Journaux des opérations », depuis la catégorie Administrative hello signale les événements panneau pour vos abonnements. À l’aide de hello journal d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur les ressources hello dans votre abonnement d’écriture. Vous pouvez également comprendre état hello d’opération de hello et d’autres propriétés pertinentes. Hello journal d’activité n’inclut pas les opérations de lecture (GET) ou pour les ressources qui utilisent hello classique / modèle de « RDFE ».

![Journaux d’activité et autres types de journaux ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Figure 1 : Journaux d’activité et autres types de journaux

Hello journal d’activité est différente de [journaux de Diagnostic](monitoring-overview-of-diagnostic-logs.md). Journaux d’activité fournissent des données sur les opérations de hello d’une ressource à partir de hello à l’extérieur (hello « plan de contrôle »). Les journaux de diagnostic sont émis par une ressource et fournissent des informations sur l’opération hello d’une ressource (hello « plan de données »).

Vous pouvez récupérer des événements à partir de votre journal des activités à l’aide de hello portail Azure, CLI, des applets de commande PowerShell et l’API REST d’analyse Azure.


> [!WARNING]
> Hello journal des activités Azure est principalement utilisé pour les activités qui se produisent dans le Gestionnaire de ressources Azure. Elle ne suit pas les ressources à l’aide du modèle de classique/RDFE hello. Certains types de ressources Classic ont un fournisseur de ressources proxy dans Azure Resource Manager (par exemple, Microsoft.ClassicCompute). Si vous interagissez avec un type de ressource classique via Azure Resource Manager à l’aide de ces fournisseurs de ressources du serveur proxy, les opérations de hello apparaissent dans le journal d’activité de hello. Si vous interagissez avec une ressource classique de type dans le portail classique de hello ou sinon en dehors de proxy du Gestionnaire de ressources Azure hello, vos actions sont enregistrées uniquement dans le journal des opérations de hello. Hello journal des opérations est accessible uniquement dans le portail classique de hello.
>
>

Hello vue suivant hello présentation vidéo journal d’activité.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Catégories Bonjour journal d’activité
Hello journal d’activité contient plusieurs catégories de données. Pour plus d’informations sur les schémas hello de ces catégories, [, consultez cet article](monitoring-activity-log-schema.md). Vous avez notamment vu les points suivants :
* **Administration** -cette catégorie contient les enregistrement hello de tous les créer, les opérations de mise à jour, de suppression et d’action effectuée par le biais du Gestionnaire de ressources. Exemples de hello les types d’événements que vous verriez dans cette catégorie incluent « créer la machine virtuelle » et « supprimer un groupe de sécurité réseau « chaque action effectuée par un utilisateur ou l’application à l’aide du Gestionnaire de ressources est modelée comme une opération sur un type particulier. Si le type d’opération hello est écrire, supprimer, ou Action, enregistrements hello de début de hello et réussite ou Échec de cette opération sont enregistrées dans la catégorie Administrative de hello. catégorie Administrative de Hello inclut également toutes les modifications de contrôle d’accès toorole dans un abonnement.
* **L’intégrité du service** -cette catégorie contient les enregistrements hello n’importe quel contrôle d’intégrité des incidents de services qui se sont produites dans Azure. Un exemple de type hello d’événement que vous verriez dans cette catégorie est « SQL Azure dans l’est des États-Unis rencontre des temps d’arrêt. » Événements de contrôle d’intégrité de service existe cinq types : Action requise, récupération d’assistance, Incident, Maintenance, informations ou la sécurité et n’apparaissent que si vous avez une ressource dans l’abonnement hello qui est affecté par l’événement de hello.
* **Alerte** -cette catégorie contient enregistrement hello pour toutes les activations d’alertes Azure. Un exemple de type hello d’événement que vous verriez dans cette catégorie est « % du processeur sur myVM a été plus de 80 pour hello 5 dernières minutes. » Une variété de systèmes Azure possèdent un concept d’alertes : vous pouvez définir une règle quelconque et recevoir une notification lorsque les conditions correspondent à cette règle. Chaque fois qu’un type d’alerte Azure pris en charge 'active,' ou hello conditions sont rempli toogenerate une notification, un enregistrement de l’activation de hello est envoyé également catégorie toothis Hello journal d’activité.
* **Mise à l’échelle** -cette catégorie contient les enregistrements de hello de toute opération toohello connexes d’événements du moteur de mise à l’échelle hello selon les paramètres d’échelle automatique que vous avez défini dans votre abonnement. Un exemple de type hello d’événement que vous verriez dans cette catégorie est « Mise à l’échelle mise à l’échelle de l’échec de l’action. » À l’aide de la mise à l’échelle, vous pouvez automatiquement montée en puissance parallèle ou mettre à l’échelle dans hello nombre d’instances d’un type de ressource pris en charge basée sur l’heure du jour et/ou la charge des données (métriques) à l’aide d’un paramètre de mise à l’échelle. Lorsque les conditions de hello sont remplies tooscale vers le haut ou vers le bas, début de hello et événements a réussi ou a échoué sont enregistrés dans cette catégorie.
* **Recommandation** : cette catégorie contient les événements de recommandation de certains types de ressources, telles que les sites Web et les serveurs SQL. Ces événements proposent des recommandations pour l’utilisation de toobetter vos ressources. Vous ne recevez que les événements de ce type si vous disposez de ressources qui émettent des recommandations.
* **Stratégie, sécurité et état d’intégrité du service** : ces catégories ne contiennent pas d’événements ; elles sont réservées à un usage ultérieur.

## <a name="event-schema-per-category"></a>Schéma d’événements par catégorie
[Consultez ce schéma d’événement le journal d’activité de l’article toounderstand hello par catégorie.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>Ce que vous pouvez faire hello journal d’activité
Voici quelques-unes des choses hello que vous pouvez faire avec hello journal d’activité :

![Journal d’activité Azure](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Interroger et afficher dans hello **portail Azure**.
* [Créer une alerte basée sur un événement du journal d’activité](monitoring-activity-log-alerts.md)
* [Diffuser en continu tooan **concentrateur d’événements** ](monitoring-stream-activity-logs-event-hubs.md) pour l’ingestion par un service tiers ou d’une solution personnalisée analytique telles que Power BI.
* Analyser dans Power BI à l’aide de hello [ **pack de contenu Power BI**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Enregistrez-le tooa **compte de stockage** pour l’inspection d’archivage ou manuelle](monitoring-archive-activity-log.md). Vous pouvez spécifier la durée de rétention hello (en jours) à l’aide de hello **profil journal**.
* Interrogez-le via l’applet de commande PowerShell, l’interface de ligne de commande ou l’API REST.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Requête hello journal d’activité Bonjour portail Azure
Dans hello portail Azure, vous pouvez afficher le journal des activités à plusieurs endroits :
* Hello **panneau du journal d’activité**, auquel vous pouvez accéder en recherchant des hello journal d’activité sous « Plus Services » dans le volet de navigation gauche hello.
* Hello **panneau d’analyse**, qui apparaît par défaut dans le volet de navigation gauche hello. Hello journal d’activité est une section de ce panneau de moniteur de Windows Azure.
* De n’importe quelle ressource **panneau des ressources**, par exemple, le panneau de configuration hello pour un ordinateur virtuel. Hello journal d’activité est une des sections hello sur la plupart de ces panneaux de ressource et en cliquant sur elle automatiquement filtre les événements de hello toothose liés toothat des ressources spécifiques.

Bonjour portail Azure, vous pouvez filtrer votre journal des activités en fonction de ces champs :
* TimeSpan - hello début et fin du temps pour les événements.
* Catégorie - catégorie d’événement hello comme décrit ci-dessus.
* Abonnement : un ou plusieurs noms d’abonnements Azure.
* Groupe de ressources : un ou plusieurs groupes de ressources au sein de ces abonnements.
* Ressources (nom) - nom hello d’une ressource spécifique.
* Type de ressource - type hello de ressource, par exemple, Microsoft.Compute/virtualmachines.
* Nom de l’opération - nom hello d’une opération Azure Resource Manager, par exemple, Microsoft.SQL/servers/Write.
* Niveau de gravité - hello gravité de l’événement hello (message d’information, avertissement, erreur critique).
* Événements déclenchés par - hello 'appelant' ou utilisateur qui a effectué l’opération de hello.
* Recherche libre : zone de recherche textuelle libre qui permet de rechercher une chaîne dans les champs de tous les événements.

Une fois que vous avez défini un ensemble de filtres, vous pouvez l’enregistrer en tant que requête persistante entre les sessions si vous avez besoin de tooperform hello même requête avec les filtres appliqués à nouveau dans hello futures. Vous pouvez également épingler une conservation de requête tooyour tableau de bord Azure tooalways un œil sur les événements spécifiques.

Cliquez sur Appliquer pour exécuter votre requête et afficher tous les événements correspondants. Cliquez sur n’importe quel événement dans la liste hello affiche hello résumé de cet événement ainsi que hello JSON raw complète de cet événement.

Pour encore plus de puissance, vous pouvez cliquer sur hello **recherche de journal** icône, qui affiche vos données de journal d’activité Bonjour [solution de journal Analytique activité journal Analytique](../log-analytics/log-analytics-activity.md). panneau du journal d’activité Hello offre un filtre/Parcourir de base sur les journaux, mais permet d’Analytique de journal toopivot, interroger et visualiser vos données de façon plus puissante.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Exportation hello journal d’activité avec un profil de journal
Un **profil de journal** contrôle comment votre journal d’activité est exporté. À l’aide d’un profil de journal, vous pouvez configurer :

* Où hello journal d’activité doit être envoyé (compte de stockage ou les concentrateurs d’événements)
* Les catégories d’événements (Write, Delete, Action) qui doivent être envoyées. *sens de Hello de « catégorie » dans le journal des profils et les événements de journal d’activité est différent. Bonjour profil du journal, « Catégorie » représente le type d’opération hello (Action d’écriture, suppression,). Dans un événement du journal d’activité, la propriété de « catégorie » de hello représente la source de hello ou type d’événement (par exemple, Administration, ServiceHealth, alerte, etc.).*
* Les régions (emplacements) qui doivent être exportées. Assurez-vous que tooinclude « globaux », comme de nombreux événements dans le journal d’activité de hello sont des événements globaux.
* La durée pendant laquelle hello journal d’activité doit être conservé dans un compte de stockage.
    - Une durée de rétention de zéro jour signifie que les journaux sont conservés indéfiniment. Sinon, valeur de hello peut être n’importe quel nombre de jours compris entre 1 et 2147483647.
    - Si les stratégies de rétention sont définies, mais que le stockage des journaux dans un compte de stockage est désactivé (par exemple, si uniquement les options de concentrateurs d’événements ou OMS sont sélectionnées), les stratégies de rétention hello n’ont aucun effet.
    - Stratégies de rétention sont appliquées par jour, donc à hello fin d’une journée (UTC), consigne un jour hello qui est désormais au-delà de la stratégie de rétention hello sont supprimés. Par exemple, si vous aviez une stratégie de rétention d’un jour, au début de hello du jour hello aujourd'hui hello les journaux à partir de hello avant-hier seraient supprimés.

Vous pouvez utiliser un compte de stockage ou espace de noms événement hub qui n’est pas hello même abonnement comme une émission journaux hello. utilisateur de Hello qui configure hello paramètre doit avoir des abonnements tooboth d’accès appropriés RBAC hello.

Ces paramètres peuvent être configurés via l’option de « L’exportation » hello dans le panneau de journal d’activité hello dans le portail de hello. Ils peuvent également être configurés par programme [à l’aide de hello API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931927.aspx), applets de commande PowerShell ou CLI. Un abonnement ne peut avoir qu’un seul profil de journal.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Configurer des profils de journal à l’aide de hello portail Azure
Vous pouvez diffuser hello journal d’activité tooan concentrateur d’événements ou les stocker dans un compte de stockage à l’aide de l’option de « Exportation » hello Bonjour portail Azure.

1. Accédez toohello **le journal d’activité** panneau à l’aide du menu de hello sur hello gauche du portail de hello.

    ![Accédez tooActivity journal dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Cliquez sur hello **exporter** bouton en haut de hello du panneau des hello.

    ![Bouton Exporter dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Dans le panneau hello qui s’affiche, vous pouvez sélectionner :  
  * régions pour lequel vous souhaitez que les événements tooexport
  * Hello toowhich compte de stockage vous souhaitez que les événements toosave
  * nombre de Hello de jours pendant lesquels que vous souhaitez tooretain ces événements dans le stockage. Un paramètre de 0 jour conserve les journaux hello indéfiniment.
  * Hello Namespace de Bus de Service dans lequel vous souhaitez qu’un toobe concentrateur d’événements créé pour ces événements de diffusion en continu.

     ![Panneau Exporter le journal d’activité](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Cliquez sur **enregistrer** toosave ces paramètres. paramètres de Hello sont alors immédiatement appliquée tooyour abonnement.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Configurer des profils de journal à l’aide d’applets de commande PowerShell Azure de hello
#### <a name="get-existing-log-profile"></a>Obtention du profil de journal existant
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Ajout d’un profil de journal
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Propriété | Requis | Description |
| --- | --- | --- |
| Name |OUI |Nom de votre profil de journal. |
| StorageAccountId |Non |ID de ressource de hello toowhich de compte de stockage hello journal d’activité doit être enregistré. |
| serviceBusRuleId |Non |ID de règle de Bus de service pour l’espace de noms Service Bus hello vous aimeriez toohave créés dans les concentrateurs d’événements. Est une chaîne au format suivant : `{service bus resource ID}/authorizationrules/{key name}`. |
| Emplacements |Oui |Liste de séparées par des virgules des régions pour lequel vous souhaitez que les événements du journal d’activité toocollect. |
| RetentionInDays |OUI |Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647. Une valeur égale à zéro stocke les journaux hello indéfiniment (indéfiniment). |
| Catégories |Non |Liste séparée par des virgules des catégories d’événements qui doivent être collectées. Les valeurs possibles sont Write, Delete et Action. |

#### <a name="remove-a-log-profile"></a>Supprimer un profil de journal
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Configurer des profils du journal d’utilisation hello CLI d’Azure inter-plateformes
#### <a name="get-existing-log-profile"></a>Obtention du profil de journal existant
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Hello `name` propriété doit être le nom de hello de votre profil de journal.

#### <a name="add-a-log-profile"></a>Ajout d’un profil de journal
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Propriété | Requis | Description |
| --- | --- | --- |
| name |OUI |Nom de votre profil de journal. |
| storageId |Non |ID de ressource de hello toowhich de compte de stockage hello journal d’activité doit être enregistré. |
| serviceBusRuleId |Non |ID de règle de Bus de service pour l’espace de noms Service Bus hello vous aimeriez toohave créés dans les concentrateurs d’événements. Est une chaîne au format suivant : `{service bus resource ID}/authorizationrules/{key name}`. |
| emplacements |Oui |Liste de séparées par des virgules des régions pour lequel vous souhaitez que les événements du journal d’activité toocollect. |
| RetentionInDays |OUI |Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647. Une valeur égale à zéro stocke les journaux hello indéfiniment (indéfiniment). |
| Catégories |Non |Liste séparée par des virgules des catégories d’événements qui doivent être collectées. Les valeurs possibles sont Write, Delete et Action. |

#### <a name="remove-a-log-profile"></a>Supprimer un profil de journal
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello journal d’activité (anciennement les journaux d’Audit)](../azure-resource-manager/resource-group-audit.md)
* [Flux tooEvent du journal des activités Azure hello concentrateurs](monitoring-stream-activity-logs-event-hubs.md)
