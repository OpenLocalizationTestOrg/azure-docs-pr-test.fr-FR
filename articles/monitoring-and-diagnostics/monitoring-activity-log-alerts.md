---
title: "Créer des alertes de journal d’activité | Documents Microsoft"
description: "Recevez des notifications par SMS, webhook et e-mail lors de la survenue de certains événements dans le journal d’activité."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="45ec4-103">Créer des alertes de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="45ec4-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="45ec4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="45ec4-104">Overview</span></span>
<span data-ttu-id="45ec4-105">Les alertes de journal d’activité s’activent lorsqu’un nouvel événement du journal d’activité correspond aux conditions spécifiées dans l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="45ec4-106">Il s’agit de ressources Azure, et peuvent donc être créées à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45ec4-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="45ec4-107">Elles peuvent également être créées, mises à jour ou supprimées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="45ec4-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="45ec4-108">Cet article présente les concepts qui sous-tendent les alertes de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="45ec4-109">Cet article décrit comment utiliser le portail Azure pour configurer une alerte sur les événements de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="45ec4-110">En général, vous créez des alertes du journal d’activité pour recevoir des notifications lorsque :</span><span class="sxs-lookup"><span data-stu-id="45ec4-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="45ec4-111">des modifications spécifiques se produisent dans votre abonnement Azure, souvent étendues à des groupes de ressources ou à des ressources.</span><span class="sxs-lookup"><span data-stu-id="45ec4-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="45ec4-112">Par exemple, vous pouvez désirer être averti lorsqu’une machine virtuelle dans myProductionResourceGroup est supprimée.</span><span class="sxs-lookup"><span data-stu-id="45ec4-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="45ec4-113">Vous pouvez également vouloir être averti si de nouveaux rôles sont attribués à un utilisateur dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="45ec4-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="45ec4-114">Un événement d’intégrité du service se produit.</span><span class="sxs-lookup"><span data-stu-id="45ec4-114">A service health event occurs.</span></span> <span data-ttu-id="45ec4-115">Les événements d’intégrité du service incluent la notification des incidents et des événements de maintenance qui s’appliquent aux ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="45ec4-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="45ec4-116">Dans les deux cas, l’alerte du journal d’activité surveille uniquement les événements de l’abonnement dans lequel elle a été créée.</span><span class="sxs-lookup"><span data-stu-id="45ec4-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="45ec4-117">Vous pouvez configurer une alerte de journal d’activité en fonction de n’importe quelle propriété de niveau supérieur de l’objet JSON d’un événement de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="45ec4-118">Toutefois, le portail affiche uniquement les options les plus courantes :</span><span class="sxs-lookup"><span data-stu-id="45ec4-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="45ec4-119">**Catégorie** : administration, intégrité du service, mise à l’échelle automatique et recommandation.</span><span class="sxs-lookup"><span data-stu-id="45ec4-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="45ec4-120">Pour plus d’informations, reportez-vous à la rubrique [Présentation du journal d’activité Azure](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="45ec4-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="45ec4-121">Pour en savoir plus sur les événements d’intégrité du service, consultez [Recevoir des alertes de journal d’activité sur les notifications de service](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="45ec4-122">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="45ec4-122">**Resource group**</span></span>
- <span data-ttu-id="45ec4-123">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="45ec4-123">**Resource**</span></span>
- <span data-ttu-id="45ec4-124">**Type de ressource**</span><span class="sxs-lookup"><span data-stu-id="45ec4-124">**Resource type**</span></span>
- <span data-ttu-id="45ec4-125">**Nom de l’opération** : le nom de l’opération de Contrôle d’accès basé sur le rôle de Gestionnaire des ressources.</span><span class="sxs-lookup"><span data-stu-id="45ec4-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="45ec4-126">**Niveau** : le niveau de gravité de l’événement (détaillé, informationnel, avertissement, erreur ou critique).</span><span class="sxs-lookup"><span data-stu-id="45ec4-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="45ec4-127">**État** : l’état de l’événement, généralement « Démarré », « Échoué » ou « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="45ec4-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="45ec4-128">**Événement lancé par** : également appelé l’« appelant ».</span><span class="sxs-lookup"><span data-stu-id="45ec4-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="45ec4-129">L’adresse e-mail ou l’identificateur Azure Active Directory de l’utilisateur qui a effectué l’opération.</span><span class="sxs-lookup"><span data-stu-id="45ec4-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="45ec4-130">Vous devez spécifier au moins deux des critères précédents dans votre alerte. Le critère de catégorie est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="45ec4-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="45ec4-131">L’alerte créée ne s’activera peut-être pas à chaque fois qu’un événement sera créé dans les journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="45ec4-132">Lorsqu’une alerte du journal d’activité devient active, elle utilise un groupe d’actions pour générer des actions ou des notifications.</span><span class="sxs-lookup"><span data-stu-id="45ec4-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="45ec4-133">Un groupe d’actions est un jeu réutilisable de destinataires de notifications, telles que des adresses de messagerie, des URL webhook ou des numéros de téléphone SMS.</span><span class="sxs-lookup"><span data-stu-id="45ec4-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="45ec4-134">Les destinataires peuvent être référencés à partir de plusieurs alertes pour centraliser et regrouper vos canaux de notification.</span><span class="sxs-lookup"><span data-stu-id="45ec4-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="45ec4-135">Lorsque vous définissez votre alerte de journal d’activité, vous avez deux options.</span><span class="sxs-lookup"><span data-stu-id="45ec4-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="45ec4-136">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="45ec4-136">You can:</span></span>

* <span data-ttu-id="45ec4-137">utiliser un groupe d’actions existant dans votre alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="45ec4-138">créer un nouveau groupe d’action.</span><span class="sxs-lookup"><span data-stu-id="45ec4-138">Create a new action group.</span></span> 

<span data-ttu-id="45ec4-139">Pour en savoir plus sur les groupes d’actions, consultez [Créer et gérer des groupes d’actions dans le portail Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="45ec4-140">Pour en savoir plus sur les notifications d’intégrité du service, consultez [Recevoir des alertes de journal d’activité sur les notifications d’intégrité du service](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="45ec4-141">Créer une alerte pour un événement du journal d’activité avec un nouveau groupe d’actions dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="45ec4-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="45ec4-142">Dans le [portail](https://portal.azure.com), sélectionnez **Moniteur**.</span><span class="sxs-lookup"><span data-stu-id="45ec4-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Le service « Moniteur »](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="45ec4-144">Dans la section **Journal d’activité**, sélectionnez **Alertes**.</span><span class="sxs-lookup"><span data-stu-id="45ec4-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![L’onglet « Alertes »](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="45ec4-146">Sélectionnez **Ajouter une alerte de journal d’activité**, puis renseignez les champs.</span><span class="sxs-lookup"><span data-stu-id="45ec4-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="45ec4-147">Entrez un nom dans la boîte **Nom de l’alerte activité journal** et sélectionnez une **Description**.</span><span class="sxs-lookup"><span data-stu-id="45ec4-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![La commande « Ajouter une alerte activité journal »](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="45ec4-149">La boîte **Abonnement** est automatiquement renseignée avec votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="45ec4-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="45ec4-150">Cet abonnement est celui dans lequel le groupe d’actions sera enregistré.</span><span class="sxs-lookup"><span data-stu-id="45ec4-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="45ec4-151">La ressource d’alerte est déployée pour cet abonnement et surveille les événements du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![La boîte de dialogue « Ajouter une alerte activité journal »](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="45ec4-153">Sélectionnez le **Groupe de ressources** dans lequel la ressource d’alerte est créée.</span><span class="sxs-lookup"><span data-stu-id="45ec4-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="45ec4-154">Le groupe de ressources n’est pas surveillé par l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="45ec4-155">Au lieu de cela, il s’agit du groupe de ressources où se trouve la ressource d’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="45ec4-156">Si vous le souhaitez, vous pouvez sélectionner une **Catégorie d’événement**, ce qui va modifier les filtres supplémentaires affichés.</span><span class="sxs-lookup"><span data-stu-id="45ec4-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="45ec4-157">Pour les événements d’administration, les filtres incluent **Groupe de ressources**, **Ressource**, **Type de ressource**, **Nom de l’opération**, **Niveau**, **État**, et **Événement initié par**.</span><span class="sxs-lookup"><span data-stu-id="45ec4-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="45ec4-158">Ces valeurs identifient les événements que cette alerte doit surveiller.</span><span class="sxs-lookup"><span data-stu-id="45ec4-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="45ec4-159">Vous devez spécifier au moins l’un des critères précédents dans votre alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="45ec4-160">L’alerte créée ne s’activera peut-être pas à chaque fois qu’un événement sera créé dans les journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="45ec4-161">Entrez un nom dans la boîte **Nom du groupe d’actions** et entrez un nom dans la boîte **Nom court**.</span><span class="sxs-lookup"><span data-stu-id="45ec4-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="45ec4-162">Le nom court est utilisé à la place d’un nom de groupe d’actions complet lorsque les notifications sont envoyées à l’aide de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="45ec4-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="45ec4-163">Définissez une liste d’actions en indiquant les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="45ec4-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="45ec4-164">a.</span><span class="sxs-lookup"><span data-stu-id="45ec4-164">a.</span></span> <span data-ttu-id="45ec4-165">**Nom** : entrez le nom, alias ou identificateur de l’action.</span><span class="sxs-lookup"><span data-stu-id="45ec4-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="45ec4-166">b.</span><span class="sxs-lookup"><span data-stu-id="45ec4-166">b.</span></span> <span data-ttu-id="45ec4-167">**Type d’action** : sélectionnez SMS, e-mail ou webhook.</span><span class="sxs-lookup"><span data-stu-id="45ec4-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="45ec4-168">c.</span><span class="sxs-lookup"><span data-stu-id="45ec4-168">c.</span></span> <span data-ttu-id="45ec4-169">**Détails** : selon le type d’action, entrez un numéro de téléphone, une adresse e-mail ou une URI de Webhook.</span><span class="sxs-lookup"><span data-stu-id="45ec4-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="45ec4-170">Sélectionnez **OK** pour créer l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="45ec4-171">L’alerte prend quelques minutes pour se propager entièrement et devenir active.</span><span class="sxs-lookup"><span data-stu-id="45ec4-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="45ec4-172">Elle se déclenche lorsque de nouveaux événements correspondent aux critères de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="45ec4-173">Pour plus d’informations, consultez [Comprendre le schéma webhook utilisé dans les alertes de journal d’activité](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="45ec4-174">Le groupe d’actions défini dans cette procédure est réutilisable en tant que groupe d’actions existant, pour la définition de toutes les futures alertes.</span><span class="sxs-lookup"><span data-stu-id="45ec4-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="45ec4-175">Créer une alerte concernant un événement du journal d’activité pour un groupe d’actions existant dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="45ec4-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="45ec4-176">Suivez les étapes 1 à 7 dans la section précédente pour créer votre alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="45ec4-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="45ec4-177">Sous **Notifier via**, sélectionnez le bouton du groupe d’actions **Existant**.</span><span class="sxs-lookup"><span data-stu-id="45ec4-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="45ec4-178">Sélectionnez un groupe d’actions existant dans la liste.</span><span class="sxs-lookup"><span data-stu-id="45ec4-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="45ec4-179">Sélectionnez **OK** pour créer l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="45ec4-180">L’alerte prend quelques minutes pour se propager entièrement et devenir active.</span><span class="sxs-lookup"><span data-stu-id="45ec4-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="45ec4-181">Elle se déclenche lorsque de nouveaux événements correspondent aux critères de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="45ec4-182">Gérez vos alertes</span><span class="sxs-lookup"><span data-stu-id="45ec4-182">Manage your alerts</span></span>

<span data-ttu-id="45ec4-183">Une fois l’alerte créée, elle apparaît dans la section Alertes du panneau Surveillance.</span><span class="sxs-lookup"><span data-stu-id="45ec4-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="45ec4-184">Sélectionnez l’alerte que vous souhaitez gérer pour :</span><span class="sxs-lookup"><span data-stu-id="45ec4-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="45ec4-185">la modifier</span><span class="sxs-lookup"><span data-stu-id="45ec4-185">Edit it.</span></span>
* <span data-ttu-id="45ec4-186">la supprimer</span><span class="sxs-lookup"><span data-stu-id="45ec4-186">Delete it.</span></span>
* <span data-ttu-id="45ec4-187">la désactiver ou l’activer si vous voulez arrêter temporairement ou reprendre la réception de notifications pour l’alerte.</span><span class="sxs-lookup"><span data-stu-id="45ec4-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45ec4-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45ec4-188">Next steps</span></span>
- <span data-ttu-id="45ec4-189">Obtenir une [vue d’ensemble des alertes](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="45ec4-190">En savoir plus sur la [limitation du débit des notifications](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="45ec4-191">Consultez le [schéma webhook des alertes de journal d’activité](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="45ec4-192">En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="45ec4-193">En savoir plus sur les [notifications sur l’intégrité du service](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="45ec4-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="45ec4-194">Créer une [alerte de journal d’activité pour surveiller toutes les opérations du moteur de mise à l’échelle automatique dans votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="45ec4-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="45ec4-195">Créer une [alerte de journal d’activité pour surveiller tous les échecs d’opérations de mise à l’échelle automatique dans votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="45ec4-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
