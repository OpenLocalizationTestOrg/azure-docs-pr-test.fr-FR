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
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="c3b45-103">Flux tooEvent du journal des activités Azure hello concentrateurs</span><span class="sxs-lookup"><span data-stu-id="c3b45-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="c3b45-104">Hello [ **journal des activités Azure** ](monitoring-overview-activity-logs.md) peut être transmis en continu côté application tooany en temps réel à l’aide de l’option des « Exportation » hello intégrée dans le portail de hello, ou en activant hello Id de règle de Bus de Service dans un profil de journal via hello CLI des applets de commande PowerShell Azure ou Azure.</span><span class="sxs-lookup"><span data-stu-id="c3b45-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="c3b45-105">Ce que vous pouvez faire avec hello journal d’activité et les concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="c3b45-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="c3b45-106">Voici quelques méthodes, vous pouvez utiliser hello de diffusion en continu de la fonctionnalité de hello journal d’activité :</span><span class="sxs-lookup"><span data-stu-id="c3b45-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="c3b45-107">**Flux des systèmes de journalisation et les données de télémétrie toothird tiers** – au fil du temps, le concentrateurs d’événements de diffusion en continu deviennent hello mécanisme toopipe votre journal des activités dans les serveurs SIEM de tiers et les solutions analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="c3b45-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="c3b45-108">**Générer une télémétrie personnalisée et la plateforme de journalisation** : Si vous disposez déjà d’une plateforme de télémétrie personnalisées ou sont simplement penser à la génération 1, hello hautement évolutive de publication / abonnement nature des concentrateurs d’événements vous permet de tooflexibly réception hello journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="c3b45-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="c3b45-109">Consultez le toousing de Dan Rosanova guide concentrateurs d’événements dans une plateforme de télémétrie à l’échelle mondiale ici.</span><span class="sxs-lookup"><span data-stu-id="c3b45-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="c3b45-110">Activer la diffusion en continu de hello journal d’activité</span><span class="sxs-lookup"><span data-stu-id="c3b45-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="c3b45-111">Vous pouvez activer la diffusion en continu de hello journal d’activité par programmation ou via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="c3b45-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="c3b45-112">Dans les deux cas, vous choisissez un Namespace de Bus de Service et une stratégie d’accès partagé pour cet espace de noms et un concentrateur d’événements est créé dans cet espace de noms lors de l’événement du journal d’activité de nouvelle première hello se produit.</span><span class="sxs-lookup"><span data-stu-id="c3b45-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="c3b45-113">Si vous n’avez pas un Namespace de Bus de Service, vous devez d’abord toocreate une.</span><span class="sxs-lookup"><span data-stu-id="c3b45-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="c3b45-114">Si vous avez précédemment transmis en continu toothis événements de journal d’activité Service Bus Namespace, hello concentrateur d’événements qui a été créé précédemment est réutilisée.</span><span class="sxs-lookup"><span data-stu-id="c3b45-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="c3b45-115">stratégie d’accès partagé de Hello définit des autorisations de hello qui a du mécanisme de diffusion en continu hello.</span><span class="sxs-lookup"><span data-stu-id="c3b45-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="c3b45-116">Aujourd'hui, la diffusion en continu de concentrateurs d’événements tooan requiert **gérer**, **envoyer**, et **écouter** autorisations.</span><span class="sxs-lookup"><span data-stu-id="c3b45-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="c3b45-117">Vous pouvez créer ou modifier des stratégies d’accès Namespace de Bus de Service partagé dans le portail classique de hello sous l’onglet « Configurer » de hello pour votre Namespace de Bus de Service.</span><span class="sxs-lookup"><span data-stu-id="c3b45-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="c3b45-118">tooupdate hello de diffusion en continu de journal d’activité journal profil tooinclude, utilisateur hello hello modification doit avoir l’autorisation de ListKey de hello sur cette règle d’autorisation du Bus de Service.</span><span class="sxs-lookup"><span data-stu-id="c3b45-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="c3b45-119">Hello service bus ou l’événement espace de noms hub n’a pas toobe Bonjour même abonnement que l’abonnement hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.</span><span class="sxs-lookup"><span data-stu-id="c3b45-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="c3b45-120">Via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c3b45-120">Via Azure portal</span></span>
1. <span data-ttu-id="c3b45-121">Accédez toohello **le journal d’activité** panneau à l’aide du menu de hello sur hello gauche du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="c3b45-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Accédez tooActivity journal dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="c3b45-123">Cliquez sur hello **exporter** bouton en haut de hello du panneau des hello.</span><span class="sxs-lookup"><span data-stu-id="c3b45-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Bouton Exporter dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="c3b45-125">Dans le panneau hello qui s’affiche, vous pouvez sélectionner les régions hello pour lequel vous souhaitez que les événements toostream et hello Service Bus Namespace dans lequel vous souhaitez qu’un toobe concentrateur d’événements créé pour ces événements de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="c3b45-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Panneau Exporter le journal d’activité](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="c3b45-127">Cliquez sur **enregistrer** toosave ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="c3b45-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="c3b45-128">paramètres de Hello sont alors immédiatement appliquée tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3b45-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="c3b45-129">Via les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3b45-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="c3b45-130">Si un profil du journal existe déjà, vous devez tout d’abord tooremove ce profil.</span><span class="sxs-lookup"><span data-stu-id="c3b45-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="c3b45-131">Utilisez `Get-AzureRmLogProfile` tooidentify si un profil du journal existe</span><span class="sxs-lookup"><span data-stu-id="c3b45-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="c3b45-132">Dans ce cas, utilisez `Remove-AzureRmLogProfile` tooremove il.</span><span class="sxs-lookup"><span data-stu-id="c3b45-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="c3b45-133">Utilisez `Set-AzureRmLogProfile` toocreate un profil :</span><span class="sxs-lookup"><span data-stu-id="c3b45-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="c3b45-134">Hello ID de règle de Bus de Service est une chaîne au format suivant : {ID de ressource de bus de service} /authorizationrules/ {nom de la clé}, par exemple</span><span class="sxs-lookup"><span data-stu-id="c3b45-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="c3b45-135">Via l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c3b45-135">Via Azure CLI</span></span>
<span data-ttu-id="c3b45-136">Si un profil du journal existe déjà, vous devez tout d’abord tooremove ce profil.</span><span class="sxs-lookup"><span data-stu-id="c3b45-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="c3b45-137">Utilisez `azure insights logprofile list` tooidentify si un profil du journal existe</span><span class="sxs-lookup"><span data-stu-id="c3b45-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="c3b45-138">Dans ce cas, utilisez `azure insights logprofile delete` tooremove il.</span><span class="sxs-lookup"><span data-stu-id="c3b45-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="c3b45-139">Utilisez `azure insights logprofile add` toocreate un profil :</span><span class="sxs-lookup"><span data-stu-id="c3b45-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="c3b45-140">Hello ID de règle de Bus de Service est une chaîne au format suivant : `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="c3b45-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="c3b45-141">Comment consommer des données de journal hello de concentrateurs d’événements ?</span><span class="sxs-lookup"><span data-stu-id="c3b45-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="c3b45-142">[schéma Hello hello journal d’activité est disponible ici](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="c3b45-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="c3b45-143">Chaque événement est dans un tableau d’objets blob JSON appelé « enregistrements ».</span><span class="sxs-lookup"><span data-stu-id="c3b45-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3b45-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3b45-144">Next Steps</span></span>
* [<span data-ttu-id="c3b45-145">Hello d’archive compte de stockage tooa de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="c3b45-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="c3b45-146">Vue d’ensemble de lecture hello Hello journal des activités Azure</span><span class="sxs-lookup"><span data-stu-id="c3b45-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="c3b45-147">Définir une alerte basée sur un événement de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="c3b45-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

