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
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Envoyer des données de diagnostic du Service de cloud computing, machines virtuelles ou Service Fabric tooApplication Insights
Services de cloud computing, les ordinateurs virtuels, machines virtuelles identiques et Service Fabric utilisent hello Azure extension toocollect les données de diagnostic.  Diagnostics Azure envoie des données tooAzure tables de stockage.  Toutefois, vous pouvez également tous les de canal ou un sous-ensemble hello tooother d’emplacements de données à l’aide d’extension de Diagnostics Windows Azure 1.5 ou version ultérieure.

Cet article décrit comment toosend les données à partir de hello tooApplication d’extension des Diagnostics Azure Insights.

## <a name="diagnostics-configuration-explained"></a>Explication de la configuration des diagnostics
Bonjour récepteurs d’extension 1.5 introduite les diagnostics Azure, qui sont des emplacements où vous pouvez envoyer des données de diagnostic supplémentaires.

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
- Hello **récepteur** *nom* attribut est une valeur de chaîne qui identifie de façon unique le récepteur de hello.

- Hello **ApplicationInsights** élément spécifie la clé d’instrumentation de hello ressource Application insights où hello des données de diagnostics Azure est envoyé.
    - Si vous n’avez pas une ressource Application Insights existante, consultez [créer une ressource Application Insights](../application-insights/app-insights-create-new-resource.md) pour plus d’informations sur la création d’une ressource et l’obtention de clé d’instrumentation hello.
    - Si vous développez un service cloud avec le kit SDK Azure 2.8 et ultérieur, cette clé d’instrumentation est automatiquement renseignée. valeur de Hello est basée sur hello **APPINSIGHTS_INSTRUMENTATIONKEY** de configuration de service lors de la compression de projet de Service Cloud hello. Consultez [problèmes de Service de cloud computing utilisez Application Insights avec Azure Diagnostics tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Hello **canaux** élément contient un ou plusieurs **canal** éléments.
    - Hello *nom* attribut identifie de façon unique les toothat canal fait référence.
    - Hello *loglevel* vous permet de spécifier le niveau de journal hello qui hello canal permet d’attribut. niveaux de journal disponibles Hello dans l’ordre de la plupart des informations de tooleast sont :
        - Détaillé
        - Information
        - Avertissement
        - Erreur
        - Critique

Un canal agit comme un filtre et vous permet de tooselect journal spécifique niveaux toosend toohello cible récepteur. Par exemple, vous pourriez collecter des journaux détaillés et envoyez-le toostorage, mais uniquement le récepteur de toohello erreurs d’envoi.

Hello graphique suivant illustre cette relation.

![Configuration publique des diagnostics](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Hello graphique suivant résume les valeurs de configuration hello et leur fonctionnement. Vous pouvez inclure plusieurs récepteurs dans la configuration de hello à différents niveaux dans la hiérarchie de hello. récepteur de Hello au niveau supérieur de hello agit comme un paramètre global et hello une spécifiée dans hello individuel élément agit comme un paramètre global toothat de remplacement.

![Récepteurs de diagnostics - Configuration avec Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Exemple de configuration complète de récepteur
Voici un exemple complet de la configuration publique de hello fichier
1. envoie toutes les erreurs tooApplication Insights (spécifié au hello **DiagnosticMonitorConfiguration** nœud)
2. envoie également les journaux détaillés de niveau pour hello journaux des applications (spécifié au hello **journaux** nœud).

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
Dans la configuration précédente de hello, hello lignes suivantes offre hello suivant significations :

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Envoyer toutes les données hello qui sont collectées par les diagnostics Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Envoyer uniquement les journaux toohello Application Insights intercepteur d’erreurs

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Application Verbose enregistre tooApplication Insights d’envoi

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Limites

- **Les canaux consignent uniquement le type et non les compteurs de performances.** Si vous spécifiez un canal comprenant un élément compteur de performances, il est ignoré.
- **niveau de journal Hello pour un canal ne peut pas dépasser le niveau de journal hello pour celles collectées par les diagnostics Azure.** Par exemple, vous ne peut pas collecter les erreurs du journal des applications dans l’élément de journaux hello et essayez de récepteur d’Application Insight toohello toosend journaux détaillés. Hello *scheduledTransferLogLevelFilter* attribut doit toujours collecter égal ou davantage de journaux hello journaux que vous essayez de toosend tooa récepteur.
- **Impossible d’envoyer des données blob collectées par tooApplication d’extension des diagnostics Azure Insights.** Par exemple, quoi que ce soit spécifié sous hello *répertoires* nœud. Pour les vidages sur incident hello réel vidage est envoyée tooblob stockage et uniquement une notification qui hello vidage sur incident a été générée sont envoyé tooApplication Insights.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[afficher vos informations de diagnostic Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) dans Application Insights.
* Utilisez [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello extension Azure diagnostics pour votre application.
* Utilisez [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello extension Azure diagnostics pour votre application
