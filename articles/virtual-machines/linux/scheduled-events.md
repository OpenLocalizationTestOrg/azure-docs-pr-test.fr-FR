---
title: "Événements planifiés pour les machines virtuelles Linux dans Azure | Microsoft Docs"
description: "Événements planifiés avec le service de métadonnées Azure sur vos machines virtuelles Linux."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: 75e509a7e39f5b268ce550d0c4dea2261d4fe56f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="0ae7c-103">Service de métadonnées Azure : Événements planifiés (préversion) pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="0ae7c-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="0ae7c-104">Les préversions sont à votre disposition, à condition que vous acceptiez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="0ae7c-105">Pour plus d’informations, consultez [Conditions d’Utilisation Supplémentaires relatives aux Évaluations Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="0ae7c-106">Le sous-service des événements planifiés est un des sous-services du service de métadonnées Azure.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="0ae7c-107">Ce sous-service est responsable de la mise à disposition des informations concernant les événements à venir (par exemple un redémarrage), pour que votre application puisse s’y préparer et limiter ainsi l’interruption.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="0ae7c-108">Il est disponible pour tous types de machines virtuelles Azure, notamment PaaS et IaaS.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="0ae7c-109">Le sous-service des événements planifiés donne à votre machine virtuelle le temps d’effectuer des tâches préventives pour réduire l’impact d’un événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="0ae7c-110">Le sous-service des événements planifiés est disponible pour les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="0ae7c-111">Pour plus d’informations sur les événements planifiés sur Windows, consultez [Événements planifiés pour les machines virtuelles Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="0ae7c-112">Pourquoi choisir les événements planifiés ?</span><span class="sxs-lookup"><span data-stu-id="0ae7c-112">Why Scheduled Events?</span></span>

<span data-ttu-id="0ae7c-113">Avec les événements planifiés, vous pouvez prendre des mesures pour limiter l’impact sur votre service de la maintenance lancée par la plateforme ou d’actions lancées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="0ae7c-114">Les charges de travail à instances multiples, qui utilisent des techniques de réplication pour maintenir leur état, peuvent être vulnérables si des interruptions affectent plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="0ae7c-115">Ces pannes peuvent entraîner de tâches coûteuses (par exemple, la reconstruction des index) ou même une perte de réplica.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="0ae7c-116">Dans de nombreux autres cas, la disponibilité globale du service peut être améliorée en effectuant une séquence d’arrêt progressif, comme terminer (ou annuler) des transactions en cours, réaffecter des tâches à d’autres machines virtuelles du cluster (basculement manuel) ou supprimer la machine virtuelle d’un pool d’équilibreur de charge du réseau.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="0ae7c-117">Dans certains cas, le fait d’avertir un administrateur d’un événement à venir ou de consigner un tel événement facilite la gestion des applications hébergées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="0ae7c-118">Le service de métadonnées Azure s’appuie sur les événements planifiés dans les cas d’utilisation suivants :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="0ae7c-119">La plateforme a lancé une maintenance (par exemple, le déploiement du système d’exploitation hôte)</span><span class="sxs-lookup"><span data-stu-id="0ae7c-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="0ae7c-120">L’utilisateur a lancé des appels (par exemple, un utilisateur redémarre ou redéploie une machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="0ae7c-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="0ae7c-121">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="0ae7c-121">The basics</span></span>  

