---
title: "alertes du journal d’activité aaaReceive sur les notifications de service | Documents Microsoft"
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
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="383db-103">Créer des alertes de journal d’activité sur les notifications de service</span><span class="sxs-lookup"><span data-stu-id="383db-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="383db-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="383db-104">Overview</span></span>
<span data-ttu-id="383db-105">Cet article vous explique comment tooset journal d’activité des alertes pour les notifications de contrôle d’intégrité de service à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="383db-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="383db-106">Vous pouvez recevoir une alerte lorsque Azure envoie des notifications tooyour abonnement Azure de service d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="383db-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="383db-107">Vous pouvez configurer l’alerte hello en fonction de :</span><span class="sxs-lookup"><span data-stu-id="383db-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="383db-108">classe Hello de notification de contrôle d’intégrité de service (incident, maintenance, informations, etc.).</span><span class="sxs-lookup"><span data-stu-id="383db-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="383db-109">Hello ou les services concernés.</span><span class="sxs-lookup"><span data-stu-id="383db-109">hello service(s) affected.</span></span>
- <span data-ttu-id="383db-110">Hello ou des régions affectées.</span><span class="sxs-lookup"><span data-stu-id="383db-110">hello region(s) affected.</span></span>
- <span data-ttu-id="383db-111">état de Hello de notification de hello (active ou résolu).</span><span class="sxs-lookup"><span data-stu-id="383db-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="383db-112">niveau Hello de notifications de hello (information, avertissement, erreur).</span><span class="sxs-lookup"><span data-stu-id="383db-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="383db-113">Vous pouvez également configurer qui alerte de hello doit être envoyé à :</span><span class="sxs-lookup"><span data-stu-id="383db-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="383db-114">sélectionner un groupe d’actions existant ;</span><span class="sxs-lookup"><span data-stu-id="383db-114">Select an existing action group.</span></span>
- <span data-ttu-id="383db-115">créer un nouveau groupe d’actions (qui peut être utilisé pour les alertes futures).</span><span class="sxs-lookup"><span data-stu-id="383db-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="383db-116">toolearn savoir plus sur les groupes d’actions, consultez [créer et gérer des groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="383db-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="383db-117">Pour plus d’informations sur la notification de contrôle d’intégrité du service tooconfigure des alertes à l’aide de modèles Azure Resource Manager, consultez [modèles Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="383db-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="383db-118">Créer une alerte sur une notification de contrôle d’intégrité de service pour un nouveau groupe d’actions à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="383db-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="383db-119">Bonjour [portal](https://portal.azure.com), sélectionnez **analyse**.</span><span class="sxs-lookup"><span data-stu-id="383db-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Hello service de « Analyse »](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="383db-121">Bonjour **le journal d’activité** section, sélectionnez **alertes**.</span><span class="sxs-lookup"><span data-stu-id="383db-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![onglet de « Alertes » Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="383db-123">Sélectionnez **ajouter une alerte journal activité**et renseignez les champs hello.</span><span class="sxs-lookup"><span data-stu-id="383db-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![Hello « Ajouter une alerte de journal d’activité » de commande](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="383db-125">Entrez un nom dans hello **nom de l’alerte activité journal** zone et fournissez un **Description**.</span><span class="sxs-lookup"><span data-stu-id="383db-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![boîte de dialogue « Ajouter une alerte de journal d’activité » Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="383db-127">Hello **abonnement** zone autofills avec votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="383db-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="383db-128">Cet abonnement est alerte de journal utilisé toosave hello activité.</span><span class="sxs-lookup"><span data-stu-id="383db-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="383db-129">ressources d’alerte Hello est toothis déployé les événements d’un abonnement et des analyses dans le journal d’activité hello pour qu’il.</span><span class="sxs-lookup"><span data-stu-id="383db-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="383db-130">Sélectionnez hello **groupe de ressources** les Bonjour ressource alerte est créée.</span><span class="sxs-lookup"><span data-stu-id="383db-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="383db-131">Cela n’est pas le groupe de ressources hello qui est surveillé par l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="383db-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="383db-132">Au lieu de cela, il s’agit de groupe de ressources de hello où se trouve la ressource d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="383db-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="383db-133">Bonjour **catégorie d’événement** boîte, sélectionnez **l’intégrité du Service**.</span><span class="sxs-lookup"><span data-stu-id="383db-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="383db-134">Si vous le souhaitez, sélectionnez hello **Service**, **région**, **Type**, **état**, et **niveau** de service notifications de contrôle d’intégrité que vous souhaitez tooreceive.</span><span class="sxs-lookup"><span data-stu-id="383db-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="383db-135">Sous **alerte via**, sélectionnez hello **nouveau** bouton d’action de groupe.</span><span class="sxs-lookup"><span data-stu-id="383db-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="383db-136">Entrez un nom dans hello **nom d’Action groupe** zone et entrez un nom dans hello **nom court** boîte.</span><span class="sxs-lookup"><span data-stu-id="383db-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="383db-137">nom court de Hello est référencé dans les notifications hello qui sont envoyées lorsque cette alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="383db-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="383db-138">Définir une liste de destinataires en fournissant du récepteur hello :</span><span class="sxs-lookup"><span data-stu-id="383db-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="383db-139">a.</span><span class="sxs-lookup"><span data-stu-id="383db-139">a.</span></span> <span data-ttu-id="383db-140">**Nom**: entrez le nom du récepteur hello, alias ou identificateur.</span><span class="sxs-lookup"><span data-stu-id="383db-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="383db-141">b.</span><span class="sxs-lookup"><span data-stu-id="383db-141">b.</span></span> <span data-ttu-id="383db-142">**Type d’action** : sélectionnez SMS, e-mail ou webhook.</span><span class="sxs-lookup"><span data-stu-id="383db-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="383db-143">c.</span><span class="sxs-lookup"><span data-stu-id="383db-143">c.</span></span> <span data-ttu-id="383db-144">**Détails**: selon le type d’action hello choisi, entrez un numéro de téléphone, une adresse de messagerie ou un webhook URI.</span><span class="sxs-lookup"><span data-stu-id="383db-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="383db-145">Sélectionnez **OK** alerte de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="383db-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="383db-146">Dans quelques minutes, alerte de hello est actif et commence tootrigger en fonction des conditions hello que vous avez spécifié lors de la création.</span><span class="sxs-lookup"><span data-stu-id="383db-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="383db-147">Pour plus d’informations sur le schéma de webhook hello pour les alertes de journal d’activité, consultez [Webhooks pour l’activité Azure journaliser les alertes](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="383db-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="383db-148">groupe d’actions Hello définie dans ces étapes est réutilisable en tant qu’un groupe d’actions existant pour toutes les définitions d’alerte futures.</span><span class="sxs-lookup"><span data-stu-id="383db-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="383db-149">Créer une alerte sur une notification de contrôle d’intégrité de service pour un groupe d’actions à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="383db-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="383db-150">Suivez les étapes 1 à 7 dans hello précédente section toocreate votre notification de contrôle d’intégrité du service.</span><span class="sxs-lookup"><span data-stu-id="383db-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="383db-151">Sous **alerte via**, sélectionnez hello **existant** bouton d’action de groupe.</span><span class="sxs-lookup"><span data-stu-id="383db-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="383db-152">Sélectionnez le groupe d’actions approprié hello.</span><span class="sxs-lookup"><span data-stu-id="383db-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="383db-153">Sélectionnez **OK** alerte de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="383db-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="383db-154">Dans quelques minutes, alerte de hello est actif et commence tootrigger en fonction des conditions hello que vous avez spécifié lors de la création.</span><span class="sxs-lookup"><span data-stu-id="383db-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="383db-155">Gérez vos alertes</span><span class="sxs-lookup"><span data-stu-id="383db-155">Manage your alerts</span></span>

<span data-ttu-id="383db-156">Après avoir créé une alerte, elle est visible dans hello **alertes** section Hello **moniteur** panneau.</span><span class="sxs-lookup"><span data-stu-id="383db-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="383db-157">Sélectionnez l’alerte hello toomanage à :</span><span class="sxs-lookup"><span data-stu-id="383db-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="383db-158">la modifier</span><span class="sxs-lookup"><span data-stu-id="383db-158">Edit it.</span></span>
* <span data-ttu-id="383db-159">la supprimer</span><span class="sxs-lookup"><span data-stu-id="383db-159">Delete it.</span></span>
* <span data-ttu-id="383db-160">Désactiver ou activer, si vous souhaitez tootemporarily arrêter ou reprenez la réception des notifications d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="383db-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="383db-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="383db-161">Next steps</span></span>
- <span data-ttu-id="383db-162">En savoir plus sur les [notifications sur l’intégrité du service](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="383db-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="383db-163">En savoir plus sur la [limitation du débit des notifications](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="383db-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="383db-164">Hello de révision [webhook alerte schéma des journaux d’activité](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="383db-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="383db-165">Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md)et découvrez comment tooreceive alertes.</span><span class="sxs-lookup"><span data-stu-id="383db-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="383db-166">En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="383db-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
