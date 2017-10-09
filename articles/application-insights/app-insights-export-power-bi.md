---
title: "aaaExport tooPower BI à partir de l’Application Insights | Documents Microsoft"
description: "Les requêtes Analytics peuvent être affichées dans Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Alimentation de Power BI à partir d’Application Insights
[Power BI](http://www.powerbi.com/) est une suite d’outils d’analyse métiers permettant d’analyser les données et de partager les informations. Chaque périphérique bénéficie de tableaux de bord riches. Vous pouvez combiner des données provenant de nombreuses sources, notamment des requêtes Analytics d’[Azure Application Insights](app-insights-overview.md).

Il existe trois méthodes recommandées de l’exportation des données de Application Insights tooPower BI. Vous pouvez les utiliser séparément ou ensemble.

* [**Adaptateur Power BI**](#power-pi-adapter) : configurez un tableau de bord complet des données de télémétrie à partir de votre application. ensemble de Hello de graphiques est prédéfinie, mais vous pouvez ajouter vos propres requêtes à partir d’autres sources.
* [**Exporter des requêtes d’Analytique** ](#export-analytics-queries) -écrire une requête de votre choix à l’aide d’Analytique, exportez-le tooPower BI. Vous pouvez placer cette requête sur un tableau de bord, avec d’autres données.
* [**Exportation continue et flux de données Analytique** ](app-insights-export-stream-analytics.md) -cela implique tooset de travail plus haut. Il est utile si vous souhaitez que tookeep vos données pendant de longues périodes. Dans le cas contraire, hello autres méthodes sont recommandées.

## <a name="power-bi-adapter"></a>Adaptateur Power BI
Cette méthode crée un tableau de bord complet des données de télémétrie. jeu de données initial Hello est prédéfinie, mais vous pouvez ajouter plusieurs tooit de données.

### <a name="get-hello-adapter"></a>Obtenir de l’adaptateur hello
1. Connectez-vous trop[Power BI](https://app.powerbi.com/).
2. Ouvrez **Obtenir des données**, **Services**, **Application Insights**
   
    ![Obtenir à partir d’une source de données Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Fournissent des détails de votre ressource Application Insights hello.
   
    ![Obtenir à partir d’une source de données Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Patientez une minute ou deux pour hello toobe de données importée.
   
    ![Adaptateur Power BI](./media/app-insights-export-power-bi/010.png)

Vous pouvez modifier du tableau de bord hello, en combinant des graphiques d’Application Insights hello avec ceux d’autres sources et avec les requêtes d’Analytique. Il existe une galerie de visualisation où vous pouvez obtenir plus de graphiques. Chaque graphique comporte des paramètres que vous pouvez définir.

Une fois l’importation initiale de hello, tableau de bord hello et rapports de hello continuent tooupdate tous les jours. Vous pouvez contrôler la planification d’actualisation hello hello le jeu de données.

## <a name="export-analytics-queries"></a>Exporter des requêtes Analytics
Cet itinéraire permet toowrite tout Analytique de requête vous le souhaitez et puis exporter ce tableau de bord Power BI tooa. (Vous pouvez ajouter toohello le tableau de bord créé par l’adaptateur de hello.)

### <a name="one-time-install-power-bi-desktop"></a>Une fois : installez Power BI Desktop
tooimport votre requête d’Application Insights, vous utilisez la version de bureau hello de Power BI. Mais, puis vous pouvez le publier toohello web ou tooyour espace de travail de cloud Power BI. 

Installez [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Exporter une requête Analytics
1. [Ouvrez Analytics et écrivez votre requête](app-insights-analytics-tour.md).
2. Tester et affiner la requête de hello jusqu'à ce que vous êtes satisfait des résultats de hello.

   **Assurez-vous que cette requête hello s’exécute correctement dans Analytique avant d’exporter.**
3. Sur hello **exporter** menu, choisissez **Power BI (M)**. Enregistrez le fichier de texte hello.
   
    ![Exporter une requête Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. Dans Power BI Desktop, sélectionnez **obtenir des données, la requête vide** et puis Bonjour éditeur de requête, sous **vue** sélectionnez **éditeur de requêtes avancé**.

    Script de langage M coller hello exportée dans hello éditeur de requêtes avancé.

    ![Éditeur de requêtes avancé](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Vous pouvez avoir tooprovide informations d’identification tooallow Power BI tooaccess Azure. Utilisez toosign de compte de société avec votre compte Microsoft.
   
    ![Fournir des informations d’identification Azure tooenable Power BI toorun votre requête d’Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Si vous avez besoin des informations d’identification de tooverify hello, utilisez commande de menu des paramètres de Source de données hello Bonjour éditeur de requête. Attention toospecify hello informations d’identification que vous utilisez pour Azure, ce qui peut être différent de vos informations d’identification pour Power BI.)
2. Choisissez une visualisation pour votre requête et sélectionnez des champs de hello pour l’axe x, y et segmentation de dimension.
   
    ![Sélectionner une visualisation](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Publier votre espace de travail rapports tooyour Power BI cloud. À partir de là, vous pouvez incorporer une version synchronisée dans d’autres pages web.
   
    ![Sélectionner une visualisation](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Actualiser les rapports hello manuellement à des intervalles, ou configurer une actualisation planifiée sur la page d’options hello.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="401-or-403-unauthorized"></a>401 ou 403 non autorisé 
Cela peut se produire si votre jeton d’actualisation n’a pas été mis à jour. Essayez ces tooensure étapes que vous avez toujours accès. Si vous avez accès et les informations d’identification de hello refershing ne fonctionne pas, ouvrez un ticket de support.

1. Connectez-vous à hello portail Azure et assurez-vous que vous pouvez accéder à des ressources de hello
2. Essayez les informations d’identification de toorefresh hello pour hello du tableau de bord

### <a name="502-bad-gateway"></a>502 Passerelle incorrecte
Cela est généralement dû à une requête Analytics qui renvoie trop de données. Il est conseillé à l’aide d’une plus petite plage de temps ou à l’aide de hello [il y a](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) fonctions uniquement [projet](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello des champs dont vous avez besoin.

Si la réduction hello le jeu de données provenant d’une requête Analytique de hello ne répond pas à vos besoins vous devez envisager d’utiliser hello [API](https://dev.applicationinsights.io/documentation/overview) toopull un plus grand jeu de données. Vous trouverez ici les instructions comment tooconvert hello M-requête exporter toouse hello API.

1. Créez une [clé d’API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).
2. Hello de mise à jour Power BI M script que vous avez exporté à partir de l’Analytique en remplaçant hello ARM des URL avec les API AI (voir l’exemple ci-dessous)
   * Remplacez **https://management.azure.com/subscriptions/...**
   * par **https://api.applicationinsights.io/beta/apps/...**
3. Enfin, mettre à jour les informations d’identification toobasic et utiliser votre clé API
  

**Script existant**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Script mis à jour**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>À propos de l’échantillonnage
Si votre application envoie une grande quantité de données, fonctionnalité d’adaptative d’échantillonnage de hello peut fonctionner et envoyer seulement un pourcentage de votre télémétrie. Hello que même a la valeur true si vous avez manuellement défini d’échantillonnage Bonjour SDK ou ingestion. [En savoir plus sur l’échantillonnage.](app-insights-sampling.md)


## <a name="next-steps"></a>Étapes suivantes
* [Power BI - En savoir plus](http://www.powerbi.com/learning/)
* [Didacticiel Analytics](app-insights-analytics-tour.md)