<span data-ttu-id="0ae7c-122">Le service de métadonnées Azure expose des informations sur les machines virtuelles en cours d’exécution en utilisant un point de terminaison REST accessible depuis la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="0ae7c-123">Les informations sont disponibles via une adresse IP non routable, de façon à ce qu’elles ne soient pas exposées en dehors de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="0ae7c-124">Scope</span><span class="sxs-lookup"><span data-stu-id="0ae7c-124">Scope</span></span>
<span data-ttu-id="0ae7c-125">Les événements planifiés sont présentés à toutes les machines virtuelles dans un service cloud ou à toutes les machines virtuelles dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="0ae7c-126">Par conséquent, vous devez vérifier le champ `Resources` de l’événement pour identifier les machines virtuelles qui seront affectées.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="0ae7c-127">Découverte du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="0ae7c-127">Discovering the endpoint</span></span>
<span data-ttu-id="0ae7c-128">Si une machine virtuelle est créée au sein d’un réseau virtuel (VNet), le service de métadonnées est disponible à partir d’une adresse IP statique non routable, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="0ae7c-129">Si la machine virtuelle n’est pas créée au sein d’un réseau virtuel, les cas par défaut pour les services cloud et les machines virtuelles classiques, une logique supplémentaire est nécessaire pour découvrir le point de terminaison à utiliser.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="0ae7c-130">Reportez-vous à cet exemple pour savoir comment [découvrir le point de terminaison hôte](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="0ae7c-131">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="0ae7c-131">Versioning</span></span> 
<span data-ttu-id="0ae7c-132">Le service de métadonnées Instance fait l’objet d’une gestion de version.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0ae7c-133">Les versions sont obligatoires et la version actuelle est `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0ae7c-134">Les préversions précédentes des événements planifiés prenaient en charge {dernière version} en tant que version de l’api.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="0ae7c-135">Ce format n’est plus pris en charge et sera déconseillé à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0ae7c-136">Utilisation d’en-têtes</span><span class="sxs-lookup"><span data-stu-id="0ae7c-136">Using headers</span></span>
<span data-ttu-id="0ae7c-137">Quand vous interrogez le service de métadonnées, vous devez fournir l’en-tête `Metadata: true` pour garantir que la demande n’a pas été redirigée involontairement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="0ae7c-138">Activation des événements planifiés</span><span class="sxs-lookup"><span data-stu-id="0ae7c-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="0ae7c-139">La première fois que vous faites une demande d’événements planifiés, Azure active implicitement la fonctionnalité sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="0ae7c-140">Par conséquent, attendez-vous à un retard pouvant atteindre deux minutes dans la réponse à votre premier appel.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="0ae7c-141">Maintenance initiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="0ae7c-141">User initiated maintenance</span></span>
<span data-ttu-id="0ae7c-142">La maintenance de machine virtuelle initiée par l’utilisateur via le portail Azure, l’API, l’interface CLI ou PowerShell entraîne un événement planifié.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="0ae7c-143">Cela vous permet de tester la logique de préparation de la maintenance dans votre application et permet à votre application de se préparer à la maintenance initiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="0ae7c-144">Le redémarrage d’une machine virtuelle planifie un événement de type `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="0ae7c-145">Le redéploiement d’une machine virtuelle planifie un événement de type `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0ae7c-146">Actuellement, 10 opérations maximum de maintenance initiée par l’utilisateur peuvent être planifiées simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="0ae7c-147">Cette limite sera assouplie avant la disponibilité générale des Événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="0ae7c-148">Actuellement, la maintenance initiée par l’utilisateur qui résulte dans des Événements planifiés n’est pas configurable.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="0ae7c-149">La possibilité de configuration est prévue pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="0ae7c-150">Utilisation de l’API</span><span class="sxs-lookup"><span data-stu-id="0ae7c-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="0ae7c-151">Rechercher des événements</span><span class="sxs-lookup"><span data-stu-id="0ae7c-151">Query for events</span></span>
<span data-ttu-id="0ae7c-152">Vous pouvez rechercher des événements planifiés simplement en effectuant l’appel suivant :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="0ae7c-153">Une réponse contient un tableau d’événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="0ae7c-154">Un tableau vide signifie qu’il n’y a actuellement aucun événement planifié.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="0ae7c-155">S'il existe des événements planifiés, la réponse contient un tableau d’événements :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="0ae7c-156">Propriétés d’événement</span><span class="sxs-lookup"><span data-stu-id="0ae7c-156">Event properties</span></span>
|<span data-ttu-id="0ae7c-157">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ae7c-157">Property</span></span>  |  <span data-ttu-id="0ae7c-158">Description</span><span class="sxs-lookup"><span data-stu-id="0ae7c-158">Description</span></span> |
| - | - |
| <span data-ttu-id="0ae7c-159">EventId</span><span class="sxs-lookup"><span data-stu-id="0ae7c-159">EventId</span></span> | <span data-ttu-id="0ae7c-160">GUID pour cet événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="0ae7c-161">Exemple :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-161">Example:</span></span> <br><ul><li><span data-ttu-id="0ae7c-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="0ae7c-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="0ae7c-163">EventType</span><span class="sxs-lookup"><span data-stu-id="0ae7c-163">EventType</span></span> | <span data-ttu-id="0ae7c-164">Impact provoqué par cet événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="0ae7c-165">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-165">Values:</span></span> <br><ul><li> <span data-ttu-id="0ae7c-166">`Freeze` : une pause de quelques secondes est planifiée pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="0ae7c-167">Le processeur est mis en pause, mais cela n’a aucun impact sur la mémoire, les fichiers ouverts ou les connexions réseau.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="0ae7c-168">`Reboot` : un redémarrage est planifié pour la machine virtuelle (la mémoire non persistante est effacée).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="0ae7c-169">`Redeploy` : un déplacement vers un autre nœud est planifié pour la machine virtuelle (le contenu des disques éphémères est perdu).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="0ae7c-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="0ae7c-170">ResourceType</span></span> | <span data-ttu-id="0ae7c-171">Type de ressource affecté par cet événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="0ae7c-172">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="0ae7c-173">Ressources</span><span class="sxs-lookup"><span data-stu-id="0ae7c-173">Resources</span></span>| <span data-ttu-id="0ae7c-174">Liste des ressources affectées par cet événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-174">List of resources this event impacts.</span></span> <span data-ttu-id="0ae7c-175">Elle contient à coup sûr des machines d’au plus un [domaine de mise à jour](manage-availability.md), mais elle peut ne pas contenir toutes les machines du domaine utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="0ae7c-176">Exemple :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-176">Example:</span></span> <br><ul><li> <span data-ttu-id="0ae7c-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="0ae7c-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="0ae7c-178">Event Status</span><span class="sxs-lookup"><span data-stu-id="0ae7c-178">Event Status</span></span> | <span data-ttu-id="0ae7c-179">État de cet événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-179">Status of this event.</span></span> <br><br> <span data-ttu-id="0ae7c-180">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-180">Values:</span></span> <ul><li><span data-ttu-id="0ae7c-181">`Scheduled` : cet événement est planifié pour démarrer après l’heure spécifiée dans la propriété `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="0ae7c-182">`Started` : cet événement a démarré.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="0ae7c-183">Aucun état `Completed` ou similaire n’est jamais fourni, car l’événement n’est plus retourné une fois qu’il est terminé.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="0ae7c-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="0ae7c-184">NotBefore</span></span>| <span data-ttu-id="0ae7c-185">Heure après laquelle cet événement peut démarrer.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="0ae7c-186">Exemple :</span><span class="sxs-lookup"><span data-stu-id="0ae7c-186">Example:</span></span> <br><ul><li> <span data-ttu-id="0ae7c-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="0ae7c-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="0ae7c-188">Planification d’événement</span><span class="sxs-lookup"><span data-stu-id="0ae7c-188">Event scheduling</span></span>
<span data-ttu-id="0ae7c-189">Chaque événement est planifié à un minimum de temps dans le futur, en fonction du type d’événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="0ae7c-190">Cette heure est reflétée dans la propriété `NotBefore` d’un événement.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="0ae7c-191">EventType</span><span class="sxs-lookup"><span data-stu-id="0ae7c-191">EventType</span></span>  | <span data-ttu-id="0ae7c-192">Préavis minimal</span><span class="sxs-lookup"><span data-stu-id="0ae7c-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="0ae7c-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="0ae7c-193">Freeze</span></span>| <span data-ttu-id="0ae7c-194">15 minutes</span><span class="sxs-lookup"><span data-stu-id="0ae7c-194">15 minutes</span></span> |
| <span data-ttu-id="0ae7c-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="0ae7c-195">Reboot</span></span> | <span data-ttu-id="0ae7c-196">15 minutes</span><span class="sxs-lookup"><span data-stu-id="0ae7c-196">15 minutes</span></span> |
| <span data-ttu-id="0ae7c-197">Redeploy</span><span class="sxs-lookup"><span data-stu-id="0ae7c-197">Redeploy</span></span> | <span data-ttu-id="0ae7c-198">10 minutes</span><span class="sxs-lookup"><span data-stu-id="0ae7c-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="0ae7c-199">Démarrage d’un événement</span><span class="sxs-lookup"><span data-stu-id="0ae7c-199">Starting an event</span></span> 

<span data-ttu-id="0ae7c-200">Une fois que vous avez pris connaissance d’un événement à venir et effectué votre logique d’arrêt appropriée, vous pouvez approuver l’événement en suspens en effectuant un appel de `POST` au service de métadonnées avec `EventId`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="0ae7c-201">Ceci indique à Azure qu’il peut raccourcir l’heure de notification minimale (quand c’est possible).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="0ae7c-202">Le fait d’accuser réception d’un événement lui permet de poursuivre pour tous les éléments `Resources` dans l’événement, et pas seulement pour la machine virtuelle qui en accuse réception.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="0ae7c-203">Vous pouvez donc choisir de désigner un leader pour coordonner l’accusé-réception, qui peut être simplement la première machine du champ `Resources`.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="0ae7c-204">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="0ae7c-204">Python sample</span></span> 

<span data-ttu-id="0ae7c-205">L’exemple suivant interroge le serveur de métadonnées pour obtenir les événements planifiés et approuve chaque événement en suspens.</span><span class="sxs-lookup"><span data-stu-id="0ae7c-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="0ae7c-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ae7c-206">Next steps</span></span> 

- <span data-ttu-id="0ae7c-207">Découvrez plus d’informations sur les API disponibles dans le [service de métadonnées d’instance](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-207">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="0ae7c-208">Découvrez plus d’informations sur la [maintenance planifiée pour les machines virtuelles Linux dans Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="0ae7c-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
