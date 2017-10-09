---
title: aaaConvert toomicroservices des applications de Services de cloud computing Azure | Documents Microsoft
description: "Ce guide compare Web des Services de Cloud et rôles de travail et l’infrastructure de Service sans état services toohelp migrent à partir des Services de cloud computing tooService l’ensemble fibre optique."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="b73dc-103">Guide tooconverting rôles Web et Worker tooService sans état services de Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="b73dc-104">Cet article décrit comment toomigrate votre Web des Services de Cloud et les rôles de travail tooService sans état services de Fabric.</span><span class="sxs-lookup"><span data-stu-id="b73dc-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="b73dc-105">Il s’agit de hello la plus simple de migration à partir des Services de cloud computing tooService l’infrastructure pour les applications dont l’architecture globale est en train de toostay à peu près hello identiques.</span><span class="sxs-lookup"><span data-stu-id="b73dc-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="b73dc-106">Projet d’application de Service project tooService l’infrastructure de cloud computing</span><span class="sxs-lookup"><span data-stu-id="b73dc-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="b73dc-107">Un projet de Service Cloud et un projet d’Application de l’infrastructure de Service ont une structure similaire et les deux unités de déploiement représentent hello pour votre application : autrement dit, elles définissent complète hello est toorun déployé votre application.</span><span class="sxs-lookup"><span data-stu-id="b73dc-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="b73dc-108">Un projet de service cloud contient un ou plusieurs rôles web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="b73dc-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="b73dc-109">De la même façon, un projet d’application Service Fabric regroupe un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="b73dc-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="b73dc-110">Hello différence est que couples de projet de Service Cloud hello hello du déploiement d’applications avec un déploiement de machine virtuelle et contient donc les paramètres de configuration de machine virtuelle, tandis que le projet d’Application Service Fabric hello définit seulement une application qui sera déployée tooa l’ensemble des machines virtuelles existantes dans un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b73dc-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="b73dc-111">cluster Service Fabric de Hello lui-même est uniquement déployé une fois, via un modèle de gestionnaire de ressources ou via hello portail Azure et plusieurs Service Fabric, les applications peuvent être déploiement tooit.</span><span class="sxs-lookup"><span data-stu-id="b73dc-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Comparaison de projet entre Service Fabric et les services cloud][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="b73dc-113">Service de toostateless de rôle de travail</span><span class="sxs-lookup"><span data-stu-id="b73dc-113">Worker Role toostateless service</span></span>
<span data-ttu-id="b73dc-114">Point de vue conceptuel, un rôle de travail représente une charge de travail sans état, ce qui signifie que chaque instance de la charge de travail hello est identique et de requêtes peuvent être routé tooany instance à tout moment.</span><span class="sxs-lookup"><span data-stu-id="b73dc-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="b73dc-115">Chaque instance n’est pas demande précédente de hello tooremember attendu.</span><span class="sxs-lookup"><span data-stu-id="b73dc-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="b73dc-116">État de cette charge de travail hello opère sur est géré par un magasin d’état externe, telles que le stockage Azure Table ou de la base de données de Document Azure.</span><span class="sxs-lookup"><span data-stu-id="b73dc-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="b73dc-117">Dans Service Fabric, ce type de charge de travail est représenté par un service sans état.</span><span class="sxs-lookup"><span data-stu-id="b73dc-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="b73dc-118">Hello toomigrating d’approche la plus simple un tooService de rôle de travail Fabric est possible en convertissant le rôle de travail code tooa Service sans état.</span><span class="sxs-lookup"><span data-stu-id="b73dc-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![Rôle de travail tooStateless Service][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="b73dc-120">Rôle toostateless service Web</span><span class="sxs-lookup"><span data-stu-id="b73dc-120">Web Role toostateless service</span></span>
<span data-ttu-id="b73dc-121">TooWorker similaire rôle, un rôle Web représente également une charge de travail sans état, et donc conceptuellement il peut aussi être mappé tooa service sans état du Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b73dc-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="b73dc-122">Toutefois, contrairement aux rôles web, Service Fabric ne prend pas en charge les IIS.</span><span class="sxs-lookup"><span data-stu-id="b73dc-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="b73dc-123">toomigrate une application web à partir d’un service sans état tooa de rôle Web nécessite la première infrastructure web tooa mobile qui permettre être auto-hébergés et ne dépend pas d’IIS ou System.Web, telles que ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="b73dc-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="b73dc-124">**Application**</span><span class="sxs-lookup"><span data-stu-id="b73dc-124">**Application**</span></span> | <span data-ttu-id="b73dc-125">**Pris en charge**</span><span class="sxs-lookup"><span data-stu-id="b73dc-125">**Supported**</span></span> | <span data-ttu-id="b73dc-126">**Chemin de migration**</span><span class="sxs-lookup"><span data-stu-id="b73dc-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b73dc-127">Formulaires web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b73dc-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="b73dc-128">Non</span><span class="sxs-lookup"><span data-stu-id="b73dc-128">No</span></span> |<span data-ttu-id="b73dc-129">Convertir tooASP.NET 1 MVC de base</span><span class="sxs-lookup"><span data-stu-id="b73dc-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="b73dc-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b73dc-130">ASP.NET MVC</span></span> |<span data-ttu-id="b73dc-131">Avec migration</span><span class="sxs-lookup"><span data-stu-id="b73dc-131">With Migration</span></span> |<span data-ttu-id="b73dc-132">TooASP.NET mise à niveau de base 1 MVC</span><span class="sxs-lookup"><span data-stu-id="b73dc-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="b73dc-133">API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b73dc-133">ASP.NET Web API</span></span> |<span data-ttu-id="b73dc-134">Avec migration</span><span class="sxs-lookup"><span data-stu-id="b73dc-134">With Migration</span></span> |<span data-ttu-id="b73dc-135">Utiliser un serveur auto-hébergé ou ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="b73dc-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="b73dc-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="b73dc-136">ASP.NET Core 1</span></span> |<span data-ttu-id="b73dc-137">Oui</span><span class="sxs-lookup"><span data-stu-id="b73dc-137">Yes</span></span> |<span data-ttu-id="b73dc-138">N/A</span><span class="sxs-lookup"><span data-stu-id="b73dc-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="b73dc-139">API de point d’entrée et cycle de vie</span><span class="sxs-lookup"><span data-stu-id="b73dc-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="b73dc-140">Les points d’entrée des API de rôle de travail et de Service Fabric sont semblables :</span><span class="sxs-lookup"><span data-stu-id="b73dc-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="b73dc-141">**Point d’entrée**</span><span class="sxs-lookup"><span data-stu-id="b73dc-141">**Entry Point**</span></span> | <span data-ttu-id="b73dc-142">**Instances de**</span><span class="sxs-lookup"><span data-stu-id="b73dc-142">**Worker Role**</span></span> | <span data-ttu-id="b73dc-143">**Service Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b73dc-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b73dc-144">Traitement en cours</span><span class="sxs-lookup"><span data-stu-id="b73dc-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="b73dc-145">Démarrer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b73dc-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="b73dc-146">N/A</span><span class="sxs-lookup"><span data-stu-id="b73dc-146">N/A</span></span> |
| <span data-ttu-id="b73dc-147">Arrêter la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b73dc-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="b73dc-148">N/A</span><span class="sxs-lookup"><span data-stu-id="b73dc-148">N/A</span></span> |
| <span data-ttu-id="b73dc-149">Ouvrir l’écouteur pour les requêtes du client</span><span class="sxs-lookup"><span data-stu-id="b73dc-149">Open listener for client requests</span></span> |<span data-ttu-id="b73dc-150">N/A</span><span class="sxs-lookup"><span data-stu-id="b73dc-150">N/A</span></span> |<ul><li> <span data-ttu-id="b73dc-151">Sans état : `CreateServiceInstanceListener()`</span><span class="sxs-lookup"><span data-stu-id="b73dc-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="b73dc-152">Avec état : `CreateServiceReplicaListener()`</span><span class="sxs-lookup"><span data-stu-id="b73dc-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="b73dc-153">Instances de</span><span class="sxs-lookup"><span data-stu-id="b73dc-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="b73dc-154">Services sans état Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="b73dc-155">Dans lequel la transformation toobegin ont un remplacement principal « exécuter ».</span><span class="sxs-lookup"><span data-stu-id="b73dc-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="b73dc-156">Les services Service Fabric associent `Run`, `Start` et `Stop` en un point d’entrée unique, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="b73dc-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="b73dc-157">Votre service doit commencer à travailler lorsque `RunAsync` démarre et doit cesser de fonctionner lorsque hello `RunAsync` CancellationToken de la méthode est signalé.</span><span class="sxs-lookup"><span data-stu-id="b73dc-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="b73dc-158">Il existe plusieurs différences importantes entre hello du cycle de vie et la durée de vie des services de rôles de travail et l’infrastructure de Service :</span><span class="sxs-lookup"><span data-stu-id="b73dc-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="b73dc-159">**Cycle de vie :** plus grande différence de hello est qu’un rôle de travail est un ordinateur virtuel et par conséquent, leur cycle de vie est liée toohello machine virtuelle, qui inclut les événements de lorsque hello machine virtuelle démarre et arrête.</span><span class="sxs-lookup"><span data-stu-id="b73dc-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="b73dc-160">Un service Service Fabric a un cycle de vie qui est distinct de cycle de vie de machine virtuelle hello, donc il n’inclut pas les événements pour lorsque hello hôte des ordinateurs virtuels ou de démarrage de la machine et de fin, car elles ne sont pas liées.</span><span class="sxs-lookup"><span data-stu-id="b73dc-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="b73dc-161">**Durée de vie :** une instance de rôle de travail sera recyclé si hello `Run` issues de la méthode.</span><span class="sxs-lookup"><span data-stu-id="b73dc-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="b73dc-162">Hello `RunAsync` méthode dans un service Service Fabric toutefois peut s’exécuter toocompletion et reste de l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="b73dc-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="b73dc-163">Service Fabric fournit un point d’entrée de configuration de la communication en option pour les services qui écoutent les requêtes des clients.</span><span class="sxs-lookup"><span data-stu-id="b73dc-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="b73dc-164">Hello RunAsync et point d’entrée de communication sont des remplacements facultatif dans les services de l’infrastructure de Service - votre service peut choisir des demandes d’écoute tooclient tooonly, ou uniquement exécuter une boucle de traitement, ou les deux - c’est pourquoi hello RunAsync méthode est autorisée tooexit sans redémarrer l’instance de service de hello, car il peut continuer toolisten pour les demandes du client.</span><span class="sxs-lookup"><span data-stu-id="b73dc-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="b73dc-165">API d’application et environnement</span><span class="sxs-lookup"><span data-stu-id="b73dc-165">Application API and environment</span></span>
<span data-ttu-id="b73dc-166">environnement de Services de cloud computing Hello API fournit des informations et des fonctionnalités d’instance de machine virtuelle en cours hello, ainsi que des informations sur les autres instances de rôle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b73dc-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="b73dc-167">L’infrastructure de service fournit des informations connexes tooits runtime et des informations sur le nœud hello un service sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b73dc-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="b73dc-168">**Tâche d’environnement**</span><span class="sxs-lookup"><span data-stu-id="b73dc-168">**Environment Task**</span></span> | <span data-ttu-id="b73dc-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="b73dc-169">**Cloud Services**</span></span> | <span data-ttu-id="b73dc-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b73dc-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b73dc-171">Paramètres de configuration et notification de modification</span><span class="sxs-lookup"><span data-stu-id="b73dc-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="b73dc-172">Stockage local</span><span class="sxs-lookup"><span data-stu-id="b73dc-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="b73dc-173">Informations sur le point de terminaison</span><span class="sxs-lookup"><span data-stu-id="b73dc-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="b73dc-174">Instance actuelle : `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="b73dc-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="b73dc-175">Autres rôles et instances : `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="b73dc-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="b73dc-176">`NodeContext` pour l’adresse du nœud actuel</span><span class="sxs-lookup"><span data-stu-id="b73dc-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="b73dc-177">`FabricClient` et `ServicePartitionResolver` pour la découverte de point de terminaison de service</span><span class="sxs-lookup"><span data-stu-id="b73dc-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="b73dc-178">Émulation de l’environnement</span><span class="sxs-lookup"><span data-stu-id="b73dc-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="b73dc-179">N/A</span><span class="sxs-lookup"><span data-stu-id="b73dc-179">N/A</span></span> |
| <span data-ttu-id="b73dc-180">Événement de modification simultanée</span><span class="sxs-lookup"><span data-stu-id="b73dc-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="b73dc-181">N/A</span><span class="sxs-lookup"><span data-stu-id="b73dc-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="b73dc-182">Paramètres de configuration</span><span class="sxs-lookup"><span data-stu-id="b73dc-182">Configuration settings</span></span>
<span data-ttu-id="b73dc-183">Paramètres de configuration dans les Services de cloud computing sont définies pour un rôle d’ordinateur virtuel et appliquent tooall des instances de ce rôle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b73dc-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="b73dc-184">Ces paramètres correspondent à des paires clé-valeur définies dans les fichiers ServiceConfiguration.*.cscfg. Ils sont accessibles directement via RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="b73dc-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="b73dc-185">Dans l’infrastructure de Service, paramètres s’appliquent individuellement tooeach service et application de tooeach, plutôt que tooa machine virtuelle, car une machine virtuelle peut héberger plusieurs services et applications.</span><span class="sxs-lookup"><span data-stu-id="b73dc-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="b73dc-186">Un service se compose de trois packages :</span><span class="sxs-lookup"><span data-stu-id="b73dc-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="b73dc-187">**Code :** contient les exécutables du service hello, les fichiers binaires, les DLL et tous les autres fichiers toorun a besoin d’un service.</span><span class="sxs-lookup"><span data-stu-id="b73dc-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="b73dc-188">**Config :** tous les fichiers de configuration et les paramètres d’un service.</span><span class="sxs-lookup"><span data-stu-id="b73dc-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="b73dc-189">**Données :** les fichiers de données statiques associés hello service.</span><span class="sxs-lookup"><span data-stu-id="b73dc-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="b73dc-190">Chacun de ces packages peut être individuellement mis à niveau et faire l’objet d’un contrôle de version indépendant.</span><span class="sxs-lookup"><span data-stu-id="b73dc-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="b73dc-191">Services tooCloud similaires, un package de configuration sont accessibles par programme via une API et les événements sont des services de hello toonotify disponibles d’une modification de package de configuration.</span><span class="sxs-lookup"><span data-stu-id="b73dc-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="b73dc-192">Un fichier Settings.xml peut être utilisé pour la configuration de la clé-valeur et de l’accès par programme toohello application paramètres section similaire d’un fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="b73dc-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="b73dc-193">Toutefois, contrairement aux services cloud, les packages de configuration Service Fabric peuvent contenir des fichiers de configuration à n’importe quel format : XML, JSON, YAML ou tout format binaire personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b73dc-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="b73dc-194">Accès à la configuration</span><span class="sxs-lookup"><span data-stu-id="b73dc-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="b73dc-195">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b73dc-195">Cloud Services</span></span>
<span data-ttu-id="b73dc-196">Les paramètres de configuration de ServiceConfiguration.*.cscfg sont accessibles par le biais de `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="b73dc-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="b73dc-197">Ces paramètres sont des instances de rôle tooall globalement disponible Bonjour même déploiement de Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="b73dc-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="b73dc-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-198">Service Fabric</span></span>
<span data-ttu-id="b73dc-199">Chaque service dispose de son propre package de configuration individuel.</span><span class="sxs-lookup"><span data-stu-id="b73dc-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="b73dc-200">Il n’existe aucun mécanisme intégré permettant à toutes les applications d’un cluster d’accéder à l’ensemble des paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="b73dc-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="b73dc-201">Lorsque vous utilisez le fichier de configuration de Settings.xml spéciaux de l’infrastructure de Service au sein d’un package de configuration, les valeurs dans Settings.xml peuvent être remplacés au niveau d’application hello, ce qui rend les paramètres de configuration de niveau application possible.</span><span class="sxs-lookup"><span data-stu-id="b73dc-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="b73dc-202">Paramètres de configuration sont accède au sein de chaque instance de service par le biais du service hello `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="b73dc-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="b73dc-203">Événements de mise à jour de la configuration</span><span class="sxs-lookup"><span data-stu-id="b73dc-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="b73dc-204">Services cloud</span><span class="sxs-lookup"><span data-stu-id="b73dc-204">Cloud Services</span></span>
<span data-ttu-id="b73dc-205">Hello `RoleEnvironment.Changed` événement est utilisé toonotify toutes les instances de rôle lorsqu’une modification se produit dans l’environnement de hello, tels qu’un changement de configuration.</span><span class="sxs-lookup"><span data-stu-id="b73dc-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="b73dc-206">Il s’agit de mises à jour de la configuration tooconsume utilisé sans le recyclage des instances de rôle ou le redémarrage d’un processus de travail.</span><span class="sxs-lookup"><span data-stu-id="b73dc-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="b73dc-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-207">Service Fabric</span></span>
<span data-ttu-id="b73dc-208">Chacun des trois types de package hello dans un service de Code, configuration et données - possèdent des événements qui notifier une instance de service lorsqu’un package est mis à jour, ajouté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="b73dc-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="b73dc-209">Un service peut contenir plusieurs packages de chaque type.</span><span class="sxs-lookup"><span data-stu-id="b73dc-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="b73dc-210">Par exemple, un service peut avoir plusieurs packages de configuration, chacun pouvant être géré et mis à niveau individuellement.</span><span class="sxs-lookup"><span data-stu-id="b73dc-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="b73dc-211">Ces événements sont des modifications tooconsume disponible dans les packages de service sans avoir à redémarrer l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="b73dc-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="b73dc-212">Tâches de démarrage</span><span class="sxs-lookup"><span data-stu-id="b73dc-212">Startup tasks</span></span>
<span data-ttu-id="b73dc-213">Les tâches de démarrage sont des actions effectuées avant le démarrage d’une application.</span><span class="sxs-lookup"><span data-stu-id="b73dc-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="b73dc-214">Une tâche de démarrage est généralement utilisées toorun les scripts de configuration avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="b73dc-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="b73dc-215">Les services cloud et Service Fabric prennent tous deux en charge les tâches de démarrage.</span><span class="sxs-lookup"><span data-stu-id="b73dc-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="b73dc-216">Hello principale différence est que dans Services de cloud computing, une tâche de démarrage est liée tooa machine virtuelle, car il fait partie d’une instance de rôle, alors que le Service fabric une tâche de démarrage est service tooa liée, ce qui n’est pas liée tooany machine virtuelle particulière.</span><span class="sxs-lookup"><span data-stu-id="b73dc-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="b73dc-217">Services cloud</span><span class="sxs-lookup"><span data-stu-id="b73dc-217">Cloud Services</span></span> | <span data-ttu-id="b73dc-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b73dc-219">Emplacement de la configuration</span><span class="sxs-lookup"><span data-stu-id="b73dc-219">Configuration location</span></span> |<span data-ttu-id="b73dc-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="b73dc-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="b73dc-221">Privilèges</span><span class="sxs-lookup"><span data-stu-id="b73dc-221">Privileges</span></span> |<span data-ttu-id="b73dc-222">« limités » ou « élevés »</span><span class="sxs-lookup"><span data-stu-id="b73dc-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="b73dc-223">Séquencement</span><span class="sxs-lookup"><span data-stu-id="b73dc-223">Sequencing</span></span> |<span data-ttu-id="b73dc-224">« simple », « en arrière-plan », « au premier plan »</span><span class="sxs-lookup"><span data-stu-id="b73dc-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="b73dc-225">Services cloud</span><span class="sxs-lookup"><span data-stu-id="b73dc-225">Cloud Services</span></span>
<span data-ttu-id="b73dc-226">Dans les services cloud, un point d’entrée de démarrage est configuré pour chaque rôle dans le fichier ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="b73dc-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="b73dc-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-227">Service Fabric</span></span>
<span data-ttu-id="b73dc-228">Dans Service Fabric, un point d’entrée de démarrage est configuré pour chaque service dans le fichier ServiceManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="b73dc-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="b73dc-229">Remarque sur l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="b73dc-229">A note about development environment</span></span>
<span data-ttu-id="b73dc-230">Services Cloud et le Service Fabric sont intégrés à Visual Studio avec des modèles de projet et la prise en charge pour le débogage, la configuration et le déployer à la fois localement et tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b73dc-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="b73dc-231">Les services cloud et Service Fabric fournissent également tous deux un environnement local d’exécution de développement.</span><span class="sxs-lookup"><span data-stu-id="b73dc-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="b73dc-232">Hello différence est que pendant que le Service de cloud computing développement runtime émule hello hello environnement Azure sur lequel il s’exécute, Service Fabric n’utilise pas un émulateur - elle utilise le runtime Service Fabric complète de hello.</span><span class="sxs-lookup"><span data-stu-id="b73dc-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="b73dc-233">Hello Service Fabric est de l’environnement que vous exécutez sur votre ordinateur de développement local hello même environnement qui s’exécute en production.</span><span class="sxs-lookup"><span data-stu-id="b73dc-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b73dc-234">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b73dc-234">Next steps</span></span>
<span data-ttu-id="b73dc-235">En savoir plus sur le Service de l’infrastructure des Services fiables et hello différences fondamentales existant entre les Services de Cloud et le Service Fabric application architecture toounderstand définition parti tootake Hello complète des fonctionnalités de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="b73dc-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="b73dc-236">Découvrir les services fiables Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="b73dc-237">Différences de toohello guide conceptuelle entre les Services de cloud computing et le Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b73dc-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
