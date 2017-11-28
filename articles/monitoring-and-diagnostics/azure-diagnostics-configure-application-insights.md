---
title: "tooApplication de données toosend aaaConfigure Diagnostics Azure Insights | Documents Microsoft"
description: "Mettre à jour la configuration publique d’Azure Diagnostics hello données toosend tooApplication Insights."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="0f674-103">Envoyer des données de diagnostic du Service de cloud computing, machines virtuelles ou Service Fabric tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="0f674-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="0f674-104">Services de cloud computing, les ordinateurs virtuels, machines virtuelles identiques et Service Fabric utilisent hello Azure extension toocollect les données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="0f674-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="0f674-105">Diagnostics Azure envoie des données tooAzure tables de stockage.</span><span class="sxs-lookup"><span data-stu-id="0f674-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="0f674-106">Toutefois, vous pouvez également tous les de canal ou un sous-ensemble hello tooother d’emplacements de données à l’aide d’extension de Diagnostics Windows Azure 1.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0f674-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="0f674-107">Cet article décrit comment toosend les données à partir de hello tooApplication d’extension des Diagnostics Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="0f674-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="0f674-108">Explication de la configuration des diagnostics</span><span class="sxs-lookup"><span data-stu-id="0f674-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="0f674-109">Bonjour récepteurs d’extension 1.5 introduite les diagnostics Azure, qui sont des emplacements où vous pouvez envoyer des données de diagnostic supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0f674-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="0f674-110">Exemple de configuration d’un récepteur pour Application Insights :</span><span class="sxs-lookup"><span data-stu-id="0f674-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="0f674-111">Hello **récepteur** *nom* attribut est une valeur de chaîne qui identifie de façon unique le récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="0f674-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="0f674-112">Hello **ApplicationInsights** élément spécifie la clé d’instrumentation de hello ressource Application insights où hello des données de diagnostics Azure est envoyé.</span><span class="sxs-lookup"><span data-stu-id="0f674-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="0f674-113">Si vous n’avez pas une ressource Application Insights existante, consultez [créer une ressource Application Insights](../application-insights/app-insights-create-new-resource.md) pour plus d’informations sur la création d’une ressource et l’obtention de clé d’instrumentation hello.</span><span class="sxs-lookup"><span data-stu-id="0f674-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="0f674-114">Si vous développez un service cloud avec le kit SDK Azure 2.8 et ultérieur, cette clé d’instrumentation est automatiquement renseignée.</span><span class="sxs-lookup"><span data-stu-id="0f674-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="0f674-115">valeur de Hello est basée sur hello **APPINSIGHTS_INSTRUMENTATIONKEY** de configuration de service lors de la compression de projet de Service Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0f674-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="0f674-116">Consultez [problèmes de Service de cloud computing utilisez Application Insights avec Azure Diagnostics tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="0f674-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="0f674-117">Hello **canaux** élément contient un ou plusieurs **canal** éléments.</span><span class="sxs-lookup"><span data-stu-id="0f674-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="0f674-118">Hello *nom* attribut identifie de façon unique les toothat canal fait référence.</span><span class="sxs-lookup"><span data-stu-id="0f674-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="0f674-119">Hello *loglevel* vous permet de spécifier le niveau de journal hello qui hello canal permet d’attribut.</span><span class="sxs-lookup"><span data-stu-id="0f674-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="0f674-120">niveaux de journal disponibles Hello dans l’ordre de la plupart des informations de tooleast sont :</span><span class="sxs-lookup"><span data-stu-id="0f674-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="0f674-121">Détaillé</span><span class="sxs-lookup"><span data-stu-id="0f674-121">Verbose</span></span>
        - <span data-ttu-id="0f674-122">Information</span><span class="sxs-lookup"><span data-stu-id="0f674-122">Information</span></span>
        - <span data-ttu-id="0f674-123">Avertissement</span><span class="sxs-lookup"><span data-stu-id="0f674-123">Warning</span></span>
        - <span data-ttu-id="0f674-124">Erreur</span><span class="sxs-lookup"><span data-stu-id="0f674-124">Error</span></span>
        - <span data-ttu-id="0f674-125">Critique</span><span class="sxs-lookup"><span data-stu-id="0f674-125">Critical</span></span>

<span data-ttu-id="0f674-126">Un canal agit comme un filtre et vous permet de tooselect journal spécifique niveaux toosend toohello cible récepteur.</span><span class="sxs-lookup"><span data-stu-id="0f674-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="0f674-127">Par exemple, vous pourriez collecter des journaux détaillés et envoyez-le toostorage, mais uniquement le récepteur de toohello erreurs d’envoi.</span><span class="sxs-lookup"><span data-stu-id="0f674-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="0f674-128">Hello graphique suivant illustre cette relation.</span><span class="sxs-lookup"><span data-stu-id="0f674-128">hello following graphic shows this relationship.</span></span>

![Configuration publique des diagnostics](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="0f674-130">Hello graphique suivant résume les valeurs de configuration hello et leur fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="0f674-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="0f674-131">Vous pouvez inclure plusieurs récepteurs dans la configuration de hello à différents niveaux dans la hiérarchie de hello.</span><span class="sxs-lookup"><span data-stu-id="0f674-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="0f674-132">récepteur de Hello au niveau supérieur de hello agit comme un paramètre global et hello une spécifiée dans hello individuel élément agit comme un paramètre global toothat de remplacement.</span><span class="sxs-lookup"><span data-stu-id="0f674-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Récepteurs de diagnostics - Configuration avec Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="0f674-134">Exemple de configuration complète de récepteur</span><span class="sxs-lookup"><span data-stu-id="0f674-134">Complete sink configuration example</span></span>
<span data-ttu-id="0f674-135">Voici un exemple complet de la configuration publique de hello fichier</span><span class="sxs-lookup"><span data-stu-id="0f674-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="0f674-136">envoie toutes les erreurs tooApplication Insights (spécifié au hello **DiagnosticMonitorConfiguration** nœud)</span><span class="sxs-lookup"><span data-stu-id="0f674-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="0f674-137">envoie également les journaux détaillés de niveau pour hello journaux des applications (spécifié au hello **journaux** nœud).</span><span class="sxs-lookup"><span data-stu-id="0f674-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="0f674-138">Dans la configuration précédente de hello, hello lignes suivantes offre hello suivant significations :</span><span class="sxs-lookup"><span data-stu-id="0f674-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="0f674-139">Envoyer toutes les données hello qui sont collectées par les diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="0f674-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="0f674-140">Envoyer uniquement les journaux toohello Application Insights intercepteur d’erreurs</span><span class="sxs-lookup"><span data-stu-id="0f674-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="0f674-141">Application Verbose enregistre tooApplication Insights d’envoi</span><span class="sxs-lookup"><span data-stu-id="0f674-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="0f674-142">Limites</span><span class="sxs-lookup"><span data-stu-id="0f674-142">Limitations</span></span>

- <span data-ttu-id="0f674-143">**Les canaux consignent uniquement le type et non les compteurs de performances.**</span><span class="sxs-lookup"><span data-stu-id="0f674-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="0f674-144">Si vous spécifiez un canal comprenant un élément compteur de performances, il est ignoré.</span><span class="sxs-lookup"><span data-stu-id="0f674-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="0f674-145">**niveau de journal Hello pour un canal ne peut pas dépasser le niveau de journal hello pour celles collectées par les diagnostics Azure.**</span><span class="sxs-lookup"><span data-stu-id="0f674-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="0f674-146">Par exemple, vous ne peut pas collecter les erreurs du journal des applications dans l’élément de journaux hello et essayez de récepteur d’Application Insight toohello toosend journaux détaillés.</span><span class="sxs-lookup"><span data-stu-id="0f674-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="0f674-147">Hello *scheduledTransferLogLevelFilter* attribut doit toujours collecter égal ou davantage de journaux hello journaux que vous essayez de toosend tooa récepteur.</span><span class="sxs-lookup"><span data-stu-id="0f674-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="0f674-148">**Impossible d’envoyer des données blob collectées par tooApplication d’extension des diagnostics Azure Insights.**</span><span class="sxs-lookup"><span data-stu-id="0f674-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="0f674-149">Par exemple, quoi que ce soit spécifié sous hello *répertoires* nœud.</span><span class="sxs-lookup"><span data-stu-id="0f674-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="0f674-150">Pour les vidages sur incident hello réel vidage est envoyée tooblob stockage et uniquement une notification qui hello vidage sur incident a été générée sont envoyé tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="0f674-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f674-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f674-151">Next Steps</span></span>
* <span data-ttu-id="0f674-152">Découvrez comment trop[afficher vos informations de diagnostic Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0f674-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="0f674-153">Utilisez [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello extension Azure diagnostics pour votre application.</span><span class="sxs-lookup"><span data-stu-id="0f674-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="0f674-154">Utilisez [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello extension Azure diagnostics pour votre application</span><span class="sxs-lookup"><span data-stu-id="0f674-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
