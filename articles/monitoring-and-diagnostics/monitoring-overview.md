---
title: aaaMonitoring dans Microsoft Azure | Documents Microsoft
description: "Choix lorsque vous souhaitez toomonitor n’est pas défini dans Microsoft Azure. Azure Monitor, Application Insights Log Analytics"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Vue d’ensemble de l’analyse dans Microsoft Azure
Cet article fournit une vue d’ensemble des outils disponibles pour la surveillance de Microsoft Azure. Il s’applique également
- surveillance des applications en cours d’exécution dans Microsoft Azure 
- outils/services s’exécutant en dehors d’Azure pouvant surveiller des objets dans Azure. 

Elle explique hello divers produits et services disponibles et comment ils fonctionnent ensemble. Il peut vous aider toodetermine les outils les plus appropriées pour vous dans les cas.  

## <a name="why-use-monitoring-and-diagnostics"></a>Pourquoi utiliser la surveillance et les diagnostics ?

Les problèmes de performances dans votre application cloud peuvent affecter votre entreprise. Avec plusieurs composants interconnectés et de nouvelles versions fréquentes, des dégradations peuvent se produire à tout moment. Et si vous développez une application, vos utilisateurs découvrent généralement des problèmes que vous n’avez pas trouvés dans le test. Vous devez savoir immédiatement sur ces problèmes et disposer des outils de diagnostic et résolution des problèmes de hello. Microsoft Azure a une gamme d’outils permettant d’identifier ces problèmes.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Comment surveiller mes applications cloud Azure ?

Il existe une gamme d’outils pour la surveillance des services et applications Azure. Certaines de leurs fonctionnalités se chevauchent. C’est en partie pour des raisons historiques et en partie en raison de toohello flou entre le développement et le fonctionnement d’une application. 

Voici les outils principaux hello :

-   **Azure Monitor** est l’outil de base pour la surveillance des services s’exécutant sur Azure. Il vous fournit des données de niveau de l’infrastructure sur débit hello d’un service et un hello entourant l’environnement. Si vous gérez vos applications dans Azure, vous décidez si tooscale vers le haut ou vers le bas des ressources, analyse d’Azure vous donne ensuite ce que vous utilisez toostart.

-   **Application Insights** peut être utilisé pour le développement et comme solution de surveillance de la production. Il fonctionne en installant un package dans votre application et vous donne donc une vue plus interne de ce qui se passe. Ses données comprennent les temps de réponse des dépendances, les traces des exceptions, le débogage des captures instantanées et les profils d’exécution. Il fournit des outils de smart puissants pour l’analyse de ces données de télémétrie deux toohelp vous déboguez une application et les toohelp vous comprenez ce que font les utilisateurs avec lui. Vous pouvez savoir si un pic dans le temps de réponse échéance toosomething dans une application ou un problème passait externe. Si vous utilisez Visual Studio et l’application hello est en cause, vous pouvez dirigé toohello droite problème ou les lignes de code pour vous pouvez de le résoudre.  

-   **Ouvrez une session Analytique** est destiné à ceux qui ont besoin de maintenance de plan et de performances tootune sur les applications qui s’exécutent en production. Il est basé dans Azure. Il collecte et agrège les données de nombreuses sources, mais avec un délai de 10 minutes too15. Il fournit une solution de gestion informatique globale holistique pour Azure, en local et dans les infrastructures cloud tierces (par exemple, Amazon Web Services). Fournit des outils plus riches tooanalyze données sur d’autres sources, permet des requêtes complexes sur tous les journaux et pouvez alertes sur les conditions spécifiées.  Vous pouvez même collecter des données personnalisées dans son référentiel central pour les interroger et visualiser. 

-   **System Center Operations Manager (SCOM)** pour gérer et surveiller les installations cloud à grande échelle. Vous le connaissez peut-être déjà comme outil de gestion local pour Windows Server en local et les solutions cloud basées sur Hyper-V, mais il peut également s’intégrer à et gérer des applications Azure. Entre autres choses, il peut installer Application Insights sur des applications en direct existantes.  Si une application est en panne, vous en êtes informé sous quelques secondes. Notez que Log Analytics ne remplace pas SCOM. Les deux fonctionnent bien ensemble.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>L’accès à la surveillance dans hello portail Azure
Tous les services de surveillance Azure sont maintenant disponibles dans un seul volet de l’interface utilisateur. Pour plus d’informations sur la façon de tooaccess cette zone, consultez [prise en main Azure analyse](monitoring-get-started.md). 

Vous pouvez également accéder à des fonctions de surveillance pour des ressources spécifiques en mettant en surbrillance ces ressources et en explorant leurs options de surveillance. 

## <a name="examples-of-when-toouse-which-tool"></a>Exemples de situations dans lesquelles toouse qui outil 

