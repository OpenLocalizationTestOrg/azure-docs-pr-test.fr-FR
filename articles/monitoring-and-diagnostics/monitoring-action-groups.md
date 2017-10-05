---
title: "Créer et gérer des groupes d’action sur le Portail Azure | Microsoft Docs"
description: "Découvrez comment créer et gérer des groupes d’action sur le Portail Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a>Créer et gérer des groupes d’actions sur le Portail Azure
## <a name="overview"></a>Vue d'ensemble ##
Cet article vous montre comment créer et gérer des groupes d’actions dans le portail Azure.

Vous pouvez configurer une liste d’actions avec des groupes d’actions. Ces groupes peuvent alors servir pour définir des alertes du journal d’activité. Ils peuvent être réutilisés par chaque alerte du journal d’activité que vous avez définie, afin que les mêmes actions soient entreprises chaque fois que l’alerte du journal d’activité est déclenchée.

Un groupe d’actions peut contenir jusqu’à 10 actions de chaque type. Chaque action se compose des propriétés suivantes :

* **Nom** : identificateur unique au sein du groupe d’actions.  
* **Type d’action** : envoyer un SMS, envoyer un e-mail ou appeler un Webhook.  
* **Détails** : numéro de téléphone, adresse e-mail ou URI de Webhook correspondant.

Pour plus d’informations sur l’utilisation de modèles Azure Resource Manager pour configurer des groupes d’actions, consultez la page [Modèles Resource Manager de groupes d’actions](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-the-azure-portal"></a>Créer un groupe d’actions à l’aide du Portail Azure ##
1. Sur le [Portail](https://portal.azure.com), sélectionnez **Moniteur**. Le panneau **Moniteur** consolide tous vos paramètres et données de monitorage sur un même affichage.

    ![Le service « Moniteur »](./media/monitoring-action-groups/home-monitor.png)
2. Dans la section **Journal d’activité**, sélectionnez **Groupes d’actions**.

    ![L’onglet « Groupes d’actions »](./media/monitoring-action-groups/action-groups-blade.png)
3. Sélectionnez **Ajouter un groupe d’actions** et renseignez les champs.

    ![La commande « Ajouter un groupe d’actions »](./media/monitoring-action-groups/add-action-group.png)
4. Entrez un nom dans la zone **Nom du groupe d’actions** et un autre dans la zone **Nom court**. Le nom court est utilisé à la place du nom complet du groupe d’actions lorsque les notifications sont envoyées à l’aide de ce groupe.

      ![La boîte de dialogue « Ajouter un groupe d’actions »](./media/monitoring-action-groups/action-group-define.png)

5. La zone **Abonnement** est automatiquement renseignée avec votre abonnement actuel. Cet abonnement est celui dans lequel est enregistré le groupe d’actions.

6. Sélectionnez le **Groupe de ressources** dans lequel le groupe d’actions est enregistré.

7. Définissez une liste d’actions en indiquant les éléments suivants pour chaque action :

    a. **Nom** : entrez un identificateur unique pour cette action.

    b. **Type d’action** : sélectionnez SMS, e-mail ou webhook.

    c. **Détails** : selon le type d’action, entrez un numéro de téléphone, une adresse e-mail ou une URI de Webhook.

8. Sélectionnez **OK** pour créer le groupe d’actions.

## <a name="manage-your-action-groups"></a>Gérer des groupes d’actions ##
Après sa création, un groupe d’actions apparaît dans la section **Groupes d’actions** du panneau **Moniteur**. Sélectionnez le groupe d’actions que vous souhaitez gérer pour :

* Ajouter, modifier ou supprimer des actions.
* Supprimer le groupe d’actions.

## <a name="next-steps"></a>Étapes suivantes ##
* En savoir plus sur le [comportement des alertes SMS](monitoring-sms-alert-behavior.md).  
* [Comprendre le schéma Webhook des alertes du journal d’activité](monitoring-activity-log-alerts-webhook.md).  
* En savoir plus sur la [limitation de la fréquence](monitoring-alerts-rate-limiting.md) des alertes. 
* Obtenir une [vue d’ensemble des alertes du journal d’activité](monitoring-overview-alerts.md) et découvrir comment recevoir des alertes.  
* Découvrir comment [configurer des alertes lorsqu’une notification d’intégrité de service est publiée](monitoring-activity-log-alerts-on-service-notifications.md).
