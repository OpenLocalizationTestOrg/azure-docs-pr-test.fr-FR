---
title: "aaaScheduled événements avec le Service de métadonnées Azure | Documents Microsoft"
description: "Réagir tooImpactful événements sur votre Machine virtuelle avant qu’ils surviennent."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="d4756-103">Service de métadonnées Azure - Événements planifiés (préversion)</span><span class="sxs-lookup"><span data-stu-id="d4756-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="d4756-104">Aperçus deviennent tooyou disponible sur condition hello que vous acceptez les conditions d’utilisation de toohello.</span><span class="sxs-lookup"><span data-stu-id="d4756-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="d4756-105">Pour plus d’informations, consultez [Conditions d’Utilisation Supplémentaires relatives aux Évaluations Microsoft Azure](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="d4756-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="d4756-106">Les événements planifiés est un des sous-Services hello sous hello Azure métadonnées de Service.</span><span class="sxs-lookup"><span data-stu-id="d4756-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="d4756-107">Ce sous-service est responsable de la mise à disposition des informations concernant les événements à venir (par exemple un redémarrage), pour que votre application puisse s’y préparer et limiter ainsi l’interruption.</span><span class="sxs-lookup"><span data-stu-id="d4756-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="d4756-108">Il est disponible pour tous types de machines virtuelles Azure, notamment PaaS et IaaS.</span><span class="sxs-lookup"><span data-stu-id="d4756-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="d4756-109">Les événements planifiés donne à vos tâches de prévention tooperform de temps Machine virtuelle que hello toominimize un événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="d4756-110">Introduction - Pourquoi utiliser Événements planifiés ?</span><span class="sxs-lookup"><span data-stu-id="d4756-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="d4756-111">Les événements planifiés, vous pouvez suivre des étapes impact de hello toolimit de maintenance de la plateforme-intiated ou des actions effectuées par l’utilisateur sur votre service.</span><span class="sxs-lookup"><span data-stu-id="d4756-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="d4756-112">Les charges de travail à plusieurs instances, qui utilisent l’état de réplication techniques toomaintain, peuvent être vulnérables toooutages se produit sur plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="d4756-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="d4756-113">Ces pannes peuvent entraîner de tâches coûteuses (par exemple, la reconstruction des index) ou même une perte de réplica.</span><span class="sxs-lookup"><span data-stu-id="d4756-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="d4756-114">Dans de nombreux autres cas, hello globale disponibilité du service peut être améliorée en effectuant une séquence d’arrêt approprié comme fin (ou annulation) les transactions en cours, en réaffectant des tâches tooother machines virtuelles dans le cluster hello (manuel de basculement), ou la suppression de hello Machine virtuelle à partir d’un pool d’équilibrage de charge réseau.</span><span class="sxs-lookup"><span data-stu-id="d4756-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="d4756-115">Il existe des cas où notifiant un administrateur sur un événement à venir ou de journalisation d’un tel événement aider à améliorer la facilité de maintenance de hello des applications hébergées dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d4756-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="d4756-116">Cas d’usage Azure Metadata Service surfaces événements planifiés suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="d4756-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="d4756-117">La plateforme a lancé une maintenance (par exemple, le déploiement du système d’exploitation hôte)</span><span class="sxs-lookup"><span data-stu-id="d4756-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="d4756-118">L’utilisateur a lancé des appels (par exemple, un utilisateur redémarre ou redéploie une machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="d4756-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="d4756-119">Événements planifiés - hello notions de base</span><span class="sxs-lookup"><span data-stu-id="d4756-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="d4756-120">Service de métadonnées Azure expose des informations sur les ordinateurs virtuels à l’aide d’un point de terminaison reste accessible à partir de hello machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d4756-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="d4756-121">informations de Hello sont disponibles via une adresse IP non routable afin que n’est pas exposée à l’extérieur de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4756-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="d4756-122">Scope</span><span class="sxs-lookup"><span data-stu-id="d4756-122">Scope</span></span>
<span data-ttu-id="d4756-123">Les événements planifiés sont tooall chaque bande les ordinateurs virtuels dans un service cloud ou tooall Machines virtuelles dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d4756-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="d4756-124">Par conséquent, vous devez vérifier hello `Resources` champ tooidentify d’événement hello qui machines virtuelles vont toobe concerné.</span><span class="sxs-lookup"><span data-stu-id="d4756-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="d4756-125">Hello point de terminaison de découverte</span><span class="sxs-lookup"><span data-stu-id="d4756-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="d4756-126">Dans les cas de hello où un ordinateur virtuel est créé dans un réseau virtuel (VNet), service de métadonnées hello est disponible à partir d’une adresse IP non routable statique, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="d4756-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="d4756-127">Si hello Machine virtuelle n’est pas créé dans un réseau virtuel, le cas par défaut de hello pour les services de cloud computing et machines virtuelles de classiques, une logique supplémentaire est toouse de point de terminaison hello toodiscover requis.</span><span class="sxs-lookup"><span data-stu-id="d4756-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="d4756-128">Consultez Comment trop de toothis exemple toolearn[découvrir le point de terminaison hello hôte](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="d4756-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="d4756-129">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="d4756-129">Versioning</span></span> 
<span data-ttu-id="d4756-130">Hello Service de métadonnées de l’Instance est créée.</span><span class="sxs-lookup"><span data-stu-id="d4756-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="d4756-131">Les versions sont obligatoires et la version actuelle de hello est `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="d4756-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d4756-132">Versions précédentes de l’aperçu des événements planifiés pris en charge {dernière} en tant que version d’api hello.</span><span class="sxs-lookup"><span data-stu-id="d4756-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="d4756-133">Ce format n’est plus pris en charge et sera déconseillé dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="d4756-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="d4756-134">Utilisation d'en-têtes</span><span class="sxs-lookup"><span data-stu-id="d4756-134">Using Headers</span></span>
<span data-ttu-id="d4756-135">Lorsque vous interrogez hello Metadata Service, vous devez fournir l’en-tête de hello `Metadata: true` demande de hello tooensure n’a pas été redirigée involontairement.</span><span class="sxs-lookup"><span data-stu-id="d4756-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="d4756-136">Activation des événements planifiés</span><span class="sxs-lookup"><span data-stu-id="d4756-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="d4756-137">Hello première fois que vous faites une demande pour les événements planifiés, Azure Active implicitement la fonction hello sur votre Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4756-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="d4756-138">Par conséquent, attendez-vous à retarder la réponse de votre premier appel de haut tootwo minutes.</span><span class="sxs-lookup"><span data-stu-id="d4756-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="d4756-139">Maintenance initiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d4756-139">User Initiated Maintenance</span></span>
<span data-ttu-id="d4756-140">Maintenance des ordinateurs virtuels via hello portail Azure, API, CLI, initiée par l’utilisateur ou de PowerShell entraîne des événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="d4756-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="d4756-141">Cela vous permet de logique de préparation maintenance tootest hello dans votre application et tooprepare de votre application pour une maintenance initiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d4756-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="d4756-142">Le redémarrage d’une machine virtuelle planifie un événement de type `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="d4756-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="d4756-143">Le redéploiement d’une machine virtuelle planifie un événement de type `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="d4756-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d4756-144">Actuellement, 10 opérations maximum de maintenance initiée par l’utilisateur peuvent être planifiées simultanément.</span><span class="sxs-lookup"><span data-stu-id="d4756-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="d4756-145">Cette limite sera assouplie avant la disponibilité générale des Événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="d4756-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="d4756-146">Actuellement, la maintenance initiée par l’utilisateur qui résulte dans des Événements planifiés n’est pas configurable.</span><span class="sxs-lookup"><span data-stu-id="d4756-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="d4756-147">La possibilité de configuration est prévue pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d4756-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="d4756-148">À l’aide des API de hello</span><span class="sxs-lookup"><span data-stu-id="d4756-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="d4756-149">Rechercher des événements</span><span class="sxs-lookup"><span data-stu-id="d4756-149">Query for events</span></span>
<span data-ttu-id="d4756-150">Vous pouvez rechercher les événements planifiés simplement en effectuant les hello suivant à appeler :</span><span class="sxs-lookup"><span data-stu-id="d4756-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="d4756-151">Une réponse contient un tableau d’événements planifiés.</span><span class="sxs-lookup"><span data-stu-id="d4756-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="d4756-152">Un tableau vide signifie qu’il n’y a actuellement aucun événement planifié.</span><span class="sxs-lookup"><span data-stu-id="d4756-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="d4756-153">Dans le cas de hello où il existe les événements planifiés, réponse de hello contient un tableau d’événements :</span><span class="sxs-lookup"><span data-stu-id="d4756-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="d4756-154">Propriétés de l’événement</span><span class="sxs-lookup"><span data-stu-id="d4756-154">Event Properties</span></span>
|<span data-ttu-id="d4756-155">Propriété</span><span class="sxs-lookup"><span data-stu-id="d4756-155">Property</span></span>  |  <span data-ttu-id="d4756-156">Description</span><span class="sxs-lookup"><span data-stu-id="d4756-156">Description</span></span> |
| - | - |
| <span data-ttu-id="d4756-157">EventId</span><span class="sxs-lookup"><span data-stu-id="d4756-157">EventId</span></span> | <span data-ttu-id="d4756-158">GUID pour cet événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="d4756-159">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d4756-159">Example:</span></span> <br><ul><li><span data-ttu-id="d4756-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="d4756-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="d4756-161">EventType</span><span class="sxs-lookup"><span data-stu-id="d4756-161">EventType</span></span> | <span data-ttu-id="d4756-162">Impact provoqué par cet événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="d4756-163">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="d4756-163">Values:</span></span> <br><ul><li> <span data-ttu-id="d4756-164">`Freeze`: hello Machine virtuelle est planifiée toopause pendant quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="d4756-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="d4756-165">Hello du processeur est suspendu, mais il n’existe aucun impact sur la mémoire, les fichiers ouverts ou les connexions réseau.</span><span class="sxs-lookup"><span data-stu-id="d4756-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="d4756-166">`Reboot`: hello Machine virtuelle est planifiée pour le redémarrage (mémoire non persistant est perdu).</span><span class="sxs-lookup"><span data-stu-id="d4756-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="d4756-167">`Redeploy`: hello Machine virtuelle est planifiée toomove tooanother nœud (disques éphémères sont perdues).</span><span class="sxs-lookup"><span data-stu-id="d4756-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="d4756-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d4756-168">ResourceType</span></span> | <span data-ttu-id="d4756-169">Type de ressource affecté par cet événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="d4756-170">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="d4756-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="d4756-171">Ressources</span><span class="sxs-lookup"><span data-stu-id="d4756-171">Resources</span></span>| <span data-ttu-id="d4756-172">Liste des ressources affectées par cet événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-172">List of resources this event impacts.</span></span> <span data-ttu-id="d4756-173">Cela est assurée au plus un toocontain machines [domaine de mise à jour](windows/manage-availability.md), mais ne peut ne pas contenir toutes les machines de hello UD.</span><span class="sxs-lookup"><span data-stu-id="d4756-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="d4756-174">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d4756-174">Example:</span></span> <br><ul><li> <span data-ttu-id="d4756-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="d4756-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="d4756-176">Event Status</span><span class="sxs-lookup"><span data-stu-id="d4756-176">Event Status</span></span> | <span data-ttu-id="d4756-177">État de cet événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-177">Status of this event.</span></span> <br><br> <span data-ttu-id="d4756-178">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="d4756-178">Values:</span></span> <ul><li><span data-ttu-id="d4756-179">`Scheduled`: Cet événement est planifiée toostart tard hello spécifié dans hello `NotBefore` propriété.</span><span class="sxs-lookup"><span data-stu-id="d4756-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="d4756-180">`Started` : cet événement a démarré.</span><span class="sxs-lookup"><span data-stu-id="d4756-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="d4756-181">Ne `Completed` ou état similaire est déjà fourni ; les événements hello seront n’est plus renvoyée lors de l’événement de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="d4756-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="d4756-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="d4756-182">NotBefore</span></span>| <span data-ttu-id="d4756-183">Heure après laquelle cet événement peut démarrer.</span><span class="sxs-lookup"><span data-stu-id="d4756-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="d4756-184">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d4756-184">Example:</span></span> <br><ul><li> <span data-ttu-id="d4756-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="d4756-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="d4756-186">Planification d’événement</span><span class="sxs-lookup"><span data-stu-id="d4756-186">Event Scheduling</span></span>
<span data-ttu-id="d4756-187">Chaque événement est planifié une quantité minimale de temps Bonjour futures basé sur le type d’événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="d4756-188">Cette heure est reflétée dans la propriété `NotBefore` d’un événement.</span><span class="sxs-lookup"><span data-stu-id="d4756-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="d4756-189">EventType</span><span class="sxs-lookup"><span data-stu-id="d4756-189">EventType</span></span>  | <span data-ttu-id="d4756-190">Préavis minimal</span><span class="sxs-lookup"><span data-stu-id="d4756-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="d4756-191">Freeze</span><span class="sxs-lookup"><span data-stu-id="d4756-191">Freeze</span></span>| <span data-ttu-id="d4756-192">15 minutes</span><span class="sxs-lookup"><span data-stu-id="d4756-192">15 minutes</span></span> |
| <span data-ttu-id="d4756-193">Reboot</span><span class="sxs-lookup"><span data-stu-id="d4756-193">Reboot</span></span> | <span data-ttu-id="d4756-194">15 minutes</span><span class="sxs-lookup"><span data-stu-id="d4756-194">15 minutes</span></span> |
| <span data-ttu-id="d4756-195">Redeploy</span><span class="sxs-lookup"><span data-stu-id="d4756-195">Redeploy</span></span> | <span data-ttu-id="d4756-196">10 minutes</span><span class="sxs-lookup"><span data-stu-id="d4756-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="d4756-197">Démarrage d’un événement (accélérer)</span><span class="sxs-lookup"><span data-stu-id="d4756-197">Starting an event (expedite)</span></span>

<span data-ttu-id="d4756-198">Une fois que vous avez appris d’un événement à venir et terminé votre logique pour l’arrêt approprié, vous pouvez approuver les événements en attente hello en effectuant un `POST` appeler le service de métadonnées toohello avec hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="d4756-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="d4756-199">Cela indique tooAzure qu’il peut raccourcir la notification de minimale hello heure (si possible).</span><span class="sxs-lookup"><span data-stu-id="d4756-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="d4756-200">Accuse réception d’un événement permettra hello événement tooproceed à tous les `Resources` dans l’événement de hello, pas seulement hello machine virtuelle qui accuse réception des événements de hello.</span><span class="sxs-lookup"><span data-stu-id="d4756-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="d4756-201">Vous pouvez donc choisir tooelect un leader toocoordinate hello accusé de réception, ce qui peut être aussi simple que la première machine de hello Bonjour `Resources` champ.</span><span class="sxs-lookup"><span data-stu-id="d4756-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="d4756-202">Exemples</span><span class="sxs-lookup"><span data-stu-id="d4756-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="d4756-203">Exemple de code PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4756-203">PowerShell Sample</span></span> 

<span data-ttu-id="d4756-204">Hello exemples de requêtes suivants hello du service de métadonnées pour les événements planifiés et approuve chaque événement en attente.</span><span class="sxs-lookup"><span data-stu-id="d4756-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


### <a name="c-sample"></a><span data-ttu-id="d4756-205">Exemple de code C\#</span><span class="sxs-lookup"><span data-stu-id="d4756-205">C\# Sample</span></span> 

<span data-ttu-id="d4756-206">Hello exemple suivant est un simple client qui communique avec le service de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="d4756-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="d4756-207">Les événements planifiés peuvent être représentées à l’aide de hello suivant des structures de données :</span><span class="sxs-lookup"><span data-stu-id="d4756-207">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="d4756-208">Hello exemples de requêtes suivants hello du service de métadonnées pour les événements planifiés et approuve chaque événement en attente.</span><span class="sxs-lookup"><span data-stu-id="d4756-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

### <a name="python-sample"></a><span data-ttu-id="d4756-209">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="d4756-209">Python Sample</span></span> 

<span data-ttu-id="d4756-210">Hello exemples de requêtes suivants hello du service de métadonnées pour les événements planifiés et approuve chaque événement en attente.</span><span class="sxs-lookup"><span data-stu-id="d4756-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d4756-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4756-211">Next Steps</span></span> 

- <span data-ttu-id="d4756-212">En savoir plus sur les API disponibles dans hello de hello [service de métadonnées de l’instance](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4756-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="d4756-213">Découvrez plus d’informations sur la [maintenance planifiée pour les machines virtuelles Windows dans Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="d4756-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="d4756-214">Découvrez plus d’informations sur la [maintenance planifiée pour les machines virtuelles Linux dans Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="d4756-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
