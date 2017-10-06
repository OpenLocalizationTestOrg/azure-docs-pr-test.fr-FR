---
title: "aaaExport à l’aide d’Analytique de flux de données à partir de l’Application Azure Insights | Documents Microsoft"
description: "Flux de données Analytique peut se transformer en permanence, filtrer et acheminer les données de salutation que vous exportez à partir de l’Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Tooprocess de flux de données Analytique d’utilisation des données exportées à partir de l’Application Insights
[Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) est l’outil idéal de hello pour le traitement des données [exporté à partir de l’Application Insights](app-insights-export-telemetry.md). Stream Analytics peut extraire des données de diverses sources. Il peut transformer et filtrer les données de hello et router tooa diverses récepteurs.

Dans cet exemple, nous allons créer un adaptateur qui Récupère des données d’Application Insights, changements de noms et traite certains des champs de hello et dirige dans Power BI.

> [!WARNING]
> Il existe beaucoup plus facile et [méthodes recommandées pour données d’Application Insights toodisplay dans Power BI](app-insights-export-power-bi.md). Hello chemin illustrée ici est simplement un tooillustrate exemple tooprocess comment les données exportées.
> 
> 

![Diagramme de blocs pour une exportation via SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Création d’un stockage dans Azure
Exportation continue retourne toujours le compte de stockage Azure données tooan, donc vous devez tout d’abord le stockage de hello toocreate.

1. Créer un compte de stockage « classiques » dans votre abonnement Bonjour [portail Azure](https://portal.azure.com).
   
   ![Sur le portail Azure, choisissez Nouveau, Données, Stockage.](./media/app-insights-export-stream-analytics/030.png)
2. Créez un conteneur.
   
    ![Dans un nouveau stockage hello, sélectionnez les conteneurs, cliquez sur la vignette de conteneurs hello, puis sur Ajouter](./media/app-insights-export-stream-analytics/040.png)
3. Copiez la clé d’accès de stockage de hello
   
    Vous en aurez besoin dès tooset hello toohello d’entrée flux analytique service.
   
    ![Dans le stockage de hello, ouvrez les paramètres, clés et effectuer une copie de hello clé d’accès primaire](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Démarrer l’exportation continue tooAzure stockage
[exportation continue](app-insights-export-telemetry.md) déplace des données d'Application Insights vers le stockage Azure.

1. Bonjour portail Azure, parcourir les ressources d’Application Insights toohello que vous avez créé pour votre application.
   
    ![Sélectionnez Parcourir, Application Insights, puis votre application.](./media/app-insights-export-stream-analytics/050.png)
2. Créez une exportation continue.
   
    ![Choisissez Paramètres, Exportation continue, Ajouter.](./media/app-insights-export-stream-analytics/060.png)

    Sélectionnez le compte de stockage hello que vous avez créé précédemment :

    ![Définir la destination de l’exportation hello](./media/app-insights-export-stream-analytics/070.png)

    Définir les types d’événement hello toosee :

    ![Choisissez les types d’événements.](./media/app-insights-export-stream-analytics/080.png)

1. Laissez les données s'accumuler. Installez-vous confortablement et laissez les utilisateurs utiliser votre application pendant un certain temps. Les données de télémétrie vont vous être transmises et vous permettre d’afficher des graphiques statistiques dans [Metrics explorer](app-insights-metrics-explorer.md) et des événements dans [Recherche de diagnostic](app-insights-diagnostic-search.md). 
   
    Et, en outre, les données de salutation exportera tooyour stockage. 
2. Inspecter les données hello exportée. Dans Visual Studio, sélectionnez **Afficher / Cloud Explorer**, puis ouvrez Azure / Stockage. (Si vous n’avez pas cette option de menu, vous devez tooinstall hello Azure SDK : ouvrir la boîte de dialogue Nouveau projet hello et ouvrez Visual C# / Cloud / obtenir Microsoft Azure SDK pour .NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Prenez note de la partie commune de hello du nom de chemin d’accès de hello, qui est dérivé de la clé de nom et d’instrumentation application hello. 

événements de Hello sont écrits les fichiers de tooblob au format JSON. Chaque fichier peut contenir un ou plusieurs événements. Par conséquent, nous souhaitons les données d’événement tooread hello et filtrer les champs hello. Il existe toutes sortes de choses que nous pouvons faire avec les données de hello, mais notre plan est aujourd'hui toouse flux Analytique toopipe hello données tooPower BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Création d’une instance Azure Stream Analytics
À partir de hello [portail Azure Classic](https://manage.windowsazure.com/), sélectionnez le service d’Analytique de flux de données Azure hello et créer une nouvelle tâche de flux de données Analytique :

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Lors de la création de tâche hello, développer ses détails :

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Définition de l’emplacement des objets blob
Définissez-le entrée tootake à partir de votre objet blob de l’exportation continue :

![](./media/app-insights-export-stream-analytics/120.png)

Vous devez maintenant hello clé d’accès primaire à partir de votre compte de stockage que vous avez notée précédemment. Définir en tant que clé de compte de stockage de hello.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Définition de la séquence d’octets préfixe du chemin d’accès
![](./media/app-insights-export-stream-analytics/140.png)

**Être vraiment tooset hello Format de Date tooYYYY-MM-JJ (avec les tirets).**

Hello modèle du préfixe de chemin d’accès spécifie où Analytique de flux de données recherche les fichiers d’entrée hello dans le stockage hello. Vous devez tooset il toohow toocorrespond de l’exportation continue stocke les données de hello. Définissez-la comme suit :

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Dans cet exemple :

* `webapplication27`est le nom hello Hello ressource Application Insights **toutes les minuscules**.
* `1234...`est la clé d’instrumentation hello Hello ressource Application Insights, **l’omission de tirets**. 
* `PageViews`est de type de hello de données vous souhaitez tooanalyze. les types disponibles Hello dépendent de filtre hello que vous définissez dans l’exportation continue. Examiner les autres types disponibles hello de toosee données exportées hello et consultez hello [exporter le modèle de données](app-insights-export-data-model.md).
* `/{date}/{time}` est une séquence écrite de manière littérale.

> [!NOTE]
> Vérifiez que hello toomake de stockage que vous obtenez le chemin d’accès hello droite.
> 
> 

### <a name="finish-initial-setup"></a>Fin de l’installation initiale
Vérifiez le format de sérialisation hello :

![Confirmez et fermez l’assistant.](./media/app-insights-export-stream-analytics/150.png)

Fermez l’Assistant de hello et attendez hello le programme d’installation toocomplete.

> [!TIP]
> Utilisez toodownload de commande exemple hello certaines données. Conserver en un toodebug d’exemple de test de votre requête.
> 
> 

## <a name="set-hello-output"></a>Sortie hello
Sélectionnez votre projet et définissez hello sortie.

![Sélectionnez le nouveau canal de hello, cliquez sur les sorties, ajouter, Power BI](./media/app-insights-export-stream-analytics/160.png)

Fournissez votre **compte professionnel ou scolaire** tooauthorize tooaccess de flux de données Analytique votre ressource Power BI. Puis inventer un nom pour la sortie de hello et pour la table et le jeu de données Power BI hello cible.

![Inventer trois noms](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Requête hello de jeu
requête de Hello détermine la traduction hello toooutput d’entrée.

![Sélectionnez le travail de hello et cliquez sur la requête. Collez l’exemple hello ci-dessous.](./media/app-insights-export-stream-analytics/180.png)

Utilisez hello Test fonction toocheck que vous obtenez une sortie de droite hello. Lui donner des exemples de données hello que vous avez suivies à partir de la page d’entrées hello. 

### <a name="query-toodisplay-counts-of-events"></a>Toodisplay les décomptes d’événements de requête
Collez cette requête :

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* entrée de l’exportation est alias hello nous a donné d’entrée de flux toohello
* pbi-sortie est l’alias de sortie hello nous avons défini
* Nous utilisons [externe GetElements appliquer](https://msdn.microsoft.com/library/azure/dn706229.aspx) , car le nom de l’événement hello est dans un arrray JSON imbriquée. Puis récupère de Select hello hello nom d’événement, ainsi que de nombre hello d’instances de ce nom dans hello laps de temps. Hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause regroupe les éléments hello dans des périodes de 1 minute.

### <a name="query-toodisplay-metric-values"></a>Les valeurs de mesure toodisplay de requête
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Cette requête explore heure de l’événement hello métriques télémétrie tooget hello et la valeur de métrique hello. les valeurs de mesure Hello étant à l’intérieur d’un tableau, nous utilisent les hello externe GetElements Appliquer modèle tooextract hello lignes. « myMetric » désigne hello métrique de hello dans ce cas. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Requête tooinclude les valeurs de propriétés de dimension
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* Cette requête inclut les valeurs des propriétés de dimension hello sans en fonction d’une dimension particulière en cours à l’index de tableau à une dimension hello fixe.

## <a name="run-hello-job"></a>Exécuter la tâche de hello
Vous pouvez sélectionner une date dans hello au-delà de travail de hello toostart à partir de. 

![Sélectionnez le travail de hello et cliquez sur la requête. Collez l’exemple hello ci-dessous.](./media/app-insights-export-stream-analytics/190.png)

Attendez que l’exécution du travail de hello.

## <a name="see-results-in-power-bi"></a>Afficher les résultats dans Power BI
> [!WARNING]
> Il existe beaucoup plus facile et [méthodes recommandées pour données d’Application Insights toodisplay dans Power BI](app-insights-export-power-bi.md). Hello chemin illustrée ici est simplement un tooillustrate exemple tooprocess comment les données exportées.
> 
> 

Ouvrez Power BI avec votre travail ou le compte scolaire et la hello sélectionnez le jeu de données et la table que vous avez défini en tant que sortie hello de tâche de flux de données Analytique hello.

![Dans Power BI, sélectionnez votre dataset et vos champs.](./media/app-insights-export-stream-analytics/200.png)

Vous pouvez maintenant utiliser ce jeu de données dans des rapports et des tableaux de bord dans [Power BI](https://powerbi.microsoft.com).

![Dans Power BI, sélectionnez votre dataset et vos champs.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Pas de données ?
* Vérifiez que vous avez [format de date set hello](#set-path-prefix-pattern) correctement tooYYYY-MM-JJ (avec les tirets).

## <a name="video"></a>Vidéo
Noam Ben Zeev montre le mode d’exportation des données à l’aide de flux de données Analytique tooprocess.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Exportation continue](app-insights-export-telemetry.md)
* [Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

