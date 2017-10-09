---
title: "l’intégration avec Application Insights aaaSCOM | Documents Microsoft"
description: "Si vous êtes un utilisateur SCOM, analysez les performances et diagnostiquez les problèmes avec Application Insights. Tableaux de bord complets, alertes intelligentes, requêtes analytiques et outils de diagnostic efficaces."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Analyse des performances des applications à l’aide d’Application Insights pour SCOM
Si vous utilisez System Center Operations Manager (SCOM) toomanage vos serveurs, vous pouvez surveiller les performances et diagnostiquer les problèmes de performances à l’aide de hello de [Azure Application Insights](app-insights-asp-net.md). Application Insights analyse les demandes entrantes de votre application web, les appels SQL et REST sortants, les exceptions et les suivis de journal. Elle fournit des tableaux de bord avec des graphiques de mesure et des alertes intelligentes, ainsi que des requêtes analytiques et des outils de recherche de diagnostic efficaces sur ces données de télémétrie. 

Vous pouvez activer l’analyse Application Insights à l’aide d’un pack d’administration SCOM.

## <a name="before-you-start"></a>Avant de commencer
Nous partons de l’hypothèse suivante :

* Serveurs web, vous êtes familiarisé avec SCOM et que vous utilisez SCOM 2012 R2 ou 2016 toomanage votre IIS.
* Vous avez déjà installé sur vos serveurs d’une application web que vous souhaitez toomonitor avec Application Insights.
* La version de l’infrastructure de l’application est .NET 4.5 ou une version ultérieure.
* Vous avez accès tooa abonnement dans [Microsoft Azure](https://azure.com) et peuvent se connecter toohello [portail Azure](https://portal.azure.com). Votre entreprise peut disposer d’un abonnement et pouvez ajouter vos tooit de compte Microsoft.

(équipe de développement hello peut générer hello [Application Insights SDK](app-insights-asp-net.md) dans l’application web hello. Cette instrumentation en cours de création lui donne plus de flexibilité dans l’écriture des données de télémétrie personnalisées. Toutefois, il n’a aucune importance : vous pouvez suivre les étapes de hello décrites ici, avec ou sans hello SDK intégré.)

## <a name="one-time-install-application-insights-management-pack"></a>(Une fois) Installer le pack d’administration Application Insights
Sur l’ordinateur hello sur lequel vous exécutez Operations Manager :

1. Désinstallez toute ancienne version du Pack d’administration de hello :
   1. Dans Operations Manager, ouvrez Administration, Packs d’administration. 
   2. Supprimez l’ancienne version de hello.
2. Téléchargez et installez le pack d’administration hello du catalogue de hello.
3. Redémarrez Operations Manager.

## <a name="create-a-management-pack"></a>Créer un pack d’administration
1. Dans Operations Manager, ouvrez **Création**, **.NET...with Application Insights** (.NET... avec Application Insights), **Assistant Ajout d’analyse**, et choisissez à nouveau **.NET...with Application Insights** (.NET... avec Application Insights).
   
    ![](./media/app-insights-scom/020.png)
2. Configuration du nom hello après votre application. (Vous avez tooinstrument une application à la fois).
   
    ![](./media/app-insights-scom/030.png)
3. Sur hello même page de l’Assistant, créez une nouvelle gestion pack, ou sélectionnez un pack que vous avez créé pour Application Insights.
   
     (hello Application Insights [Pack d’administration](https://technet.microsoft.com/library/cc974491.aspx) est un modèle à partir de laquelle vous créez une instance. Vous pouvez réutiliser hello même instance ultérieurement.)

    ![Dans l’onglet Propriétés générales de hello, tapez le nom de hello de l’application hello. Cliquez sur Nouveau et saisissez un nom pour un pack d’administration. Cliquez sur OK, puis sur Suivant.](./media/app-insights-scom/040.png)

1. Choisissez une application que vous souhaitez toomonitor. recherche de la fonctionnalité de recherche Hello parmi les applications installées sur vos serveurs.
   
    ![Sur l’onglet tooMonitor, cliquez sur Ajouter, tapez une partie du nom de l’application hello, cliquez sur Rechercher, choisissez application hello, puis ajouter, OK.](./media/app-insights-scom/050.png)
   
    champ de Hello facultatif analyse étendue peut être utilisé toospecify un sous-ensemble de vos serveurs, si vous ne souhaitez pas application hello de toomonitor dans tous les serveurs.
2. Sur la page d’Assistant suivante hello, vous devez tout d’abord fournir toosign de vos informations d’identification dans tooMicrosoft Azure.
   
    Dans cette page, vous choisissez de ressource d’Application Insights hello où vous souhaitez toobe de données de télémétrie hello analysé et affiché. 
   
   * Si l’application hello a été configurée pour Application Insights au cours du développement, sélectionnez la ressource existante.
   * Sinon, créez une ressource nommée pour une application hello. S’il existe des autres applications qui sont des composants de hello même système, placez-les dans hello même groupe de ressources, toomanage plus facilement des données de télémétrie toohello accès toomake.
     
     Vous pouvez modifier ces paramètres plus tard.
     
     ![Dans l’onglet Application Insights settings (Paramètres d’Application Insights), cliquez sur « se connecter » et indiquez vos informations d’identification de compte Microsoft pour Azure. Choisissez ensuite un abonnement, un groupe de ressources et une ressource.](./media/app-insights-scom/060.png)
3. Assistant hello terminée.
   
    ![Click Create](./media/app-insights-scom/070.png)

Répétez cette procédure pour chaque application que vous souhaitez toomonitor.

Si vous avez besoin de paramètres de toochange ultérieurement, ouvrez à nouveau les propriétés de hello Hello surveiller à partir de la fenêtre de création de hello.

![Dans la fenêtre de création, sélectionnez .NET Application Performance Monitoring with Application Insights (Analyse des performances des applications .NET avec Application Insights), choisissez votre analyse et cliquez sur Propriétés.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Vérifier l’analyse
Moniteur de Hello que vous avez installé la recherche de votre application sur chaque serveur. Dans ce cas, il trouve l’application hello, il configure Application Insights Status Monitor toomonitor hello application. Si nécessaire, il installe tout d’abord le moniteur d’état sur le serveur de hello.

Vous pouvez vérifier les instances de l’application hello a trouvé :

![Dans la fenêtre d’analyse, ouvrez Application Insights.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Afficher les données de télémétrie dans Application Insights
Bonjour [portail Azure](https://portal.azure.com), parcourir les ressources toohello pour votre application. Vous [pouvez voir les graphiques affichant les données de télémétrie](app-insights-dashboards.md) depuis votre application. (Si elle n’a pas affichées sur la page principale de hello encore, cliquez sur flux Live de métriques).

## <a name="next-steps"></a>Étapes suivantes
* [Configurer un tableau de bord](app-insights-dashboards.md) graphiques de données plus importantes toobring hello ensemble cela et les autres applications d’analyse.
* [En savoir plus sur les métriques](app-insights-metrics-explorer.md)
* [Configurer des alertes](app-insights-alerts.md)
* [Diagnostiquer des problèmes de performances](app-insights-detect-triage-diagnose.md)
* [Requêtes Analytics efficaces](app-insights-analytics.md)
* [Tests web de disponibilité](app-insights-monitor-web-app-availability.md)

