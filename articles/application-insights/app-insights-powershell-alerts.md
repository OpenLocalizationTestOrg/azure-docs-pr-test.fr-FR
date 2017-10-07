---
title: alertes de tooset aaaUse Powershell dans Application Insights | Documents Microsoft
description: "Automatiser la configuration des e-mails de tooget Application Insights sur les modifications de métriques."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Utilisez PowerShell tooset alertes dans Application Insights
Vous pouvez automatiser la configuration de hello de [alertes](app-insights-alerts.md) dans [Application Insights](app-insights-overview.md).

En outre, vous pouvez [définir webhooks tooautomate votre alerte tooan de réponse](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Si vous souhaitez que les ressources toocreate et des alertes sur hello même temps, envisagez de [à l’aide d’un modèle Azure Resource Manager](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Installation unique
Si vous n’avez pas utilisé précédemment PowerShell avec votre abonnement Azure :

Installez le module de Azure Powershell de hello sur ordinateur hello où vous souhaitez les scripts toorun hello.

* Installez le programme [Microsoft Web Platform Installer (v5 ou version ultérieure)](http://www.microsoft.com/web/downloads/platform.aspx).
* Utiliser tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>Se connecter tooAzure
Démarrer PowerShell d’Azure et [connecter tooyour abonnement](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Obtention d’alertes
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Ajout d’alerte
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Exemple 1
M’avertir si les demandes de tooHTTP de réponse du serveur hello, moyenne plus de 5 minutes, est inférieure à 1 seconde. Ma ressource Application Insights est appelée IceCreamWebApp et se trouve dans le groupe de ressources Fabrikam. Je suis propriétaire hello Hello abonnement Azure.

Hello GUID est l’ID d’abonnement hello (pas hello clé d’instrumentation de l’application hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Exemple 2
J’ai une application dans laquelle utiliser [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport une mesure nommée « salesPerHour ». Envoyer un courrier électronique toomy collègues si « salesPerHour » est inférieur à 100, en moyenne plus de 24 heures.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

Hello même règle peut être utilisé pour la métrique de hello signalées à l’aide de hello [paramètre de mesure](app-insights-api-custom-events-metrics.md#properties) de suivi d’un autre appel de TrackEvent ou trackPageView.

## <a name="metric-names"></a>Noms de métrique
| Nom de métrique | Nom d’écran | Description |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Exceptions du navigateur |Nombre d’exceptions non interceptées levées dans le navigateur de hello. |
| `basicExceptionServer.count` |Exceptions de serveur |Nombre d’exceptions non gérées levées par une application hello |
| `clientPerformance.clientProcess.value` |Temps de traitement du client |Temps écoulé entre la réception hello dernier octet d’un document jusqu'à ce que le chargement de DOM hello. Les demandes asynchrones peuvent encore être en cours de traitement. |
| `clientPerformance.networkConnection.value` |Temps de connexion au réseau pour le chargement de page |Navigateur de hello temps prend tooconnect toohello réseau. Peut être 0 en cas de mise en cache. |
| `clientPerformance.receiveRequest.value` |Temps de réception de réponse |Temps écoulé entre l’envoi demande toostarting tooreceive réponse de navigateur. |
| `clientPerformance.sendRequest.value` |Temps d’envoi de demande |Temps nécessaire à la demande de toosend de navigateur. |
| `clientPerformance.total.value` |Temps de chargement de la page de navigateur |Temps s’écoulant entre la demande de l’utilisateur et le chargement du DOM, des feuilles de style, des scripts et des images. |
| `performanceCounter.available_bytes.value` |Mémoire disponible |Mémoire physique immédiatement disponible pour un processus ou pour une utilisation du système. |
| `performanceCounter.io_data_bytes_per_sec.value` |Taux d’E/S du processus |Nombre total d’octets par seconde et toofiles écrite, réseau et périphériques. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |Taux d’exceptions |Exceptions levées par seconde. |
| `performanceCounter.percentage_processor_time.value` |Processeur de processus |Hello pourcentage de temps de tous les threads de processus utilisé par les instructions tooexecution du processeur hello pour les processus des applications hello. |
| `performanceCounter.percentage_processor_total.value` |Temps processeur |pourcentage de Hello de temps qui hello processeur passe dans des threads non inactifs. |
| `performanceCounter.process_private_bytes.value` |Octets privés du processus |Mémoire exclusivement affectée toohello surveiller le processus de l’application. |
| `performanceCounter.request_execution_time.value` |Durée d’exécution de la demande ASP.NET |Durée d’exécution de la demande la plus récente hello. |
| `performanceCounter.requests_in_application_queue.value` |Demandes ASP.NET en file d’attente d’exécution |Longueur de file d’attente de demandes d’application hello. |
| `performanceCounter.requests_per_sec.value` |Taux de demandes ASP.NET |Taux de toutes les demandes application toohello par seconde à partir de ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Défaillances de dépendance |Nombre d’échecs des appels effectués par hello server application tooexternal des ressources. |
| `request.duration` |Temps de réponse du serveur |Temps écoulé entre la réception d’une demande HTTP et la fin de l’envoi de réponse de hello. |
| `request.rate` |Taux de demandes |Taux de toutes les demandes d’application toohello par seconde. |
| `requestFailed.count` |Demandes ayant échoué |Nombre de requêtes HTTP qui ont abouti au code de réponse > = 400 |
| `view.count` |Affichages de page |Nombre de demandes d’utilisateur client pour une page web. Le trafic synthétique est filtré. |
| {nom de votre mesure personnalisée} |{nom de votre mesure} |Votre valeur métrique signalés par [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) ou Bonjour [paramètre de mesures d’un appel de suivi](app-insights-api-custom-events-metrics.md#properties). |

métriques de Hello sont envoyés par les modules de télémétrie différents :

| Groupe de mesures | Module du collecteur |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>view |[JavaScript du navigateur](app-insights-javascript.md) |
| performanceCounter |[Performances](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Dépendance](app-insights-configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[Demande serveur](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhooks
Vous pouvez [automatiser votre alerte tooan de réponse](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure appelle une adresse web de votre choix lorsqu’une alerte est déclenchée.

## <a name="see-also"></a>Voir aussi
* [Script tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Créer des ressources Application Insights et de test Web  templates à partir de modèles (en anglais)](app-insights-powershell.md)
* [Automatiser le couplage Insights tooApplication de Microsoft Azure Diagnostics](app-insights-powershell-azure-diagnostics.md)
* [Automatiser votre alerte tooan de réponse](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
