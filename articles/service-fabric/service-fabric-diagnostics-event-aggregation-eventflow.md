---
title: "aaaAzure l’agrégation d’événements Service Fabric avec EventFlow | Documents Microsoft"
description: "Découvrez l’agrégation et la collecte d’événements à l’aide d’EventFlow pour la surveillance et le diagnostic de clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="00b60-103">Agrégation et collection d’événements avec EventFlow</span><span class="sxs-lookup"><span data-stu-id="00b60-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="00b60-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) peut acheminer les événements à partir d’un nœud tooone ou autres destinations de surveillance.</span><span class="sxs-lookup"><span data-stu-id="00b60-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="00b60-105">Comme il est inclus en tant que package NuGet dans votre projet de service, configuration et le code de EventFlow se déplacent avec service hello, éliminant le problème de configuration de nœud par nœud hello mentionné plus haut sur les Diagnostics de Azure.</span><span class="sxs-lookup"><span data-stu-id="00b60-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="00b60-106">EventFlow s’exécute dans votre processus de service et se connecte directement les sorties toohello configuré.</span><span class="sxs-lookup"><span data-stu-id="00b60-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="00b60-107">En raison de la connexion directe de hello, EventFlow fonctionne pour Azure, conteneur et les déploiements de service local.</span><span class="sxs-lookup"><span data-stu-id="00b60-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="00b60-108">Faites preuve de prudence si vous exécutez EventFlow dans des scénarios de haute densité, par exemple dans un conteneur, car chaque pipeline EventFlow établit une connexion externe.</span><span class="sxs-lookup"><span data-stu-id="00b60-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="00b60-109">Par conséquent, si vous hébergez plusieurs processus, cela donne lieu à plusieurs connexions sortantes.</span><span class="sxs-lookup"><span data-stu-id="00b60-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="00b60-110">Cela n’est pas autant un critère important pour les applications de Service Fabric, car tous les réplicas d’un `ServiceType` exécuter Bonjour même processus, et cela limite le nombre de hello de connexions sortantes.</span><span class="sxs-lookup"><span data-stu-id="00b60-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="00b60-111">EventFlow offre également le filtrage d’événements, afin que seuls les événements hello qui correspondent au filtre spécifié de hello sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="00b60-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="00b60-112">Configuration d’EventFlow</span><span class="sxs-lookup"><span data-stu-id="00b60-112">Setting up EventFlow</span></span>

