---
title: "Diffusion des données d’Azure Diagnostics dans le chemin réactif à l’aide d’Event Hubs | Microsoft Docs"
description: "Configuration de bout en bout d’Azure Diagnostics avec Event Hubs, y compris des conseils relatifs aux scénarios courants."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="daf97-103">Diffusion des données d’Azure Diagnostics dans le chemin réactif à l’aide d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="daf97-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="daf97-104">Azure Diagnostics propose des moyens flexibles de collecter des mesures et des journaux à partir de machines virtuelles de services cloud et de transférer les résultats dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="daf97-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="daf97-105">Depuis mars 2016 (Kit de développement logiciel (SDK) 2.9), vous pouvez envoyer les données Diagnostics à des sources de données personnalisées et transférer des données de chemin réactif en quelques secondes à l’aide [d’Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="daf97-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="daf97-106">Les types de données pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="daf97-106">Supported data types include:</span></span>

* <span data-ttu-id="daf97-107">Suivi d’événements pour les événements Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="daf97-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="daf97-108">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="daf97-108">Performance counters</span></span>
* <span data-ttu-id="daf97-109">Journaux d’événements Windows</span><span class="sxs-lookup"><span data-stu-id="daf97-109">Windows event logs</span></span>
* <span data-ttu-id="daf97-110">Journaux d’application</span><span class="sxs-lookup"><span data-stu-id="daf97-110">Application logs</span></span>
* <span data-ttu-id="daf97-111">Journaux d’infrastructure de diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="daf97-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="daf97-112">Cet article vous montre la procédure complète de configuration de diagnostics  Azure avec Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="daf97-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="daf97-113">Des recommandations vous sont également proposées pour les scénarios courants suivants :</span><span class="sxs-lookup"><span data-stu-id="daf97-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="daf97-114">Comment personnaliser les journaux et les mesures envoyés à Event Hubs</span><span class="sxs-lookup"><span data-stu-id="daf97-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="daf97-115">Comment modifier les configurations dans chaque environnement</span><span class="sxs-lookup"><span data-stu-id="daf97-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="daf97-116">Comment afficher les données de flux Event Hubs</span><span class="sxs-lookup"><span data-stu-id="daf97-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="daf97-117">Comment résoudre les problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="daf97-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="daf97-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="daf97-118">Prerequisites</span></span>
<span data-ttu-id="daf97-119">La réception par Event Hubs de données provenant d’Azure Diagnostics est prise en charge dans Services cloud, Machines virtuelles, Virtual Machine Scale Sets et Service Fabric à partir du Kit de développement logiciel (SDK) 2.9 Azure, ainsi que dans les outils Azure correspondants pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daf97-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="daf97-120">Extension Azure Diagnostics 1.6 (ciblée par défaut par le[Kit de développement logiciel (SDK) Azure pour .NET 2.9 ou ultérieur](https://azure.microsoft.com/downloads/) )</span><span class="sxs-lookup"><span data-stu-id="daf97-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="daf97-121">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="daf97-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="daf97-122">Configurations existantes d’Azure Diagnostics dans une application à l’aide d’un fichier *.wadcfgx* et de l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="daf97-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="daf97-123">Visual Studio : [Configuration de Diagnostics pour les services cloud et les machines virtuelles Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="daf97-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="daf97-124">Windows PowerShell : [Activer les diagnostics dans Services cloud Azure à l’aide de PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="daf97-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="daf97-125">Espace de noms Event Hubs approvisionné tel que décrit dans l’article [Prise en main d’Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="daf97-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="daf97-126">Connexion d’Azure Diagnostics au récepteur Event Hubs</span><span class="sxs-lookup"><span data-stu-id="daf97-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="daf97-127">Par défaut, Azure Diagnostics transmet toujours des journaux et des mesures à un compte Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="daf97-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="daf97-128">Une application peut également envoyer des données vers Event Hubs en ajoutant une nouvelle section **Sinks** sous l’élément **PublicConfig** / **WadCfg** du fichier *.wadcfgx*.</span><span class="sxs-lookup"><span data-stu-id="daf97-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="daf97-129">Dans Visual Studio, le fichier *.wadcfgx* est stocké dans le chemin suivant : **Projet de service cloud** > **Rôles** > **(RoleName)** > fichier **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="daf97-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="daf97-130">Dans cet exemple, l’URL du hub d’événements est définie sur l’espace de noms complet du hub d’événements (espace de noms Event Hubs + « / » + nom du hub d’événements).</span><span class="sxs-lookup"><span data-stu-id="daf97-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="daf97-131">L’URL du hub d’événements s’affiche dans le [portail Azure](http://go.microsoft.com/fwlink/?LinkID=213885) dans le tableau de bord Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="daf97-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="daf97-132">Le nom **Sink** peut être défini sur n’importe quelle chaîne valide tant que cette même valeur est utilisée de manière cohérente dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="daf97-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="daf97-133">Des récepteurs supplémentaires, tels que *applicationInsights* , peuvent être configurés dans cette section.</span><span class="sxs-lookup"><span data-stu-id="daf97-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="daf97-134">Azure Diagnostics permet de définir un ou plusieurs récepteurs si chaque récepteur est également déclaré dans la section **PrivateConfig** .</span><span class="sxs-lookup"><span data-stu-id="daf97-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="daf97-135">Le récepteur Event Hubs doit également être déclaré et défini dans la section **PrivateConfig** du fichier de configuration *.wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="daf97-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="daf97-136">La valeur `SharedAccessKeyName` doit correspondre à une clé de signature d’accès partagé (SAS) et à une stratégie définie dans l’espace de noms **Event Hubs** .</span><span class="sxs-lookup"><span data-stu-id="daf97-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="daf97-137">Dans le [portail Azure](https://manage.windowsazure.com), accédez au tableau de bord Event Hubs, cliquez sur l’onglet **Configurer** et définissez une stratégie nommée (par exemple, « SendRule ») qui possède des autorisations *d’envoi* .</span><span class="sxs-lookup"><span data-stu-id="daf97-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="daf97-138">L’élément **StorageAccount** est également déclaré dans le fichier **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="daf97-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="daf97-139">Il est inutile de modifier les valeurs ici si elles fonctionnent correctement.</span><span class="sxs-lookup"><span data-stu-id="daf97-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="daf97-140">Dans cet exemple, nous ne renseignons pas les valeurs afin d’indiquer que ces valeurs seront définies par une ressource en aval.</span><span class="sxs-lookup"><span data-stu-id="daf97-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="daf97-141">Par exemple, le fichier de configuration d’environnement *ServiceConfiguration.Cloud.cscfg* définit les noms et les clés appropriés à l’environnement.</span><span class="sxs-lookup"><span data-stu-id="daf97-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="daf97-142">La clé SAP Event Hubs est stockée en texte brut dans le fichier *.wadcfgx*.</span><span class="sxs-lookup"><span data-stu-id="daf97-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="daf97-143">Cette clé est souvent intégrée au contrôle du code source ou est disponible en tant que ressource dans votre serveur de builds. Vous devez donc la protéger en conséquence.</span><span class="sxs-lookup"><span data-stu-id="daf97-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="daf97-144">Nous vous recommandons d’utiliser ici une clé SAP avec les autorisations *Envoyer uniquement* afin qu’un utilisateur malveillant puisse écrire dans le hub d’événements, mais sans l’écouter ni le gérer.</span><span class="sxs-lookup"><span data-stu-id="daf97-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="daf97-145">Configurer Azure Diagnostics pour l’envoi de journaux et de mesures vers Event Hubs</span><span class="sxs-lookup"><span data-stu-id="daf97-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="daf97-146">Comme indiqué précédemment, toutes les données de diagnostic par défaut et personnalisées (autrement dit, les mesures et journaux) sont automatiquement envoyées vers Stockage Azure à des intervalles configurés.</span><span class="sxs-lookup"><span data-stu-id="daf97-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="daf97-147">Avec Event Hubs et tout récepteur supplémentaire, vous pouvez spécifier n’importe quel nœud racine ou terminal de la hiérarchie à envoyer au hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="daf97-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="daf97-148">Cela inclut les événements ETW, les compteurs de performances, les journaux des événements Windows et les journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="daf97-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="daf97-149">Il est important de prendre en compte le nombre de points de données qui doit réellement être transféré vers Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="daf97-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="daf97-150">En règle générale, les développeurs transfèrent des données de chemin réactif à faible latence qui doivent être consommées et interprétées rapidement.</span><span class="sxs-lookup"><span data-stu-id="daf97-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="daf97-151">Il s’agit, par exemple, des systèmes qui analysent les alertes ou les règles de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="daf97-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="daf97-152">Un développeur peut également configurer un autre magasin d’analyse ou de recherche, par exemple, Azure Stream Analytics, ElasticSearch, un système de surveillance personnalisé ou un système de surveillance tiers favori.</span><span class="sxs-lookup"><span data-stu-id="daf97-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="daf97-153">Voici quelques exemples de configurations :</span><span class="sxs-lookup"><span data-stu-id="daf97-153">The following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="daf97-154">Dans l’exemple ci-dessus, le récepteur est appliqué au nœud parent **PerformanceCounters** dans la hiérarchie, ce qui signifie que tous les enfants **PerformanceCounters** sont envoyés à Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="daf97-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="daf97-155">Dans l’exemple précédent, le récepteur est appliqué uniquement à trois compteurs : **Demandes en attente**, **Demandes rejetées** et **% temps processeur**.</span><span class="sxs-lookup"><span data-stu-id="daf97-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="daf97-156">L’exemple suivant montre comment un développeur peut limiter le volume de données envoyées comme mesures critiques utilisées pour l’intégrité de ce service.</span><span class="sxs-lookup"><span data-stu-id="daf97-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="daf97-157">Dans cet exemple, le récepteur est appliqué aux journaux et filtré uniquement pour le suivi au niveau de l’erreur.</span><span class="sxs-lookup"><span data-stu-id="daf97-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="daf97-158">Déploiement et mise à jour d’une configuration de diagnostics et d’application de services cloud</span><span class="sxs-lookup"><span data-stu-id="daf97-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="daf97-159">Visual Studio offre le moyen le plus facile de déployer l’application et de configurer le récepteur Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="daf97-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="daf97-160">Pour afficher et modifier le fichier, ouvrez le fichier *.wadcfgx* dans Visual Studio, modifiez-le, puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="daf97-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="daf97-161">Le chemin d’accès est **Projet de service cloud** > **rôles** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="daf97-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="daf97-162">À ce stade, toutes les opérations de déploiement et de mise à jour du déploiement effectuées dans Visual Studio et dans Visual Studio Team System, de même que l’ensemble des commandes ou scripts basés sur MSBuild et qui utilisent la cible **/t:publish** incluent le fichier *.wadcfgx* dans le processus d’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="daf97-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="daf97-163">En outre, les déploiements et les mises à jour déploient le fichier vers Azure à l’aide de l’extension de l’agent Azure Diagnostics appropriée sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="daf97-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="daf97-164">Une fois l’application et la configuration d’Azure Diagnostics déployées, l’activité correspondante s’affiche dans le tableau de bord du hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="daf97-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="daf97-165">Cela vous indique que vous pouvez maintenant afficher les données de chemin réactif dans le client d’écouteur ou l’outil d’analyse de votre choix.</span><span class="sxs-lookup"><span data-stu-id="daf97-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="daf97-166">Dans l’illustration suivante, le tableau de bord Event Hubs indique un envoi intègre de données de diagnostic vers le hub d’événements après 23h00.</span><span class="sxs-lookup"><span data-stu-id="daf97-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="daf97-167">Cette heure correspond au moment où l’application a été déployée avec un fichier *.wadcfgx* mis à jour et où le récepteur a été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="daf97-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="daf97-168">Lorsque vous effectuez des mises à jour du fichier de configuration d’Azure Diagnostics (.wadcfgx), il est recommandé de les publier dans l’ensemble de l’application et de la configuration à l’aide de la publication Visual Studio ou d’un script Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daf97-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="daf97-169">Affichage des données de chemin réactif</span><span class="sxs-lookup"><span data-stu-id="daf97-169">View hot-path data</span></span>
<span data-ttu-id="daf97-170">Comme indiqué précédemment, il existe plusieurs scénarios d’utilisation pour écouter et traiter des données Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="daf97-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="daf97-171">Une approche simple consiste à créer une petite application console de test pour écouter le hub d’événements et imprimer le flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="daf97-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="daf97-172">Vous pouvez placer le code suivant (expliqué plus en détail dans l’article [Prise en main d’Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)) dans une application console.</span><span class="sxs-lookup"><span data-stu-id="daf97-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="daf97-173">Notez que l’application console doit inclure le [package Event Processor Host NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="daf97-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="daf97-174">N’oubliez pas de remplacer les valeurs entre crochets de la fonction **Main** par les valeurs de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="daf97-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="daf97-175">Résolution des problèmes liés aux récepteurs Event Hubs</span><span class="sxs-lookup"><span data-stu-id="daf97-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="daf97-176">Le hub d’événements n’affiche pas l’activité attendue relative à des événements entrants ou sortants.</span><span class="sxs-lookup"><span data-stu-id="daf97-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="daf97-177">Vérifiez que le hub d’événements a été correctement approvisionné.</span><span class="sxs-lookup"><span data-stu-id="daf97-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="daf97-178">Toutes les informations de connexion de la section **PrivateConfig** du fichier *.wadcfgx* doivent correspondre aux valeurs de votre ressource, comme indiqué dans le portail.</span><span class="sxs-lookup"><span data-stu-id="daf97-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="daf97-179">Assurez-vous qu’une stratégie SAS est définie (« SendRule » dans l’exemple) dans le portail et que l’autorisation *d’envoi* a été octroyée.</span><span class="sxs-lookup"><span data-stu-id="daf97-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="daf97-180">Après une mise à jour, le hub d’événements n’affiche plus d’activité relative aux événements entrants ou sortants.</span><span class="sxs-lookup"><span data-stu-id="daf97-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="daf97-181">Tout d’abord, assurez-vous que les informations du hub d’événements et de la configuration sont correctes, comme nous l’avons expliqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="daf97-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="daf97-182">Le fichier **PrivateConfig** est parfois réinitialisé au cours d’une mise à jour du déploiement.</span><span class="sxs-lookup"><span data-stu-id="daf97-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="daf97-183">La solution recommandée consiste à apporter toutes les modifications dans le projet *.wadcfgx* , puis à transmettre une mise à jour complète de l’application.</span><span class="sxs-lookup"><span data-stu-id="daf97-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="daf97-184">Si ce n’est pas possible, assurez-vous que la mise à jour des diagnostics transmet un fichier **PrivateConfig** complet qui comprend la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="daf97-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="daf97-185">J’ai essayé ces suggestions, mais le hub d’événements ne fonctionne toujours pas.</span><span class="sxs-lookup"><span data-stu-id="daf97-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="daf97-186">Consultez la table Azure Storage **WADDiagnosticInfrastructureLogsTable**qui contient les journaux et les erreurs d’Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="daf97-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="daf97-187">Une option consiste à utiliser un outil tel que l’ [explorateur de stockage Azure](http://www.storageexplorer.com) pour vous connecter à ce compte de stockage, consulter cette table et ajouter une requête pour l’horodatage (TimeStamp) des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="daf97-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="daf97-188">Vous pouvez utiliser l’outil pour exporter un fichier .csv et l’ouvrir dans une application comme Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="daf97-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="daf97-189">Excel permet de rechercher facilement des chaînes de carte d’appel, telles **qu’EventHubs**afin d’identifier l’erreur signalée.</span><span class="sxs-lookup"><span data-stu-id="daf97-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="daf97-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daf97-190">Next steps</span></span>
<span data-ttu-id="daf97-191">•    [En savoir plus sur Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="daf97-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="daf97-192">Annexe : Exemple de fichier de configuration d’Azure Diagnostics (.wadcfgx)</span><span class="sxs-lookup"><span data-stu-id="daf97-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="daf97-193">Le fichier complémentaire *ServiceConfiguration.Cloud.cscfg* pour cet exemple se présente comme suit.</span><span class="sxs-lookup"><span data-stu-id="daf97-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="daf97-194">Les paramètres équivalents JSON pour les machines virtuelles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="daf97-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="daf97-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daf97-195">Next steps</span></span>
<span data-ttu-id="daf97-196">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="daf97-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="daf97-197">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="daf97-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="daf97-198">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="daf97-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="daf97-199">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="daf97-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
