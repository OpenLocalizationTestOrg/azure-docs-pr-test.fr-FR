---
title: "Démarrage rapide avec Azure Application Insights | Microsoft Docs"
description: Fournit des instructions permettant de configurer rapidement une application mobile pour la surveillance avec Application Insights et App Center
services: application-insights
keywords: 
author: numberbycolors
ms.author: daviste
ms.date: 10/05/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: 897c45322148aeb088f1ec2e7f8d9f46b58c71aa
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2017
---
# <a name="start-analyzing-your-mobile-app-with-app-center-and-application-insights"></a>Commencer à analyser votre application mobile avec App Center et Application Insights

Ce démarrage rapide vous guide tout au long de la connexion de l’instance App Center de votre application à Application Insights. Avec Application Insights, vous pouvez interroger, segmenter, filtrer et analyser vos données de télémétrie avec davantage d’outils puissants que ceux disponibles à partir du service [Analytics](https://docs.microsoft.com/mobile-center/analytics/) d’App Center.

## <a name="prerequisites"></a>Composants requis

Pour effectuer ce démarrage rapide, les éléments suivants sont requis :

- Un abonnement Azure.
- Une application iOS, Android, Xamarin, Universal Windows ou React Native.
 
Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="onboard-to-app-center"></a>Intégrer l’application à App Center

Avant de pouvoir utiliser Application Insights avec votre application mobile, vous devez intégrer celle-ci à [App Center](https://docs.microsoft.com/mobile-center/). Application Insights ne reçoit pas de données de télémétrie directement de votre application mobile. Au lieu de cela, votre application envoie les données de télémétrie d’événements personnalisés à App Center. Ensuite, App Center exporte en continu des copies de ces événements personnalisés vers Application Insights à mesure que les événements sont reçus.

Pour intégrer votre application, suivez le démarrage rapide d’App Center pour chaque plateforme qu’elle prend en charge. Créez des instances distinctes d’App Center pour chaque plateforme :

* [iOS](https://docs.microsoft.com/mobile-center/sdk/getting-started/ios)
* [Android](https://docs.microsoft.com/mobile-center/sdk/getting-started/android)
* [Xamarin](https://docs.microsoft.com/mobile-center/sdk/getting-started/xamarin)
* [Windows universel](https://docs.microsoft.com/mobile-center/sdk/getting-started/uwp)
* [React Native](https://docs.microsoft.com/mobile-center/sdk/getting-started/react-native)

## <a name="track-events-in-your-app"></a>Suivre les événements dans votre application

Une fois votre application intégrée à App Center, vous devez la modifier pour envoyer les données de télémétrie des événements personnalisés à l’aide du Kit de développement logiciel (SDK) App Center. Les événements personnalisés sont le seul type de données de télémétrie App Center qui est exporté vers Application Insights.

Pour envoyer des événements personnalisés à partir d’applications iOS, utilisez la méthode `trackEvent` ou `trackEvent:withProperties` dans le Kit de développement logiciel (SDK) App Center. [Découvrez plus en détail le suivi des événements à partir des applications iOS.](https://docs.microsoft.com/mobile-center/sdk/analytics/ios)

```Swift
MSAnalytics.trackEvent("Video clicked")
```

Pour envoyer des événements personnalisés à partir d’applications Android, utilisez la méthode `trackEvent` dans le Kit de développement logiciel (SDK) App Center. [Découvrez plus en détail le suivi des événements à partir des applications Android.](https://docs.microsoft.com/mobile-center/sdk/analytics/android)

```Java
Analytics.trackEvent("Video clicked")
```

Pour envoyer des événements personnalisés à partir d’autres plateformes d’applications, utilisez les méthodes `trackEvent` dans leurs Kits de développement logiciel (SDK) App Center.

Pour vous assurer que vos événements personnalisés sont reçus, accédez à l’onglet **Événements** sous la section **Analytique** dans App Center. Quelques minutes peuvent s’écouler entre l’envoi des événements à partir de votre application et leur affichage.

## <a name="create-an-application-insights-resource"></a>Création d’une ressource Application Insights dans Azure

Dès que votre application envoie des événements personnalisés et que ces derniers sont reçus par App Center, vous devez créer une ressource Application Insights de type App Center dans le Portail Azure :

1. Connectez-vous au [portail Azure](https://portal.azure.com/).
2. Sélectionnez **Nouveau** > **Surveillance + gestion** > **Application Insights**.

    ![Ajout d’une ressource Application Insights](./media/app-insights-mobile-center-quickstart/add.png)

    Une boîte de configuration s’affiche. Utilisez le tableau ci-dessous pour remplir les champs d’entrée.

    | Paramètres        |  Valeur           | Description  |
   | ------------- |:-------------|:-----|
   | **Name**      | Une valeur globale unique, comme « myApp-iOS » | Nom identifiant l’application que vous analysez |
   | **Type d’application** | Application App Center | Type de l’application que vous analysez |
   | **Groupe de ressources**     | Un nouveau groupe de ressources, ou un groupe de ressources existant à partir du menu | Groupe de ressources dans lequel créer la ressource Application Insights |
   | **Emplacement** | Un emplacement à partir du menu | Choisissez un emplacement près de chez vous ou proche de l’endroit où votre application est hébergée |

3. Cliquez sur **Créer**.

Si votre application prend en charge plusieurs plateformes (iOS, Android, etc.), il est préférable de créer des ressources Application Insights distinctes, à raison d’une par plateforme.

## <a name="export-to-application-insights"></a>Exporter vers Application Insights

Dans votre nouvelle ressource Application Insights, dans la page **Vue d’ensemble**, dans la section **Bases** en haut, copiez la clé d’instrumentation pour cette ressource.

Dans l’instance App Center pour votre application :

1. Dans la page **Paramètres**, cliquez sur **Exporter**.
2. Choisissez **Nouvelle exportation**, choisissez **Application Insights**, puis cliquez sur **Personnaliser**.
3. Collez la clé d’instrumentation Application Insights dans la zone.
4. Acceptez d’accroître l’utilisation de l’abonnement Azure contenant votre ressource Application Insights. Chaque ressource Application Insights est gratuite pour le premier Go de données reçues par mois. [Découvrez plus en détail les tarifs Application Insights.](https://azure.microsoft.com/pricing/details/application-insights/)

N’oubliez pas de répéter ce processus pour chaque plateforme prise en charge par votre application.

Une fois [l’exportation](https://docs.microsoft.com/mobile-center/analytics/export) configurée, chaque événement personnalisé reçu par App Center est copié dans Application Insights. Plusieurs minutes pouvant s’écouler avant que les événements n’atteignent Application Insights, s’ils n’apparaissent pas immédiatement, attendez un peu avant d’effectuer des diagnostics.

Pour que vous disposiez de davantage de données à la première connexion, les 48 heures d’événements personnalisés les plus récentes dans App Center sont automatiquement exportées vers Application Insights.

## <a name="start-monitoring-your-app"></a>Démarrer la surveillance de votre application

Application Insights peut interroger, segmenter, filtrer et analyser les données de télémétrie des événements personnalisés à partir de vos applications, au-delà des outils d’analytique fournis par App Center.

1. **Interroger les données de télémétrie de vos événements personnalisés.** Dans la page **Vue d’ensemble** d’Application Insights, choisissez **Analytique**. 

   ![Bouton Analytique dans Application Insights](./media/app-insights-mobile-center-quickstart/analytics.png)

   Le portail Application Insights Analytics associé à votre ressource Application Insights s’ouvre. Le portail Analytics vous permet d’interroger directement vos données à l’aide du langage de requête Log Analytics ; vous pouvez ainsi poser des questions arbitrairement complexes sur votre application et ses utilisateurs.
   
   Ouvrez un nouvel onglet dans le portail Analytics, puis collez la requête suivante. Elle retourne pour chaque événement personnalisé et par ordre décroissant le nombre d’utilisateurs distincts ayant envoyé cet événement à partir de votre application au cours des dernières 24 heures.

   ```AIQL
   customEvents
   | where timestamp >= ago(24h)
   | summarize dcount(user_Id) by name 
   | order by dcount_user_Id desc 
   ```

   ![Portail Analytics](./media/app-insights-mobile-center-quickstart/analytics-portal.png)

   1. Sélectionnez la requête en cliquant n’importe où sur celle-ci dans l’éditeur de texte.
   2. Ensuite, cliquez sur **Accéder** pour exécuter la requête. 

   Découvrez-en plus sur [Application Insights Analytics](app-insights-analytics.md) et le [langage de requête Log Analytics](https://docs.loganalytics.io/docs/Language-Reference).


2. **Segmenter et filtrer les données de télémétrie de vos événements personnalisés.** Dans la page **Vue d’ensemble** d’Application Insights, choisissez **Utilisateurs** dans la table des matières.

   ![Icône de l’outil Utilisateurs](./media/app-insights-mobile-center-quickstart/users-icon.png)

   L’outil Utilisateurs affiche le nombre d’utilisateurs de votre application qui ont cliqué sur certains boutons, visité certains écrans ou effectué toute autre action faisant de votre part l’objet d’un suivi en tant qu’événement avec le Kit de développement logiciel (SDK) App Center. Si vous recherchez un moyen de segmenter et de filtrer vos événements App Center, l’outil Utilisateurs est un excellent choix.

   ![Outil Utilisateurs](./media/app-insights-mobile-center-quickstart/users.png) 

   Par exemple, segmentez l’utilisation par zone géographique en choisissant **Pays ou région** dans le menu déroulant **Et par**.

3. **Analyser des modèles de conversion, de rétention et navigation dans votre application.** Dans la page **Vue d’ensemble** d’Application Insights, choisissez **Flux d’utilisateurs** dans la table des matières.

   ![Outil Flux d’utilisateurs](./media/app-insights-mobile-center-quickstart/user-flows.png)

   L’outil Flux d’utilisateurs visualise les événements qu’envoie les utilisateurs après un événement de début. Il est utile pour obtenir une vue d’ensemble de la façon dont les utilisateurs parcourent votre application. Il peut aussi révéler des endroits de votre application où les utilisateurs ne vont plus ou répètent la même action encore et encore.

   En plus de Flux d’utilisateurs, Application Insights dispose de plusieurs outils d’analyse de l’utilisation pour répondre à des questions spécifiques :

   * **Entonnoirs**, pour analyser et surveiller le taux de conversion.
   * **Rétention**, pour analyser dans quelle mesure votre application conserve les utilisateurs au fil du temps.
   * **Classeurs**, pour combiner des visualisations et du texte dans un rapport partageable.
   * **Cohortes**, pour nommer et enregistrer des groupes d’utilisateurs ou d’événements spécifiques afin qu’ils puissent être facilement référencés à partir d’autres outils d’analytique.

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous ne souhaitez pas continuer à utiliser Application Insights avec App Center, désactivez l’exportation dans App Center, puis supprimez la ressource Application Insights. Ainsi, vous ne serez plus facturé par Application Insights pour cette ressource.

Pour désactiver l’exportation dans App Center :

1. Dans App Center, accédez à **Paramètres** et choisissez **Exporter**.
2. Cliquez sur l’exportation d’Application Insights à supprimer, puis cliquez sur **Supprimer l’exportation** en bas et confirmez l’opération.

Pour supprimer la ressource Application Insights :

1. Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis choisissez le groupe de ressources dans lequel votre ressource Application Insights a été créée.
2. Ouvrez la ressource Application Insights à supprimer. Ensuite, cliquez sur **Supprimer** dans le menu supérieur de la ressource, puis confirmez l’opération. Cette opération supprime définitivement la copie des données qui ont été exportées vers Application Insights.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Comprendre comment les clients utilisent votre application](app-insights-usage-overview.md)