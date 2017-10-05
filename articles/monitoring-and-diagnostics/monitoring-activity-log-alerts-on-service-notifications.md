---
title: "Recevoir des alertes de journal d’activité sur les notifications de service | Documents Microsoft"
description: "Soyez informé par SMS, e-mail ou webhook en cas de service Azure."
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="95643-103">Créer des alertes de journal d’activité sur les notifications de service</span><span class="sxs-lookup"><span data-stu-id="95643-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="95643-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="95643-104">Overview</span></span>
<span data-ttu-id="95643-105">Cet article vous indique comment configurer des alertes de journal d’activité pour les notifications sur l’intégrité du service à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95643-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="95643-106">Vous pouvez recevoir une alerte lorsqu’Azure envoie des notifications sur l’état du service sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="95643-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="95643-107">Vous pouvez configurer l’alerte en fonction des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="95643-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="95643-108">la classe de notification sur l’intégrité du service (incident, maintenance, informations, etc.) ;</span><span class="sxs-lookup"><span data-stu-id="95643-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="95643-109">le ou les services affectés ;</span><span class="sxs-lookup"><span data-stu-id="95643-109">The service(s) affected.</span></span>
- <span data-ttu-id="95643-110">la ou les régions affectées ;</span><span class="sxs-lookup"><span data-stu-id="95643-110">The region(s) affected.</span></span>
- <span data-ttu-id="95643-111">l’état de la notification (actif ou résolu) ;</span><span class="sxs-lookup"><span data-stu-id="95643-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="95643-112">le niveau des notifications (informationnelle, avertissement, erreur).</span><span class="sxs-lookup"><span data-stu-id="95643-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="95643-113">Vous pouvez également configurer à qui l’alerte doit être envoyée :</span><span class="sxs-lookup"><span data-stu-id="95643-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="95643-114">sélectionner un groupe d’actions existant ;</span><span class="sxs-lookup"><span data-stu-id="95643-114">Select an existing action group.</span></span>
- <span data-ttu-id="95643-115">créer un nouveau groupe d’actions (qui peut être utilisé pour les alertes futures).</span><span class="sxs-lookup"><span data-stu-id="95643-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="95643-116">Pour en savoir plus sur les groupes d’actions, consultez [Créer et gérer des groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="95643-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="95643-117">Pour plus d’informations sur le mode de configuration des alertes de notification sur l’intégrité du service à l’aide de modèles Azure Resource Manager, consultez [Modèles Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="95643-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="95643-118">Créer une alerte sur une notification sur l’intégrité du service pour un nouveau groupe d’actions à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="95643-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="95643-119">Dans le [Portail](https://portal.azure.com), sélectionnez **Moniteur**.</span><span class="sxs-lookup"><span data-stu-id="95643-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Le service « Moniteur »](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="95643-121">Dans la section **Journal d’activité**, sélectionnez **Alertes**.</span><span class="sxs-lookup"><span data-stu-id="95643-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![L’onglet « Alertes »](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="95643-123">Sélectionnez **Ajouter une alerte de journal d’activité**, puis renseignez les champs.</span><span class="sxs-lookup"><span data-stu-id="95643-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![La commande « Ajouter une alerte activité journal »](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="95643-125">Entrez un nom dans la boîte **Nom de l’alerte activité journal** et fournissez une **Description**.</span><span class="sxs-lookup"><span data-stu-id="95643-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![La boîte de dialogue « Ajouter une alerte activité journal »](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="95643-127">La boîte **Abonnement** est automatiquement renseignée avec votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="95643-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="95643-128">Cet abonnement est utilisé pour enregistrer l’alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="95643-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="95643-129">La ressource d’alerte est déployée pour cet abonnement et surveille les événements du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="95643-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="95643-130">Sélectionnez le **Groupe de ressources** dans lequel la ressource d’alerte est créée.</span><span class="sxs-lookup"><span data-stu-id="95643-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="95643-131">Il ne s’agit pas du groupe de ressources surveillé par l’alerte.</span><span class="sxs-lookup"><span data-stu-id="95643-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="95643-132">Au lieu de cela, il s’agit du groupe de ressources où se trouve la ressource d’alerte.</span><span class="sxs-lookup"><span data-stu-id="95643-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="95643-133">Dans la boîte **Catégorie d’événement**, sélectionnez **Intégrité du service**.</span><span class="sxs-lookup"><span data-stu-id="95643-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="95643-134">En option, sélectionnez **Service**, **Région**, **Type**, **État** et **Niveau** des notifications sur l’intégrité du service que vous souhaitez recevoir.</span><span class="sxs-lookup"><span data-stu-id="95643-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="95643-135">Sous **Alerte via**, sélectionnez le bouton du groupe d’actions **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="95643-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="95643-136">Entrez un nom dans la boîte **Nom du groupe d’actions** et entrez un nom dans la boîte **Nom court**.</span><span class="sxs-lookup"><span data-stu-id="95643-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="95643-137">Le nom court est référencé dans les notifications envoyées lorsque cette alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="95643-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="95643-138">Définissez ensuite une liste de destinataires en indiquant les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="95643-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="95643-139">a.</span><span class="sxs-lookup"><span data-stu-id="95643-139">a.</span></span> <span data-ttu-id="95643-140">**Nom** : entrez le nom, l’alias ou l’identificateur du destinataire.</span><span class="sxs-lookup"><span data-stu-id="95643-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="95643-141">b.</span><span class="sxs-lookup"><span data-stu-id="95643-141">b.</span></span> <span data-ttu-id="95643-142">**Type d’action** : sélectionnez SMS, e-mail ou webhook.</span><span class="sxs-lookup"><span data-stu-id="95643-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="95643-143">c.</span><span class="sxs-lookup"><span data-stu-id="95643-143">c.</span></span> <span data-ttu-id="95643-144">**Détails** : selon le type d’action choisi, indiquez un numéro de téléphone, une adresse e-mail ou une URI Webhook.</span><span class="sxs-lookup"><span data-stu-id="95643-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="95643-145">Sélectionnez **OK** pour créer l’alerte.</span><span class="sxs-lookup"><span data-stu-id="95643-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="95643-146">Dans quelques minutes, l’alerte est active et commence à se déclencher en fonction des conditions que vous avez spécifiées lors de la création.</span><span class="sxs-lookup"><span data-stu-id="95643-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="95643-147">Pour plus d’informations sur le schéma de webhook sur les alertes de journal d’activité, consultez [Webhooks pour les alertes du journal d’activité Azure](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="95643-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="95643-148">Le groupe d’actions défini dans cette procédure est réutilisable en tant que groupe d’actions existant, pour la définition de toutes les futures alertes.</span><span class="sxs-lookup"><span data-stu-id="95643-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="95643-149">Créer une alerte sur une notification sur l’intégrité du service pour un groupe d’actions existant à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="95643-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="95643-150">Suivez les étapes 1 à 7 dans la section précédente pour créer votre notification d’intégrité du service.</span><span class="sxs-lookup"><span data-stu-id="95643-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="95643-151">Sous **Alerte via**, sélectionnez le bouton du groupe d’actions **Existant**.</span><span class="sxs-lookup"><span data-stu-id="95643-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="95643-152">Sélectionnez le groupe d’actions approprié.</span><span class="sxs-lookup"><span data-stu-id="95643-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="95643-153">Sélectionnez **OK** pour créer l’alerte.</span><span class="sxs-lookup"><span data-stu-id="95643-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="95643-154">Dans quelques minutes, l’alerte est active et commence à se déclencher en fonction des conditions que vous avez spécifiées lors de la création.</span><span class="sxs-lookup"><span data-stu-id="95643-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="95643-155">Gérez vos alertes</span><span class="sxs-lookup"><span data-stu-id="95643-155">Manage your alerts</span></span>

<span data-ttu-id="95643-156">Une fois l’alerte créée, elle apparaît dans la section **Alertes** du panneau **Moniteur**.</span><span class="sxs-lookup"><span data-stu-id="95643-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="95643-157">Sélectionnez l’alerte que vous souhaitez gérer pour :</span><span class="sxs-lookup"><span data-stu-id="95643-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="95643-158">la modifier</span><span class="sxs-lookup"><span data-stu-id="95643-158">Edit it.</span></span>
* <span data-ttu-id="95643-159">la supprimer</span><span class="sxs-lookup"><span data-stu-id="95643-159">Delete it.</span></span>
* <span data-ttu-id="95643-160">la désactiver ou l’activer si vous voulez arrêter temporairement ou reprendre la réception de notifications pour l’alerte.</span><span class="sxs-lookup"><span data-stu-id="95643-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95643-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95643-161">Next steps</span></span>
- <span data-ttu-id="95643-162">En savoir plus sur les [notifications sur l’intégrité du service](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="95643-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="95643-163">En savoir plus sur la [limitation du débit des notifications](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="95643-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="95643-164">Consultez le [schéma webhook des alertes de journal d’activité](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="95643-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="95643-165">Obtenez une [vue d’ensemble des alertes du journal d’activité](monitoring-overview-alerts.md) et découvrez comment recevoir des alertes.</span><span class="sxs-lookup"><span data-stu-id="95643-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="95643-166">En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="95643-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