Hello les sections suivantes montrent quelques scénarios de base et les outils qui doivent être utilisés ensemble. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Scénario 1 : correction des erreurs dans une application Azure en développement   

**est préférable de Hello toouse Application Insights, analyse d’Azure et Visual Studio d’ensemble**

Azure fournit désormais la puissance du débogueur de Visual Studio hello dans le cloud de hello hello. Configurer tooApplication de télémétrie toosend moniteur Azure Insights. Activer hello de tooinclude Visual Studio Application Insights SDK dans votre application. Une fois dans Application Insights, vous pouvez utiliser toodiscover de mappage de l’Application hello visuellement les parties de votre application en cours d’exécution sont défectueuses ou non. Corrigez les parties qui ne sont pas intègres, les erreurs et les exceptions déjà disponibles pour exploration. Vous pouvez utiliser hello analytique différents dans toogo Application Insights plus approfondis. Si vous n’êtes pas certain de l’erreur de hello, vous pouvez utiliser tootrace de débogueur Visual Studio hello en point de code et code confidentiel plus précisément un problème. 

Pour plus d’informations, consultez [d’analyse des applications Web](../application-insights/app-insights-azure-web-apps.md) et faire référence de table toohello de sommaire à gauche de hello pour obtenir des instructions sur les différents types d’applications et les langues.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Scénario 2 : déboguer une application web Azure .NET pour les erreurs qui apparaissent uniquement en production 

> [!NOTE]
> Ces fonctionnalités sont en version préliminaire. 

**Hello meilleure option est toouse Application Insights et si possible Visual Studio pour hello complète expérience de débogage.**

Utilisez hello Application Insights instantané débogueur toodebug votre application. Lorsqu’un certain seuil d’erreur se produit avec les composants de production, système de hello capture automatiquement les données de télémétrie de windows appelée « instantanés ». Hello quantité capturée est sécurisée pour un cloud de production, car elle est petite suffisamment pas tooaffect performances, mais le suivi de tooallow assez important.  système de Hello peut capturer plusieurs instantanés. Vous pouvez examiner un point dans le temps dans hello portail Azure ou utiliser Visual Studio pour une expérience complète hello. Avec Visual Studio, les développeurs peuvent parcourir cet instantané comme s’ils effectuaient le débogage en temps réel. Les paramètres, la mémoire, les variables locales et les trames sont tous disponibles. Les développeurs doivent pouvoir accéder aux données de production toothis via un rôle RBAC.  

Pour plus d’informations, consultez [Débogage d’instantané](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Scénario 3 : déboguer une application Windows Azure qui utilise des conteneurs ou microservices 

**Identique au scénario 1. Utilisez Visual Studio, Application Insights et Azure Monitor ensemble** Application Insights prend également en charge la collecte des données de télémétrie des processus qui s’exécutent dans des conteneurs et microservices (Kubernetes, Docker, Azure Service Fabric). Pour plus d’informations, [regardez cette vidéo sur le débogage des conteneurs et microservices](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Scénario 4 : corriger les problèmes de performances dans votre application Azure

Hello [profileur d’Application Insights](../application-insights/app-insights-profiler.md) est conçue toohelp résoudre ces types de problèmes. Vous pouvez identifier et résoudre les problèmes de performances pour les applications qui s’exécutent dans App Service (applications web, applications logiques, applications mobiles, applications d’API) et d’autres ressources de calcul comme les machines virtuelles, les jeux de mise à l’échelle de machines virtuelles, les services de cloud computing et Service Fabric. 

> [!NOTE]
> Capacité tooprofile ordinateurs virtuels, machines virtuelles identiques (mise), Services de cloud computing et les Services de Fabric est en version préliminaire.   

En outre, vous sont proactive informé par courrier électronique sur certains types d’erreurs, telles que des délais de chargement lent des pages, par un outil de détection actives hello.  Vous n’avez pas besoin toodo toute configuration de cet outil. Pour plus d’informations, consultez [Détection intelligente - anomalies de performances](../application-insights/app-insights-proactive-performance-diagnostics.md) et [Détection intelligente - anomalies de performances](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur

* [Azure Monitor dans une vidéo de l’Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Prise en main d’Azure Monitor](monitoring-get-started.md)
* [Diagnostics Azure](../azure-diagnostics.md) si vous essayez de toodiagnose des problèmes dans votre Service Cloud, l’ordinateur virtuel, machine virtuelle à l’échelle définie ou le Service application de l’ensemble fibre optique.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) si vous essayez de toodiagnostic des problèmes dans votre application de Service Web de l’application.
* [Ouvrez une session Analytique](https://azure.microsoft.com/documentation/services/log-analytics/) et hello [Operations Management Suite](https://www.microsoft.com/oms/) solution de surveillance de la production