---
title: "Configurer les diagnostics Azure pour envoyer des données à Application Insights | Microsoft Docs"
description: "Mettez à jour la configuration publique des diagnostics Azure pour envoyer des données à Application Insights."
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
ms.openlocfilehash: 7dd8c6e1fbfba2587aadb3410c3a769b57e06001
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a>Envoyer des données de diagnostic de service cloud, de machine virtuelle ou de Service Fabric à Application Insights
Les services cloud, les machines virtuelles, les groupes de machines virtuelles identiques et Service Fabric utilisent l’extension Azure Diagnostics pour collecter des données.  Les diagnostics Azure envoient les données dans des tables de stockage Azure.  Toutefois, vous pouvez également transmettre toutes les données ou un sous-ensemble de données vers d’autres emplacements à l’aide de l’extension Azure Diagnostics 1.5 ou version ultérieure.

Cet article décrit comment envoyer des données à partir de l’extension Azure Diagnostics vers Application Insights.

## <a name="diagnostics-configuration-explained"></a>Explication de la configuration des diagnostics
L’extension des diagnostics Azure 1.5 a introduit des récepteurs, qui sont des emplacements supplémentaires où vous pouvez envoyer des données de diagnostic.

Exemple de configuration d’un récepteur pour Application Insights :

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
- L’attribut **Sink** *name* est une valeur de chaîne qui identifie de façon unique le récepteur.

- L’élément **ApplicationInsights** spécifie la clé d’instrumentation de la ressource Application Insights où les données des diagnostics Azure sont envoyées.
    - Si vous ne disposez pas d’une ressource Application Insights, consultez [Créer une ressource Application Insights](../application-insights/app-insights-create-new-resource.md) pour plus d’informations sur la création d’une ressource et l’obtention de la clé d’instrumentation.
    - Si vous développez un service cloud avec le kit SDK Azure 2.8 et ultérieur, cette clé d’instrumentation est automatiquement renseignée. La valeur est basée sur le paramètre de configuration de service **APPINSIGHTS_INSTRUMENTATIONKEY** lors de l’empaquetage du projet de service cloud. Consultez [Utiliser Application Insights avec les diagnostics Azure pour résoudre les problèmes de service cloud](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- L’élément **Channels** contient au moins un élément **Channel**.
    - L’attribut *name* fait référence uniquement à ce canal.
    - L’attribut *loglevel* vous permet de spécifier le niveau de consignation autorisé par le canal. Les niveaux de consignation disponibles sont, du plus informatif au moins informatif :
        - Détaillé
        - Information
        - Avertissement
        - Erreur
        - Critique

Un canal fonctionne comme un filtre et vous permet de sélectionner les niveaux de consignation spécifiques à envoyer au récepteur cible. Par exemple, vous pouvez collecter des journaux détaillés et les envoyer vers le stockage, mais envoyer uniquement les erreurs vers le récepteur.

Le graphique suivant illustre cette relation.

![Configuration publique des diagnostics](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Le graphique suivant résume les valeurs de configuration et leur fonctionnement. Vous pouvez inclure plusieurs récepteurs à la configuration à différents niveaux de la hiérarchie. Le récepteur spécifié au niveau supérieur fonctionne comme un paramètre global et celui spécifié au niveau des éléments individuels écrase ce paramètre global.

![Récepteurs de diagnostics - Configuration avec Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Exemple de configuration complète de récepteur
Voici un exemple complet de fichier de configuration publique qui
1. envoie toutes les erreurs à Application Insights (spécifiées au niveau du nœud **DiagnosticMonitorConfiguration**)
2. envoie également des journaux détaillés pour les journaux des applications (spécifiés au niveau du nœud **Logs**).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
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
Dans la configuration précédente, les lignes ci-dessous ont les significations suivantes :

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a>Envoyer toutes les données qui sont collectées par les diagnostics Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a>Envoyer uniquement les journaux d’erreurs au récepteur Application Insights

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a>Envoyer les journaux d’application détaillés à Application Insights

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Limitations

- **Les canaux consignent uniquement le type et non les compteurs de performances.** Si vous spécifiez un canal comprenant un élément compteur de performances, il est ignoré.
- **Le niveau de consignation d’un canal ne peut pas dépasser le niveau de consignation de ce qui est collecté par les diagnostics Azure.** Par exemple, vous ne pouvez pas collecter les erreurs de consignation des applications dans l’élément Journaux et tenter d’envoyer des journaux détaillés vers le journal de suivi Application Insight. L'attribut *scheduledTransferLogLevelFilter* doit toujours collecter au moins autant de journaux que ceux que vous essayez d'envoyer à un récepteur.
- **Vous ne pouvez pas envoyer des données blob collectées par l’extension des diagnostics Azure à Application Insights.** Par exemple, rien qui soit spécifié sous le nœud *Directories*. Pour les vidages sur incident, le vidage sur incident réel est toujours envoyé au stockage Blob et seule une notification de génération du vidage sur incident est envoyée à Application Insights.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment [visualiser vos informations de diagnostic Azure](https://docs.microsoft.com/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) dans Application Insights.
* Utilisez [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) pour activer l’extension des diagnostics Azure pour votre application.
* Utilisez [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) pour activer l'extension des diagnostics Azure pour votre application
