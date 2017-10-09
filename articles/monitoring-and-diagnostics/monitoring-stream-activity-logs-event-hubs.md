---
title: "tooEvent de journal des activités Azure hello aaaStream Hubs | Documents Microsoft"
description: "Découvrez comment toostream hello tooEvent du journal des activités Azure concentrateurs."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Flux tooEvent du journal des activités Azure hello concentrateurs
Hello [ **journal des activités Azure** ](monitoring-overview-activity-logs.md) peut être transmis en continu côté application tooany en temps réel à l’aide de l’option des « Exportation » hello intégrée dans le portail de hello, ou en activant hello Id de règle de Bus de Service dans un profil de journal via hello CLI des applets de commande PowerShell Azure ou Azure.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Ce que vous pouvez faire avec hello journal d’activité et les concentrateurs d’événements
Voici quelques méthodes, vous pouvez utiliser hello de diffusion en continu de la fonctionnalité de hello journal d’activité :

* **Flux des systèmes de journalisation et les données de télémétrie toothird tiers** – au fil du temps, le concentrateurs d’événements de diffusion en continu deviennent hello mécanisme toopipe votre journal des activités dans les serveurs SIEM de tiers et les solutions analytique de journal.
* **Générer une télémétrie personnalisée et la plateforme de journalisation** : Si vous disposez déjà d’une plateforme de télémétrie personnalisées ou sont simplement penser à la génération 1, hello hautement évolutive de publication / abonnement nature des concentrateurs d’événements vous permet de tooflexibly réception hello journal d’activité. [Consultez le toousing de Dan Rosanova guide concentrateurs d’événements dans une plateforme de télémétrie à l’échelle mondiale ici.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Activer la diffusion en continu de hello journal d’activité
Vous pouvez activer la diffusion en continu de hello journal d’activité par programmation ou via le portail de hello. Dans les deux cas, vous choisissez un Namespace de Bus de Service et une stratégie d’accès partagé pour cet espace de noms et un concentrateur d’événements est créé dans cet espace de noms lors de l’événement du journal d’activité de nouvelle première hello se produit. Si vous n’avez pas un Namespace de Bus de Service, vous devez d’abord toocreate une. Si vous avez précédemment transmis en continu toothis événements de journal d’activité Service Bus Namespace, hello concentrateur d’événements qui a été créé précédemment est réutilisée. stratégie d’accès partagé de Hello définit des autorisations de hello qui a du mécanisme de diffusion en continu hello. Aujourd'hui, la diffusion en continu de concentrateurs d’événements tooan requiert **gérer**, **envoyer**, et **écouter** autorisations. Vous pouvez créer ou modifier des stratégies d’accès Namespace de Bus de Service partagé dans le portail classique de hello sous l’onglet « Configurer » de hello pour votre Namespace de Bus de Service. tooupdate hello de diffusion en continu de journal d’activité journal profil tooinclude, utilisateur hello hello modification doit avoir l’autorisation de ListKey de hello sur cette règle d’autorisation du Bus de Service.

Hello service bus ou l’événement espace de noms hub n’a pas toobe Bonjour même abonnement que l’abonnement hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.

### <a name="via-azure-portal"></a>Via le portail Azure
1. Accédez toohello **le journal d’activité** panneau à l’aide du menu de hello sur hello gauche du portail de hello.
   
    ![Accédez tooActivity journal dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Cliquez sur hello **exporter** bouton en haut de hello du panneau des hello.
   
    ![Bouton Exporter dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Dans le panneau hello qui s’affiche, vous pouvez sélectionner les régions hello pour lequel vous souhaitez que les événements toostream et hello Service Bus Namespace dans lequel vous souhaitez qu’un toobe concentrateur d’événements créé pour ces événements de diffusion en continu.
   
    ![Panneau Exporter le journal d’activité](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Cliquez sur **enregistrer** toosave ces paramètres. paramètres de Hello sont alors immédiatement appliquée tooyour abonnement.

### <a name="via-powershell-cmdlets"></a>Via les applets de commande PowerShell
Si un profil du journal existe déjà, vous devez tout d’abord tooremove ce profil.

1. Utilisez `Get-AzureRmLogProfile` tooidentify si un profil du journal existe
2. Dans ce cas, utilisez `Remove-AzureRmLogProfile` tooremove il.
3. Utilisez `Set-AzureRmLogProfile` toocreate un profil :

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Hello ID de règle de Bus de Service est une chaîne au format suivant : {ID de ressource de bus de service} /authorizationrules/ {nom de la clé}, par exemple 

### <a name="via-azure-cli"></a>Via l’interface de ligne de commande Azure
Si un profil du journal existe déjà, vous devez tout d’abord tooremove ce profil.

1. Utilisez `azure insights logprofile list` tooidentify si un profil du journal existe
2. Dans ce cas, utilisez `azure insights logprofile delete` tooremove il.
3. Utilisez `azure insights logprofile add` toocreate un profil :

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Hello ID de règle de Bus de Service est une chaîne au format suivant : `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Comment consommer des données de journal hello de concentrateurs d’événements ?
[schéma Hello hello journal d’activité est disponible ici](monitoring-overview-activity-logs.md). Chaque événement est dans un tableau d’objets blob JSON appelé « enregistrements ».

## <a name="next-steps"></a>Étapes suivantes
* [Hello d’archive compte de stockage tooa de journal d’activité](monitoring-archive-activity-log.md)
* [Vue d’ensemble de lecture hello Hello journal des activités Azure](monitoring-overview-activity-logs.md)
* [Définir une alerte basée sur un événement de journal d’activité](insights-auditlog-to-webhook-email.md)

