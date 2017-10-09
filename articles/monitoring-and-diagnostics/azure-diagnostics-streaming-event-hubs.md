---
title: "aaaStreaming des données de Diagnostics Azure dans le chemin d’accès à chaud hello à l’aide de concentrateurs d’événements | Documents Microsoft"
description: "Configuration des Diagnostics Azure avec des concentrateurs d’événements de fin tooend, y compris des instructions pour les scénarios courants."
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
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="95a23-103">Diffusion en continu des données de Diagnostics Azure dans le chemin réactif hello à l’aide de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="95a23-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="95a23-104">Diagnostics Azure fournit des méthodes souples toocollect métriques et des journaux à partir de cloud services virtual machines virtuelles et de transférer les résultats tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="95a23-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="95a23-105">À compter de l’intervalle de temps hello mars 2016 (Kit de développement logiciel 2.9), vous pouvez envoyer Diagnostics toocustom des sources de données et transférer des données de chemin réactif en secondes à l’aide de [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="95a23-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="95a23-106">Les types de données pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="95a23-106">Supported data types include:</span></span>

* <span data-ttu-id="95a23-107">Suivi d’événements pour les événements Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="95a23-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="95a23-108">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="95a23-108">Performance counters</span></span>
* <span data-ttu-id="95a23-109">Journaux d’événements Windows</span><span class="sxs-lookup"><span data-stu-id="95a23-109">Windows event logs</span></span>
* <span data-ttu-id="95a23-110">Journaux d’application</span><span class="sxs-lookup"><span data-stu-id="95a23-110">Application logs</span></span>
* <span data-ttu-id="95a23-111">Journaux d’infrastructure de diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="95a23-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="95a23-112">Cet article explique comment tooconfigure Azure Diagnostics avec les concentrateurs d’événements de fin tooend.</span><span class="sxs-lookup"><span data-stu-id="95a23-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="95a23-113">Aucune aide est également fournie pour hello les scénarios courants suivants :</span><span class="sxs-lookup"><span data-stu-id="95a23-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="95a23-114">Mode de journalisation des toocustomize hello et métriques envoyées tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="95a23-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="95a23-115">Comment les configurations toochange dans chaque environnement</span><span class="sxs-lookup"><span data-stu-id="95a23-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="95a23-116">Comment tooview concentrateurs d’événements de flux de données</span><span class="sxs-lookup"><span data-stu-id="95a23-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="95a23-117">Comment tootroubleshoot hello connexion</span><span class="sxs-lookup"><span data-stu-id="95a23-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="95a23-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="95a23-118">Prerequisites</span></span>
<span data-ttu-id="95a23-119">Des données receieving de concentrateurs d’événements à partir d’Azure Diagnostics sont prise en charge dans les Services de cloud computing, machines virtuelles, machines virtuelles identiques et l’infrastructure de Service à partir de hello Azure SDK 2.9 et hello correspondant Windows Azure Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95a23-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="95a23-120">Extension Azure Diagnostics 1.6 (ciblée par défaut par le[Kit de développement logiciel (SDK) Azure pour .NET 2.9 ou ultérieur](https://azure.microsoft.com/downloads/) )</span><span class="sxs-lookup"><span data-stu-id="95a23-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="95a23-121">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="95a23-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="95a23-122">Des configurations de Diagnostics Azure dans une application à l’aide un *.wadcfgx* fichier et l’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="95a23-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="95a23-123">Visual Studio : [Configuration de Diagnostics pour les services cloud et les machines virtuelles Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="95a23-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="95a23-124">Windows PowerShell : [Activer les diagnostics dans Services cloud Azure à l’aide de PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="95a23-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="95a23-125">Espace de noms de concentrateurs événements mis en service par l’article hello, [prise en main les concentrateurs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="95a23-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="95a23-126">Se connecter à Azure Diagnostics tooEvent concentrateurs récepteur</span><span class="sxs-lookup"><span data-stu-id="95a23-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="95a23-127">Par défaut, les Diagnostics Windows Azure envoie toujours des journaux et des métriques tooan compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="95a23-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="95a23-128">Une application peut également envoyer des données tooEvent concentrateurs en ajoutant un nouvel **récepteurs** section sous hello **PublicConfig** / **WadCfg** élément Hello *.wadcfgx* fichier.</span><span class="sxs-lookup"><span data-stu-id="95a23-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="95a23-129">Dans Visual Studio, hello *.wadcfgx* fichier est stocké dans hello suivant le chemin d’accès : **projet de Service Cloud** > **rôles** > **() RoleName)** > **diagnostics.wadcfgx** fichier.</span><span class="sxs-lookup"><span data-stu-id="95a23-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="95a23-130">Dans cet exemple, le concentrateur d’événements hello URL a la valeur toohello entièrement qualifié espace de noms du hub d’événements hello : espace de noms de concentrateurs d’événements + « / » + nom de hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="95a23-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="95a23-131">concentrateur d’événements Hello URL s’affiche dans hello [portail Azure](http://go.microsoft.com/fwlink/?LinkID=213885) sur le tableau de bord hello concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="95a23-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="95a23-132">Hello **récepteur** nom peut être défini tooany les chaîne valide tant que hello même valeur est utilisée par tout au long de fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="95a23-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="95a23-133">Des récepteurs supplémentaires, tels que *applicationInsights* , peuvent être configurés dans cette section.</span><span class="sxs-lookup"><span data-stu-id="95a23-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="95a23-134">Diagnostics Azure permet à un ou plusieurs récepteurs toobe défini si chaque récepteur est également déclaré dans hello **PrivateConfig** section.</span><span class="sxs-lookup"><span data-stu-id="95a23-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="95a23-135">Hello concentrateurs d’événements récepteur doit également être déclaré et défini dans hello **PrivateConfig** section Hello *.wadcfgx* le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="95a23-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="95a23-136">Hello `SharedAccessKeyName` valeur doit correspondre à une clé de Signature d’accès partagé (SAP) et la stratégie qui a été défini dans hello **concentrateurs d’événements** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="95a23-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="95a23-137">Parcourir le tableau de bord de concentrateurs d’événements toohello Bonjour [portail Azure](https://manage.windowsazure.com), cliquez sur hello **configurer** onglet et définir une stratégie nommée (par exemple, « SendRule ») qui a *envoyer* autorisations.</span><span class="sxs-lookup"><span data-stu-id="95a23-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="95a23-138">Hello **StorageAccount** est également déclaré dans **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="95a23-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="95a23-139">Il n’est pas nécessaire ici les valeurs toochange s’ils fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="95a23-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="95a23-140">Dans cet exemple, nous ne renseignez pas les valeurs hello, qui est un signe qu’un composant en aval définira les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="95a23-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="95a23-141">Par exemple, hello *ServiceConfiguration.Cloud.cscfg* fichier de configuration d’environnement définit les noms d’environnement approprié hello et les clés.</span><span class="sxs-lookup"><span data-stu-id="95a23-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="95a23-142">la clé SAS de concentrateurs d’événements de Hello est stockée en texte brut dans hello *.wadcfgx* fichier.</span><span class="sxs-lookup"><span data-stu-id="95a23-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="95a23-143">Souvent, cette clé est activée dans le contrôle de code toosource ou n’est disponible en tant qu’un élément multimédia dans votre serveur de builds, vous devez donc protéger il comme il convient.</span><span class="sxs-lookup"><span data-stu-id="95a23-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="95a23-144">Nous vous recommandons d’utiliser une clé SAS ici avec *envoyer uniquement* autorisations afin qu’un utilisateur malveillant peut écrire toohello concentrateur d’événements, mais pas écouter tooit ou le gérer.</span><span class="sxs-lookup"><span data-stu-id="95a23-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="95a23-145">Configurer les Diagnostics Azure toosend métriques et journaux tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="95a23-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="95a23-146">Comme indiqué précédemment, tous les par défaut et les données de diagnostic personnalisé, autrement dit, mesures et les journaux, est automatiquement envoyé tooAzure stockage dans des intervalles de salutation configurée.</span><span class="sxs-lookup"><span data-stu-id="95a23-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="95a23-147">Avec des concentrateurs d’événements et n’importe quel récepteur supplémentaire, vous pouvez spécifier n’importe quel nœud racine ou feuille dans toobe de hiérarchie hello envoyé toohello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="95a23-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="95a23-148">Cela inclut les événements ETW, les compteurs de performances, les journaux des événements Windows et les journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="95a23-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="95a23-149">Il est important de tooconsider combien de points de données doit être transférées tooEvent concentrateurs.</span><span class="sxs-lookup"><span data-stu-id="95a23-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="95a23-150">En règle générale, les développeurs transfèrent des données de chemin réactif à faible latence qui doivent être consommées et interprétées rapidement.</span><span class="sxs-lookup"><span data-stu-id="95a23-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="95a23-151">Il s’agit, par exemple, des systèmes qui analysent les alertes ou les règles de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="95a23-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="95a23-152">Un développeur peut également configurer un autre magasin d’analyse ou de recherche, par exemple, Azure Stream Analytics, ElasticSearch, un système de surveillance personnalisé ou un système de surveillance tiers favori.</span><span class="sxs-lookup"><span data-stu-id="95a23-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="95a23-153">Hello Voici quelques exemples de configuration.</span><span class="sxs-lookup"><span data-stu-id="95a23-153">hello following are some example configurations.</span></span>

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

<span data-ttu-id="95a23-154">Bonjour exemple ci-dessus, l’intercepteur hello est appliqué toohello parent **PerformanceCounters** nœud dans la hiérarchie de hello, ce qui signifie que tous les enfants **PerformanceCounters** tooEvent Hubs sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="95a23-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

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

<span data-ttu-id="95a23-155">Dans l’exemple précédent de hello, récepteur de hello est appliqué tooonly trois compteurs : **en file d’attente de demandes**, **demandes rejetées**, et **% temps processeur**.</span><span class="sxs-lookup"><span data-stu-id="95a23-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="95a23-156">Hello suivant montre comment un développeur peut limiter la quantité hello données envoyées toobe hello métriques critiques qui sont utilisés pour le contrôle d’intégrité de ce service.</span><span class="sxs-lookup"><span data-stu-id="95a23-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="95a23-157">Dans cet exemple, le récepteur de hello est toologs appliqués et filtré de suivi de niveau tooerror uniquement.</span><span class="sxs-lookup"><span data-stu-id="95a23-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="95a23-158">Déploiement et mise à jour d’une configuration de diagnostics et d’application de services cloud</span><span class="sxs-lookup"><span data-stu-id="95a23-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="95a23-159">Visual Studio fournit l’application hello plus simple chemin d’accès toodeploy hello et configuration de récepteur de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="95a23-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="95a23-160">fichier hello tooview et modifier, ouvrez hello *.wadcfgx* de fichiers dans Visual Studio, modifiez-le, puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="95a23-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="95a23-161">chemin d’accès Hello est **projet de Service Cloud** > **rôles** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="95a23-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="95a23-162">À ce stade, tous les déploiement déploiement mise à jour et des actions dans Visual Studio, Visual Studio Team System et toutes les commandes ou scripts qui sont basés sur MSBuild et utilisent hello **/t : publier** cible incluent hello *.wadcfgx*  dans le processus d’empaquetage hello.</span><span class="sxs-lookup"><span data-stu-id="95a23-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="95a23-163">En outre, les mises à jour et les déploiements déploiement hello fichier tooAzure à l’aide d’extension de l’agent de Diagnostics Azure appropriée hello sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="95a23-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="95a23-164">Après avoir déployé l’application hello et configuration des Diagnostics Windows Azure, vous verrez immédiatement l’activité dans le tableau de bord de hello du concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="95a23-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="95a23-165">Cela indique que vous êtes prêt toomove sur les données de chemin d’accès à chaud tooviewing hello dans hello écouteur client ou l’analyse de l’outil de votre choix.</span><span class="sxs-lookup"><span data-stu-id="95a23-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="95a23-166">Dans la figure suivante de hello, tableau de bord de concentrateurs d’événements hello affiche envoi intègre de démarrage de diagnostics données toohello événement hub après 23 h 00.</span><span class="sxs-lookup"><span data-stu-id="95a23-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="95a23-167">C'est-à-dire quand hello application a été déployée avec une mise à jour *.wadcfgx* de fichiers et hello récepteur a été configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="95a23-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="95a23-168">Lorsque vous modifiez le fichier de configuration de Diagnostics Azure mises à jour toohello (.wadcfgx), il est recommandé que vous effectuez un push hello mises à jour toohello ensemble de l’application, ainsi qu’une configuration de hello à l’aide de la publication dans Visual Studio, ou un script Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95a23-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="95a23-169">Affichage des données de chemin réactif</span><span class="sxs-lookup"><span data-stu-id="95a23-169">View hot-path data</span></span>
<span data-ttu-id="95a23-170">Comme indiqué précédemment, il existe plusieurs cas d’usage pour l’écoute tooand le traitement des données de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="95a23-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="95a23-171">Une approche simple est toocreate un concentrateur d’événements de test peu console application toolisten toohello et impression hello le flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="95a23-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="95a23-172">Vous pouvez placer hello suivant de code, qui est expliquée plus en détail dans [prise en main les concentrateurs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), dans une application console.</span><span class="sxs-lookup"><span data-stu-id="95a23-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="95a23-173">Notez que les applications de console hello doivent inclure hello [événement processeur hôte NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="95a23-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="95a23-174">N’oubliez pas de valeurs de hello tooreplace figurant entre crochets Bonjour **Main** fonction avec des valeurs pour vos ressources.</span><span class="sxs-lookup"><span data-stu-id="95a23-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="95a23-175">Résolution des problèmes liés aux récepteurs Event Hubs</span><span class="sxs-lookup"><span data-stu-id="95a23-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="95a23-176">concentrateur d’événements Hello n’affiche pas l’activité d’événements entrants ou sortants comme prévu.</span><span class="sxs-lookup"><span data-stu-id="95a23-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="95a23-177">Vérifiez que le hub d’événements a été correctement approvisionné.</span><span class="sxs-lookup"><span data-stu-id="95a23-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="95a23-178">Toutes les informations de connexion dans hello **PrivateConfig** section de *.wadcfgx* doit correspondre à valeurs hello de votre ressource, comme indiqué dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="95a23-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="95a23-179">Assurez-vous que vous disposez d’une SAS stratégie définie (« SendRule » dans l’exemple de hello) dans le portail de hello et qui *envoyer* l’autorisation est accordée.</span><span class="sxs-lookup"><span data-stu-id="95a23-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="95a23-180">Après une mise à jour, concentrateur d’événements hello n’affiche plus activité d’événement entrant ou sortant.</span><span class="sxs-lookup"><span data-stu-id="95a23-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="95a23-181">Tout d’abord, vérifiez que ce concentrateur d’événements hello et informations de configuration sont correcte, comme expliqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="95a23-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="95a23-182">Parfois hello **PrivateConfig** est réinitialisée dans une mise à jour du déploiement.</span><span class="sxs-lookup"><span data-stu-id="95a23-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="95a23-183">Hello recommandé de correctif toomake toutes les modifications trop*.wadcfgx* hello du projet et ensuite, pour ajouter une mise à jour de l’application complète.</span><span class="sxs-lookup"><span data-stu-id="95a23-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="95a23-184">Si ce n’est pas possible, assurez-vous que cette mise à jour des diagnostics hello pousse complète **PrivateConfig** qui inclut la clé SAS hello.</span><span class="sxs-lookup"><span data-stu-id="95a23-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="95a23-185">J’ai essayé les suggestions hello et concentrateur d’événements hello fonctionne toujours pas.</span><span class="sxs-lookup"><span data-stu-id="95a23-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="95a23-186">Recherchez dans la table de stockage Azure hello qui contient des erreurs et des journaux de Diagnostics Azure lui-même : **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="95a23-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="95a23-187">Une option consiste à toouse un outil tel que [Azure Storage Explorer](http://www.storageexplorer.com) compte de stockage tooconnect toothis, afficher ce tableau et ajouter une requête pour l’horodatage Bonjour des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="95a23-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="95a23-188">Vous pouvez utiliser l’outil de hello tooexport un fichier .csv et ouvrez-le dans une application telle que Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="95a23-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="95a23-189">Excel rend toosearch facile pour les chaînes de la carte d’appel, tels que **EventHubs**, toosee d’indiquer l’erreur est signalée.</span><span class="sxs-lookup"><span data-stu-id="95a23-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="95a23-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95a23-190">Next steps</span></span>
<span data-ttu-id="95a23-191">•    [En savoir plus sur Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="95a23-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="95a23-192">Annexe : Exemple de fichier de configuration d’Azure Diagnostics (.wadcfgx)</span><span class="sxs-lookup"><span data-stu-id="95a23-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="95a23-193">Hello complémentaire *ServiceConfiguration.Cloud.cscfg* pour cet exemple se présente comme hello suivant.</span><span class="sxs-lookup"><span data-stu-id="95a23-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

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

<span data-ttu-id="95a23-194">Les paramètres équivalents JSON pour les machines virtuelles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="95a23-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="95a23-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95a23-195">Next steps</span></span>
<span data-ttu-id="95a23-196">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="95a23-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="95a23-197">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="95a23-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="95a23-198">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="95a23-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="95a23-199">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="95a23-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
