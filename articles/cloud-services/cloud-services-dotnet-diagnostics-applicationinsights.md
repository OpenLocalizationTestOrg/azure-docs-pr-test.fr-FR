---
title: "aaaTroubleshoot les Services de Cloud à l’aide d’Application Insights | Documents Microsoft"
description: "Découvrez comment le service de cloud computing tootroubleshoot problèmes à l’aide de données de tooprocess Application Insights à partir d’Azure Diagnostics."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Résoudre les problèmes de Cloud Services à l’aide d’Application Insights
Avec [Azure SDK 2.8](https://azure.microsoft.com/downloads/) et extension des diagnostics Windows Azure 1.5, vous pouvez envoyer des données de Diagnostics Windows Azure pour votre Service Cloud directement tooApplication Insights. Hello journaux collectés par les Diagnostics Azure&mdash;, y compris les journaux des applications, les journaux des événements Windows, les journaux ETW et les compteurs de performance&mdash;peuvent être envoyés tooApplication Insights. Vous pouvez ensuite visualiser ces informations dans l’interface utilisateur du portail Application Insights hello. Vous pouvez ensuite utiliser hello Application Insights SDK tooget vue d’ensemble de mesures et les fichiers journaux qui proviennent de votre application, ainsi que de système de hello et de données au niveau de l’infrastructure qui proviennent d’Azure Diagnostics.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Configurer les Diagnostics Azure toosend données tooApplication Insights
Suivez ces tooset étapes de votre tooApplication de données cloud service projet toosend Diagnostics Azure Insights.

1. Dans l’Explorateur de solutions Visual Studio, cliquez sur un rôle et sélectionnez **propriétés** Concepteur de rôle tooopen hello.

    ![Propriétés de rôle de l'Explorateur de solutions][1]

2. Bonjour **Diagnostics** section hello du Concepteur de rôle, sélectionnez hello **envoyer des données de diagnostics tooApplication Insights** option.

    ![Concepteur de rôle envoyez des diagnostics insights tooapplication de données][2]

3. Dans la boîte de dialogue hello qui s’affiche, sélectionnez la ressource Application Insights hello que données de diagnostics Windows Azure hello toosend à. boîte de dialogue Hello vous permet de tooselect une ressource Application Insights existante à partir de votre abonnement ou toomanually spécifier une clé d’instrumentation pour une ressource Application Insights. Pour plus d’informations sur la création d’une ressource Application Insights, consultez [Créer une ressource Application Insights](../application-insights/app-insights-create-new-resource.md).

    ![sélectionner une ressource Application Insights][3]

    Une fois que vous avez ajouté la ressource d’Application Insights hello, clé d’instrumentation hello pour cette ressource est stocké comme un paramètre de configuration de service avec le nom de hello **APPINSIGHTS_INSTRUMENTATIONKEY**. Vous pouvez modifier ce paramètre de configuration pour chaque configuration ou environnement de service. toodo, sélectionnez une autre configuration de hello **Configuration du Service** liste et spécifiez une nouvelle clé d’instrumentation pour cette configuration.

    ![sélectionner une configuration de service][4]

    Hello **APPINSIGHTS_INSTRUMENTATIONKEY** paramètre de configuration est utilisé par extension de diagnostics de Visual Studio tooconfigure hello avec les informations de ressource de Application Insights appropriées hello lors de la publication. paramètre de configuration Hello est un moyen pratique de définir des clés d’instrumentation différentes pour différentes configurations de service. Visual Studio traduire ce paramètre et l’insérer dans la configuration publique d’extension diagnostics hello pendant hello processus de publication. processus de hello toosimplify de configuration de l’extension de diagnostics hello avec PowerShell, sortie hello du package à partir de Visual Studio contient également hello publique XML de configuration avec la clé d’instrumentation hello approprié Application Insights. fichiers de configuration publics Hello sont créés dans le dossier d’Extensions hello et suivent le modèle de hello *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Les déploiements PowerShell peuvent utiliser cette toomap modèle chaque rôle tooa de configuration.

4) toosend de diagnostics Azure tooconfigure tous les compteurs de performance et les journaux des erreurs de niveau collectées par tooApplication de l’agent de diagnostics Windows Azure hello Insights, activer hello **envoyer des données de diagnostics tooApplication Insights** option. 

    Si vous souhaitez toofurther configurer les données envoyées tooApplication Insights, vous devez modifier manuellement hello *diagnostics.wadcfgx* fichier pour chaque rôle. Consultez [tooApplication de données toosend configurer les Diagnostics Azure Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn plus d’informations sur la mise à jour manuelle de configuration de hello.

Lorsque le service cloud hello est toosend configuré les diagnostics Azure données tooapplication insights, vous pouvez la déployer tooAzure normalement, assurant hello extension Azure diagnostics est activée. Pour plus d’informations, consultez [Publication d’un service cloud en utilisant Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Affichage des données des diagnostics Azure dans Application Insights
Hello télémétrie de diagnostic Azure s’affiche dans hello Application Insights ressource configurée pour votre service cloud.

Types de journaux de diagnostics Azure mappent les concepts de Insights tooApplication des façons suivantes :

* Les compteurs de performances s’affichent en tant que métriques personnalisées dans Application Insights.
* Les journaux des événements Windows s’affichent en tant que traces et événements personnalisés dans Application Insights.
* Les journaux d’applications, les journaux ETW et les journaux d’infrastructure de diagnostics éventuels s’affichent en tant que traces dans Application Insights.

tooview des données de diagnostics Azure dans Application Insights, effectuez l’une des suivantes de hello :

* Utilisez [Metrics explorer](../application-insights/app-insights-metrics-explorer.md) toovisualize des performances personnalisées compteurs ou le nombre des différents types d’événements du journal des événements Windows.

    ![Métriques personnalisées dans Metrics Explorer][5]

* Utilisez [recherche](../application-insights/app-insights-diagnostic-search.md) toosearch dans les journaux de trace hello envoyés par les Diagnostics Windows Azure. Par exemple, si une exception non gérée a provoqué hello rôle toocrash et recyclage, plus d’informations sur l’exception de hello s’affiche dans hello *Application* canal de *journal des événements Windows*. Vous pouvez utiliser des toolook de recherche à hello erreur du journal des événements Windows et obtenir la trace de pile complet hello pour hello exception toohelp rechercher hello cause du problème de hello.

    ![Rechercher dans les traces][6]

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter un service de cloud hello Application Insights SDK tooyour](../application-insights/app-insights-cloudservices.md) toosend des données sur les demandes, les exceptions, les dépendances et les données de télémétrie personnalisées à partir de votre application. Lorsqu’elles sont combinées avec des données de Diagnostics Windows Azure hello, ces informations vous pouvez obtenir une vue complète de votre application et le système, tout en hello même ressource d’Application Insight.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
