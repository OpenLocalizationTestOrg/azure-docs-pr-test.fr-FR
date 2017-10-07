---
title: "aaaScheduled événements pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Événements planifiés à l’aide du service de métadonnées de Azure hello pour sur vos machines virtuelles de Linux."
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
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="2bd73-103">Service de métadonnées Azure : Événements planifiés (préversion) pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="2bd73-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="2bd73-104">Aperçus deviennent tooyou disponible sur condition hello que vous acceptez les conditions d’utilisation de toohello.</span><span class="sxs-lookup"><span data-stu-id="2bd73-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="2bd73-105">Pour plus d’informations, consultez [Conditions d’Utilisation Supplémentaires relatives aux Évaluations Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="2bd73-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="2bd73-106">Les événements planifiés est un des sous-Services hello sous hello Azure métadonnées de Service.</span><span class="sxs-lookup"><span data-stu-id="2bd73-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="2bd73-107">Ce sous-service est responsable de la mise à disposition des informations concernant les événements à venir (par exemple un redémarrage), pour que votre application puisse s’y préparer et limiter ainsi l’interruption.</span><span class="sxs-lookup"><span data-stu-id="2bd73-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="2bd73-108">Il est disponible pour tous types de machines virtuelles Azure, notamment PaaS et IaaS.</span><span class="sxs-lookup"><span data-stu-id="2bd73-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="2bd73-109">Les événements planifiés donne à vos tâches de prévention tooperform de temps Machine virtuelle que hello toominimize un événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="2bd73-110">Le sous-service des événements planifiés est disponible pour les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="2bd73-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="2bd73-111">Pour plus d’informations sur les événements planifiés sur Windows, consultez [Événements planifiés pour les machines virtuelles Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="2bd73-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="2bd73-112">Pourquoi choisir les événements planifiés ?</span><span class="sxs-lookup"><span data-stu-id="2bd73-112">Why Scheduled Events?</span></span>

<span data-ttu-id="2bd73-113">Les événements planifiés, vous pouvez suivre des étapes impact de hello toolimit de maintenance de la plateforme-intiated ou des actions effectuées par l’utilisateur sur votre service.</span><span class="sxs-lookup"><span data-stu-id="2bd73-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="2bd73-114">Les charges de travail à plusieurs instances, qui utilisent l’état de réplication techniques toomaintain, peuvent être vulnérables toooutages se produit sur plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="2bd73-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="2bd73-115">Ces pannes peuvent entraîner de tâches coûteuses (par exemple, la reconstruction des index) ou même une perte de réplica.</span><span class="sxs-lookup"><span data-stu-id="2bd73-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="2bd73-116">Dans de nombreux autres cas, hello globale disponibilité du service peut être améliorée en effectuant une séquence d’arrêt approprié comme fin (ou annulation) les transactions en cours, en réaffectant des tâches tooother machines virtuelles dans le cluster hello (manuel de basculement), ou la suppression de hello Machine virtuelle à partir d’un pool d’équilibrage de charge réseau.</span><span class="sxs-lookup"><span data-stu-id="2bd73-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="2bd73-117">Il existe des cas où notifiant un administrateur sur un événement à venir ou de journalisation d’un tel événement aider à améliorer la facilité de maintenance de hello des applications hébergées dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="2bd73-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="2bd73-118">Cas d’usage Azure Metadata Service surfaces événements planifiés suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="2bd73-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="2bd73-119">La plateforme a lancé une maintenance (par exemple, le déploiement du système d’exploitation hôte)</span><span class="sxs-lookup"><span data-stu-id="2bd73-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="2bd73-120">L’utilisateur a lancé des appels (par exemple, un utilisateur redémarre ou redéploie une machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="2bd73-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="2bd73-121">principes de base Hello</span><span class="sxs-lookup"><span data-stu-id="2bd73-121">hello basics</span></span>  

<span data-ttu-id="2bd73-122">Service de métadonnées Azure expose des informations sur les ordinateurs virtuels à l’aide d’un point de terminaison reste accessible à partir de hello machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2bd73-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="2bd73-123">informations de Hello sont disponibles via une adresse IP non routable afin que n’est pas exposée à l’extérieur de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2bd73-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="2bd73-124">Scope</span><span class="sxs-lookup"><span data-stu-id="2bd73-124">Scope</span></span>
<span data-ttu-id="2bd73-125">Les événements planifiés sont tooall chaque bande les ordinateurs virtuels dans un service cloud ou tooall Machines virtuelles dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2bd73-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="2bd73-126">Par conséquent, vous devez vérifier hello `Resources` champ tooidentify d’événement hello qui machines virtuelles vont toobe concerné.</span><span class="sxs-lookup"><span data-stu-id="2bd73-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="2bd73-127">Découverte de point de terminaison hello</span><span class="sxs-lookup"><span data-stu-id="2bd73-127">Discovering hello endpoint</span></span>
<span data-ttu-id="2bd73-128">Dans les cas de hello où un ordinateur virtuel est créé dans un réseau virtuel (VNet), service de métadonnées hello est disponible à partir d’une adresse IP non routable statique, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="2bd73-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="2bd73-129">Si hello Machine virtuelle n’est pas créé dans un réseau virtuel, le cas par défaut de hello pour les services de cloud computing et machines virtuelles de classiques, une logique supplémentaire est toouse de point de terminaison hello toodiscover requis.</span><span class="sxs-lookup"><span data-stu-id="2bd73-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="2bd73-130">Consultez Comment trop de toothis exemple toolearn[découvrir le point de terminaison hello hôte](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="2bd73-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="2bd73-131">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="2bd73-131">Versioning</span></span> 
<span data-ttu-id="2bd73-132">Hello Service de métadonnées de l’Instance est créée.</span><span class="sxs-lookup"><span data-stu-id="2bd73-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="2bd73-133">Les versions sont obligatoires et la version actuelle de hello est `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="2bd73-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bd73-134">Versions précédentes de l’aperçu des événements planifiés pris en charge {dernière} en tant que version d’api hello.</span><span class="sxs-lookup"><span data-stu-id="2bd73-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="2bd73-135">Ce format n’est plus pris en charge et sera déconseillé dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="2bd73-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="2bd73-136">Utilisation d’en-têtes</span><span class="sxs-lookup"><span data-stu-id="2bd73-136">Using headers</span></span>
<span data-ttu-id="2bd73-137">Lorsque vous interrogez hello Metadata Service, vous devez fournir l’en-tête de hello `Metadata: true` demande de hello tooensure n’a pas été redirigée involontairement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="2bd73-138">Activation des événements planifiés</span><span class="sxs-lookup"><span data-stu-id="2bd73-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="2bd73-139">Hello première fois que vous faites une demande pour les événements planifiés, Azure Active implicitement la fonction hello sur votre Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2bd73-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="2bd73-140">Par conséquent, attendez-vous à retarder la réponse de votre premier appel de haut tootwo minutes.</span><span class="sxs-lookup"><span data-stu-id="2bd73-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="2bd73-141">Maintenance initiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2bd73-141">User initiated maintenance</span></span>
<span data-ttu-id="2bd73-142">Maintenance des ordinateurs virtuels via hello portail Azure, API, CLI, initiée par l’utilisateur ou de PowerShell entraîne un événement planifié.</span><span class="sxs-lookup"><span data-stu-id="2bd73-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="2bd73-143">Cela vous permet de logique de préparation maintenance tootest hello dans votre application et tooprepare de votre application pour une maintenance initiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2bd73-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="2bd73-144">Le redémarrage d’une machine virtuelle planifie un événement de type `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="2bd73-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="2bd73-145">Le redéploiement d’une machine virtuelle planifie un événement de type `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="2bd73-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bd73-146">Actuellement, 10 opérations maximum de maintenance initiée par l’utilisateur peuvent être planifiées simultanément.</span><span class="sxs-lookup"><span data-stu-id="2bd73-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="2bd73-147">Cette limite sera assouplie avant la disponibilité générale des Événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="2bd73-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bd73-148">Actuellement, la maintenance initiée par l’utilisateur qui résulte dans des Événements planifiés n’est pas configurable.</span><span class="sxs-lookup"><span data-stu-id="2bd73-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="2bd73-149">La possibilité de configuration est prévue pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2bd73-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="2bd73-150">À l’aide des API de hello</span><span class="sxs-lookup"><span data-stu-id="2bd73-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="2bd73-151">Rechercher des événements</span><span class="sxs-lookup"><span data-stu-id="2bd73-151">Query for events</span></span>
<span data-ttu-id="2bd73-152">Vous pouvez rechercher les événements planifiés simplement en effectuant les hello suivant à appeler :</span><span class="sxs-lookup"><span data-stu-id="2bd73-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="2bd73-153">Une réponse contient un tableau d’événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="2bd73-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="2bd73-154">Un tableau vide signifie qu’il n’y a actuellement aucun événement planifié.</span><span class="sxs-lookup"><span data-stu-id="2bd73-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="2bd73-155">Dans le cas de hello où il existe les événements planifiés, réponse de hello contient un tableau d’événements :</span><span class="sxs-lookup"><span data-stu-id="2bd73-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="2bd73-156">Propriétés d’événement</span><span class="sxs-lookup"><span data-stu-id="2bd73-156">Event properties</span></span>
|<span data-ttu-id="2bd73-157">Propriété</span><span class="sxs-lookup"><span data-stu-id="2bd73-157">Property</span></span>  |  <span data-ttu-id="2bd73-158">Description</span><span class="sxs-lookup"><span data-stu-id="2bd73-158">Description</span></span> |
| - | - |
| <span data-ttu-id="2bd73-159">EventId</span><span class="sxs-lookup"><span data-stu-id="2bd73-159">EventId</span></span> | <span data-ttu-id="2bd73-160">GUID pour cet événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="2bd73-161">Exemple :</span><span class="sxs-lookup"><span data-stu-id="2bd73-161">Example:</span></span> <br><ul><li><span data-ttu-id="2bd73-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="2bd73-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="2bd73-163">EventType</span><span class="sxs-lookup"><span data-stu-id="2bd73-163">EventType</span></span> | <span data-ttu-id="2bd73-164">Impact provoqué par cet événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="2bd73-165">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="2bd73-165">Values:</span></span> <br><ul><li> <span data-ttu-id="2bd73-166">`Freeze`: hello Machine virtuelle est planifiée toopause pendant quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="2bd73-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="2bd73-167">Hello du processeur est suspendue, mais il n’existe aucun impact sur la mémoire, les fichiers ouverts ou les connexions réseau.</span><span class="sxs-lookup"><span data-stu-id="2bd73-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="2bd73-168">`Reboot`: hello Machine virtuelle est planifiée pour le redémarrage (mémoire non persistant est perdu).</span><span class="sxs-lookup"><span data-stu-id="2bd73-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="2bd73-169">`Redeploy`: hello Machine virtuelle est planifiée toomove tooanother nœud (disques éphémères sont perdues).</span><span class="sxs-lookup"><span data-stu-id="2bd73-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="2bd73-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="2bd73-170">ResourceType</span></span> | <span data-ttu-id="2bd73-171">Type de ressource affecté par cet événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="2bd73-172">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="2bd73-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="2bd73-173">Ressources</span><span class="sxs-lookup"><span data-stu-id="2bd73-173">Resources</span></span>| <span data-ttu-id="2bd73-174">Liste des ressources affectées par cet événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-174">List of resources this event impacts.</span></span> <span data-ttu-id="2bd73-175">Cela est assurée au plus un toocontain machines [domaine de mise à jour](manage-availability.md), mais ne peut ne pas contenir toutes les machines de hello UD.</span><span class="sxs-lookup"><span data-stu-id="2bd73-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="2bd73-176">Exemple :</span><span class="sxs-lookup"><span data-stu-id="2bd73-176">Example:</span></span> <br><ul><li> <span data-ttu-id="2bd73-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="2bd73-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="2bd73-178">Event Status</span><span class="sxs-lookup"><span data-stu-id="2bd73-178">Event Status</span></span> | <span data-ttu-id="2bd73-179">État de cet événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-179">Status of this event.</span></span> <br><br> <span data-ttu-id="2bd73-180">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="2bd73-180">Values:</span></span> <ul><li><span data-ttu-id="2bd73-181">`Scheduled`: Cet événement est planifiée toostart tard hello spécifié dans hello `NotBefore` propriété.</span><span class="sxs-lookup"><span data-stu-id="2bd73-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="2bd73-182">`Started` : cet événement a démarré.</span><span class="sxs-lookup"><span data-stu-id="2bd73-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="2bd73-183">Ne `Completed` ou état similaire est déjà fourni ; les événements hello seront n’est plus renvoyée lors de l’événement de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="2bd73-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="2bd73-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="2bd73-184">NotBefore</span></span>| <span data-ttu-id="2bd73-185">Heure après laquelle cet événement peut démarrer.</span><span class="sxs-lookup"><span data-stu-id="2bd73-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="2bd73-186">Exemple :</span><span class="sxs-lookup"><span data-stu-id="2bd73-186">Example:</span></span> <br><ul><li> <span data-ttu-id="2bd73-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="2bd73-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="2bd73-188">Planification d’événement</span><span class="sxs-lookup"><span data-stu-id="2bd73-188">Event scheduling</span></span>
<span data-ttu-id="2bd73-189">Chaque événement est planifié une quantité minimale de temps Bonjour futures basé sur le type d’événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="2bd73-190">Cette heure est reflétée dans la propriété `NotBefore` d’un événement.</span><span class="sxs-lookup"><span data-stu-id="2bd73-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="2bd73-191">EventType</span><span class="sxs-lookup"><span data-stu-id="2bd73-191">EventType</span></span>  | <span data-ttu-id="2bd73-192">Préavis minimal</span><span class="sxs-lookup"><span data-stu-id="2bd73-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="2bd73-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="2bd73-193">Freeze</span></span>| <span data-ttu-id="2bd73-194">15 minutes</span><span class="sxs-lookup"><span data-stu-id="2bd73-194">15 minutes</span></span> |
| <span data-ttu-id="2bd73-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="2bd73-195">Reboot</span></span> | <span data-ttu-id="2bd73-196">15 minutes</span><span class="sxs-lookup"><span data-stu-id="2bd73-196">15 minutes</span></span> |
| <span data-ttu-id="2bd73-197">Redeploy</span><span class="sxs-lookup"><span data-stu-id="2bd73-197">Redeploy</span></span> | <span data-ttu-id="2bd73-198">10 minutes</span><span class="sxs-lookup"><span data-stu-id="2bd73-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="2bd73-199">Démarrage d’un événement</span><span class="sxs-lookup"><span data-stu-id="2bd73-199">Starting an event</span></span> 

<span data-ttu-id="2bd73-200">Une fois que vous avez appris d’un événement à venir et terminé votre logique pour l’arrêt approprié, vous pouvez approuver les événements en attente hello en effectuant un `POST` appeler le service de métadonnées toohello avec hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="2bd73-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="2bd73-201">Cela indique tooAzure qu’il peut raccourcir la notification de minimale hello heure (si possible).</span><span class="sxs-lookup"><span data-stu-id="2bd73-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="2bd73-202">Accuse réception d’un événement permet de hello événement tooproceed pour tous les `Resources` dans l’événement de hello, pas seulement hello machine virtuelle qui accuse réception des événements de hello.</span><span class="sxs-lookup"><span data-stu-id="2bd73-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="2bd73-203">Vous pouvez donc choisir tooelect un leader toocoordinate hello accusé de réception, ce qui peut être aussi simple que la première machine de hello Bonjour `Resources` champ.</span><span class="sxs-lookup"><span data-stu-id="2bd73-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="2bd73-204">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="2bd73-204">Python sample</span></span> 

<span data-ttu-id="2bd73-205">Hello exemples de requêtes suivants hello du service de métadonnées pour les événements planifiés et approuve chaque événement en attente.</span><span class="sxs-lookup"><span data-stu-id="2bd73-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2bd73-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bd73-206">Next steps</span></span> 

- <span data-ttu-id="2bd73-207">En savoir plus sur les API disponibles dans hello de hello [service de métadonnées de l’Instance](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="2bd73-207">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="2bd73-208">Découvrez plus d’informations sur la [maintenance planifiée pour les machines virtuelles Linux dans Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="2bd73-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