<span data-ttu-id="00b60-113">Les fichiers binaires EventFlow sont disponibles sous la forme d’un ensemble de packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="00b60-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="00b60-114">tooadd projet de service Service Fabric EventFlow tooa, avec le bouton droit de projet hello Bonjour l’Explorateur de solutions et choisissez « NuGet de gérer les packages ».</span><span class="sxs-lookup"><span data-stu-id="00b60-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="00b60-115">Commutateur toohello « Parcourir » onglet et recherchez «`Diagnostics.EventFlow`» :</span><span class="sxs-lookup"><span data-stu-id="00b60-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Packages NuGet EventFlow dans l’interface utilisateur du gestionnaire de package NuGet Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="00b60-117">Une liste de différents packages s’affiche, étiquetés avec « Entrées » et « Sorties ».</span><span class="sxs-lookup"><span data-stu-id="00b60-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="00b60-118">EventFlow prend en charge différents fournisseurs de journalisation et analyseurs.</span><span class="sxs-lookup"><span data-stu-id="00b60-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="00b60-119">service Hello EventFlow d’hébergement doit inclure les packages appropriés en fonction de la source de hello et de destination pour les journaux d’application hello.</span><span class="sxs-lookup"><span data-stu-id="00b60-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="00b60-120">En outre package de ServiceFabric toohello core, vous devez au moins une entrée et sortie configurée.</span><span class="sxs-lookup"><span data-stu-id="00b60-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="00b60-121">Par exemple, vous pouvez ajouter hello suivant packages toosent EventSource événements tooApplication Insights :</span><span class="sxs-lookup"><span data-stu-id="00b60-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="00b60-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture à partir de la classe EventSource du service hello, des données EventSources standard tels que *Services de Microsoft ServiceFabric* et *ServiceFabric-Microsoft-acteurs*)</span><span class="sxs-lookup"><span data-stu-id="00b60-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="00b60-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(nous allons toosend hello journaux tooan Azure Application Insights ressource)</span><span class="sxs-lookup"><span data-stu-id="00b60-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="00b60-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(permet l’initialisation du pipeline de EventFlow hello à partir de la configuration du service Service Fabric et signale les problèmes à l’envoi de données de diagnostic sous forme de rapports d’intégrité de l’infrastructure de Service)</span><span class="sxs-lookup"><span data-stu-id="00b60-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="00b60-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`le package nécessite hello service projet tootarget .NET Framework 4.6 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="00b60-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="00b60-126">Assurez-vous que vous définissez framework cible appropriée de hello dans Propriétés du projet avant d’installer ce package.</span><span class="sxs-lookup"><span data-stu-id="00b60-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="00b60-127">Une fois toutes les hello packages sont installés, étape suivante de hello est tooconfigure et activer EventFlow dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="00b60-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="00b60-128">Configuration et activation de la collecte de journaux</span><span class="sxs-lookup"><span data-stu-id="00b60-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="00b60-129">pipeline de EventFlow Hello chargé de l’envoi des journaux de hello est créé à partir d’une spécification stockée dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="00b60-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="00b60-130">Hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installe un fichier de configuration de départ EventFlow sous `PackageRoot\Config` dossier de solution, nommé `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="00b60-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="00b60-131">Ce fichier de configuration a besoin de données de toocapture de toobe modifié à partir de service par défaut de hello `EventSource` classe et autres entrées tooconfigure, envoyer et données toohello place approprié.</span><span class="sxs-lookup"><span data-stu-id="00b60-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="00b60-132">Voici un exemple *eventFlowConfig.json* basé sur les packages NuGet hello mentionnés ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="00b60-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="00b60-133">nom Hello de ServiceEventSource du service valeur hello Hello propriété Name de hello `EventSourceAttribute` appliqué toohello ServiceEventSource classe.</span><span class="sxs-lookup"><span data-stu-id="00b60-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="00b60-134">Il est spécifié dans hello `ServiceEventSource.cs` fichier, qui fait partie du code de service hello.</span><span class="sxs-lookup"><span data-stu-id="00b60-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="00b60-135">Par exemple, Bonjour suivant nom hello d’extrait de code Hello ServiceEventSource est *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="00b60-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="00b60-136">Notez que le fichier `eventFlowConfig.json` fait partie du package de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="00b60-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="00b60-137">Fichier toothis des modifications peut être inclus dans intégral ou configuration-uniquement les mises à niveau du service de hello, objet tooService Fabric mise à niveau les vérifications d’intégrité et restauration automatique cas d’échec de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="00b60-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="00b60-138">Pour plus d’informations, consultez [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="00b60-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="00b60-139">Hello *filtres* section de la configuration de hello vous permet de toofurther personnaliser informations hello toogo continu des sorties de toohello pipeline hello EventFlow, ce qui vous toodrop ou inclure certaines informations ou modifier hello structure de données d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="00b60-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="00b60-140">Pour plus d’informations sur le filtrage, consultez les [Filtres EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="00b60-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="00b60-141">étape finale de Hello est le pipeline de EventFlow tooinstantiate dans le code de démarrage de votre service, situé dans `Program.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="00b60-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="00b60-142">nom de Hello passé comme paramètre hello Hello `CreatePipeline` méthode Hello `ServiceFabricDiagnosticsPipelineFactory` hello désigne hello *entité de contrôle d’intégrité* représentant le pipeline de collection de journaux de EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="00b60-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="00b60-143">Ce nom est utilisé en cas de EventFlow et d’erreur et la signale via hello sous-système de contrôle d’intégrité de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="00b60-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="00b60-144">À l’aide des paramètres de la structure de Service et application paramètres tooin eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="00b60-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="00b60-145">EventFlow prend en charge à l’aide des paramètres de la structure de Service et les paramètres d’application paremeters tooconfigure EventFlow.</span><span class="sxs-lookup"><span data-stu-id="00b60-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="00b60-146">Vous pouvez consulter les paramètres de paramètres de l’ensemble fibre optique tooService à l’aide de cette syntaxe spéciale pour les valeurs :</span><span class="sxs-lookup"><span data-stu-id="00b60-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="00b60-147">`<section-name>`est le nom hello Hello section de configuration de l’infrastructure de Service, et `<setting-name>` configuration hello à fournissant valeur hello tooconfigure utilisé un paramètre EventFlow.</span><span class="sxs-lookup"><span data-stu-id="00b60-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="00b60-148">plus sur la façon de tooread toodo, accédez trop[prise en charge pour les paramètres de l’infrastructure de Service et application](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="00b60-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="00b60-149">Vérification</span><span class="sxs-lookup"><span data-stu-id="00b60-149">Verification</span></span>

<span data-ttu-id="00b60-150">Démarrer votre service et observez hello débogage fenêtre Sortie de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00b60-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="00b60-151">Après le démarrage du service de hello, vous devez commencer à voir la preuve que l’envoi de votre service enregistre la sortie toohello que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="00b60-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="00b60-152">Accédez tooyour événement analyse et visualisation de la plateforme et vérifiez que les journaux ont démarré tooshow up (opération peut prendre quelques minutes).</span><span class="sxs-lookup"><span data-stu-id="00b60-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00b60-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00b60-153">Next steps</span></span>

* [<span data-ttu-id="00b60-154">Analyse et visualisation d’événements avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="00b60-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="00b60-155">Analyse et visualisation d’événements avec OMS</span><span class="sxs-lookup"><span data-stu-id="00b60-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="00b60-156">Documentation relative à EventFlow</span><span class="sxs-lookup"><span data-stu-id="00b60-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)