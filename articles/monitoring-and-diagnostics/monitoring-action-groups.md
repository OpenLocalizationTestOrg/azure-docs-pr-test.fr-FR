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
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="ba320-103">Créer et gérer des groupes d’actions sur le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ba320-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="ba320-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ba320-104">Overview</span></span> ##
<span data-ttu-id="ba320-105">Cet article vous montre comment créer et gérer des groupes d’actions dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ba320-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="ba320-106">Vous pouvez configurer une liste d’actions avec des groupes d’actions.</span><span class="sxs-lookup"><span data-stu-id="ba320-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="ba320-107">Ces groupes peuvent alors servir pour définir des alertes du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="ba320-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="ba320-108">Ils peuvent être réutilisés par chaque alerte du journal d’activité que vous avez définie, afin que les mêmes actions soient entreprises chaque fois que l’alerte du journal d’activité est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="ba320-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="ba320-109">Un groupe d’actions peut contenir jusqu’à 10 actions de chaque type.</span><span class="sxs-lookup"><span data-stu-id="ba320-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="ba320-110">Chaque action se compose des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba320-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="ba320-111">**Nom** : identificateur unique au sein du groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="ba320-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="ba320-112">**Type d’action** : envoyer un SMS, envoyer un e-mail ou appeler un Webhook.</span><span class="sxs-lookup"><span data-stu-id="ba320-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="ba320-113">**Détails** : numéro de téléphone, adresse e-mail ou URI de Webhook correspondant.</span><span class="sxs-lookup"><span data-stu-id="ba320-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="ba320-114">Pour plus d’informations sur l’utilisation de modèles Azure Resource Manager pour configurer des groupes d’actions, consultez la page [Modèles Resource Manager de groupes d’actions](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="ba320-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="ba320-115">Créer un groupe d’actions à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ba320-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="ba320-116">Sur le [Portail](https://portal.azure.com), sélectionnez **Moniteur**.</span><span class="sxs-lookup"><span data-stu-id="ba320-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="ba320-117">Le panneau **Moniteur** consolide tous vos paramètres et données de monitorage sur un même affichage.</span><span class="sxs-lookup"><span data-stu-id="ba320-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Le service « Moniteur »](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="ba320-119">Dans la section **Journal d’activité**, sélectionnez **Groupes d’actions**.</span><span class="sxs-lookup"><span data-stu-id="ba320-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![L’onglet « Groupes d’actions »](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="ba320-121">Sélectionnez **Ajouter un groupe d’actions** et renseignez les champs.</span><span class="sxs-lookup"><span data-stu-id="ba320-121">Select **Add action group**, and fill in the fields.</span></span>

    ![La commande « Ajouter un groupe d’actions »](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="ba320-123">Entrez un nom dans la zone **Nom du groupe d’actions** et un autre dans la zone **Nom court**.</span><span class="sxs-lookup"><span data-stu-id="ba320-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="ba320-124">Le nom court est utilisé à la place du nom complet du groupe d’actions lorsque les notifications sont envoyées à l’aide de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="ba320-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![La boîte de dialogue « Ajouter un groupe d’actions »](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="ba320-126">La zone **Abonnement** est automatiquement renseignée avec votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="ba320-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="ba320-127">Cet abonnement est celui dans lequel est enregistré le groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="ba320-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="ba320-128">Sélectionnez le **Groupe de ressources** dans lequel le groupe d’actions est enregistré.</span><span class="sxs-lookup"><span data-stu-id="ba320-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="ba320-129">Définissez une liste d’actions en indiquant les éléments suivants pour chaque action :</span><span class="sxs-lookup"><span data-stu-id="ba320-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="ba320-130">a.</span><span class="sxs-lookup"><span data-stu-id="ba320-130">a.</span></span> <span data-ttu-id="ba320-131">**Nom** : entrez un identificateur unique pour cette action.</span><span class="sxs-lookup"><span data-stu-id="ba320-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="ba320-132">b.</span><span class="sxs-lookup"><span data-stu-id="ba320-132">b.</span></span> <span data-ttu-id="ba320-133">**Type d’action** : sélectionnez SMS, e-mail ou webhook.</span><span class="sxs-lookup"><span data-stu-id="ba320-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="ba320-134">c.</span><span class="sxs-lookup"><span data-stu-id="ba320-134">c.</span></span> <span data-ttu-id="ba320-135">**Détails** : selon le type d’action, entrez un numéro de téléphone, une adresse e-mail ou une URI de Webhook.</span><span class="sxs-lookup"><span data-stu-id="ba320-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="ba320-136">Sélectionnez **OK** pour créer le groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="ba320-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="ba320-137">Gérer des groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="ba320-137">Manage your action groups</span></span> ##
<span data-ttu-id="ba320-138">Après sa création, un groupe d’actions apparaît dans la section **Groupes d’actions** du panneau **Moniteur**.</span><span class="sxs-lookup"><span data-stu-id="ba320-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="ba320-139">Sélectionnez le groupe d’actions que vous souhaitez gérer pour :</span><span class="sxs-lookup"><span data-stu-id="ba320-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="ba320-140">Ajouter, modifier ou supprimer des actions.</span><span class="sxs-lookup"><span data-stu-id="ba320-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="ba320-141">Supprimer le groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="ba320-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba320-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba320-142">Next steps</span></span> ##
* <span data-ttu-id="ba320-143">En savoir plus sur le [comportement des alertes SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ba320-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="ba320-144">[Comprendre le schéma Webhook des alertes du journal d’activité](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="ba320-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="ba320-145">En savoir plus sur la [limitation de la fréquence](monitoring-alerts-rate-limiting.md) des alertes.</span><span class="sxs-lookup"><span data-stu-id="ba320-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="ba320-146">Obtenir une [vue d’ensemble des alertes du journal d’activité](monitoring-overview-alerts.md) et découvrir comment recevoir des alertes.</span><span class="sxs-lookup"><span data-stu-id="ba320-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="ba320-147">Découvrir comment [configurer des alertes lorsqu’une notification d’intégrité de service est publiée](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="ba320-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
