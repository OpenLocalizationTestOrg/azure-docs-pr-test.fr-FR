---
title: "aaaCreate et gérer des groupes d’actions Bonjour portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate et gérer des groupes d’actions Bonjour portail Azure."
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
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="31ff5-103">Créer et gérer des groupes d’actions Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="31ff5-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="31ff5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="31ff5-104">Overview</span></span> ##
<span data-ttu-id="31ff5-105">Cet article vous montre comment toocreate et gérer des groupes d’actions Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="31ff5-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="31ff5-106">Vous pouvez configurer une liste d’actions avec des groupes d’actions.</span><span class="sxs-lookup"><span data-stu-id="31ff5-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="31ff5-107">Ces groupes peuvent alors servir pour définir des alertes du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="31ff5-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="31ff5-108">Ces groupes peuvent ensuite être réutilisées par chaque alerte de journal d’activité que vous définissez, vous être assuré que hello même action chaque déclenchement de l’alerte de journal d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="31ff5-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="31ff5-109">Un groupe d’actions peut avoir au plus too10 de chaque type d’action.</span><span class="sxs-lookup"><span data-stu-id="31ff5-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="31ff5-110">Chaque action est constituée de hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="31ff5-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="31ff5-111">**Nom**: un identificateur unique au sein du groupe d’actions hello.</span><span class="sxs-lookup"><span data-stu-id="31ff5-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="31ff5-112">**Type d’action** : envoyer un SMS, envoyer un e-mail ou appeler un Webhook.</span><span class="sxs-lookup"><span data-stu-id="31ff5-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="31ff5-113">**Détails**: hello webhook URI, adresse de messagerie ou numéro de téléphone correspondant.</span><span class="sxs-lookup"><span data-stu-id="31ff5-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="31ff5-114">Pour plus d’informations sur la façon de toouse groupes d’actions modèles tooconfigure Azure Resource Manager, consultez [modèles de gestionnaire de ressources du groupe Action](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="31ff5-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="31ff5-115">Créer un groupe d’actions à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="31ff5-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="31ff5-116">Bonjour [portal](https://portal.azure.com), sélectionnez **analyse**.</span><span class="sxs-lookup"><span data-stu-id="31ff5-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="31ff5-117">Hello **moniteur** panneau consolide toutes vos paramètres de surveillance et données dans une vue.</span><span class="sxs-lookup"><span data-stu-id="31ff5-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Hello service de « Analyse »](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="31ff5-119">Bonjour **le journal d’activité** section, sélectionnez **groupes d’actions**.</span><span class="sxs-lookup"><span data-stu-id="31ff5-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![onglet de « Groupes d’actions » Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="31ff5-121">Sélectionnez **ajouter un groupe action**et renseignez les champs hello.</span><span class="sxs-lookup"><span data-stu-id="31ff5-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Hello « Ajouter un groupe d’actions » une commande](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="31ff5-123">Entrez un nom dans hello **nom d’Action groupe** zone et entrez un nom dans hello **nom court** boîte.</span><span class="sxs-lookup"><span data-stu-id="31ff5-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="31ff5-124">nom court de Hello est utilisé à la place d’un nom de groupe complet de l’action lorsque les notifications sont envoyées à l’aide de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="31ff5-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![boîte de dialogue groupe d’actions Hello ajouter »](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="31ff5-126">Hello **abonnement** zone autofills avec votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="31ff5-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="31ff5-127">Cet abonnement est hello un dans le groupe d’actions hello est enregistré.</span><span class="sxs-lookup"><span data-stu-id="31ff5-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="31ff5-128">Sélectionnez hello **groupe de ressources** dans l’action hello groupe est enregistré.</span><span class="sxs-lookup"><span data-stu-id="31ff5-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="31ff5-129">Définissez une liste d’actions en indiquant les éléments suivants pour chaque action :</span><span class="sxs-lookup"><span data-stu-id="31ff5-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="31ff5-130">a.</span><span class="sxs-lookup"><span data-stu-id="31ff5-130">a.</span></span> <span data-ttu-id="31ff5-131">**Nom** : entrez un identificateur unique pour cette action.</span><span class="sxs-lookup"><span data-stu-id="31ff5-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="31ff5-132">b.</span><span class="sxs-lookup"><span data-stu-id="31ff5-132">b.</span></span> <span data-ttu-id="31ff5-133">**Type d’action** : sélectionnez SMS, e-mail ou webhook.</span><span class="sxs-lookup"><span data-stu-id="31ff5-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="31ff5-134">c.</span><span class="sxs-lookup"><span data-stu-id="31ff5-134">c.</span></span> <span data-ttu-id="31ff5-135">**Détails**: selon le type d’action hello, entrez un numéro de téléphone, une adresse de messagerie ou un webhook URI.</span><span class="sxs-lookup"><span data-stu-id="31ff5-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="31ff5-136">Sélectionnez **OK** groupe d’actions toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="31ff5-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="31ff5-137">Gérer des groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="31ff5-137">Manage your action groups</span></span> ##
<span data-ttu-id="31ff5-138">Après avoir créé un groupe d’actions, il est visible dans hello **groupes d’actions** section Hello **moniteur** panneau.</span><span class="sxs-lookup"><span data-stu-id="31ff5-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="31ff5-139">Sélectionnez hello action groupe toomanage à :</span><span class="sxs-lookup"><span data-stu-id="31ff5-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="31ff5-140">Ajouter, modifier ou supprimer des actions.</span><span class="sxs-lookup"><span data-stu-id="31ff5-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="31ff5-141">Supprimer le groupe d’actions hello.</span><span class="sxs-lookup"><span data-stu-id="31ff5-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31ff5-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31ff5-142">Next steps</span></span> ##
* <span data-ttu-id="31ff5-143">En savoir plus sur le [comportement des alertes SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="31ff5-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="31ff5-144">Obtenir un [compréhension de schéma webhook alerte des journaux d’activité hello](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="31ff5-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="31ff5-145">En savoir plus sur la [limitation de la fréquence](monitoring-alerts-rate-limiting.md) des alertes.</span><span class="sxs-lookup"><span data-stu-id="31ff5-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="31ff5-146">Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md)et découvrez comment tooreceive alertes.</span><span class="sxs-lookup"><span data-stu-id="31ff5-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="31ff5-147">Découvrez comment trop[configurer des alertes lors de la validation d’une notification de contrôle d’intégrité du service](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="31ff5-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
