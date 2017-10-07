---
title: "Exporter tooSQL à partir de l’Application Azure Insights | Documents Microsoft"
description: "En continu exporter tooSQL de données d’Application Insights à l’aide de flux de données Analytique."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Procédure pas à pas : Exportation tooSQL à partir de l’Application Insights à l’aide de flux de données Analytique
Cet article explique comment toomove vos données de télémétrie de [Azure Application Insights] [ start] dans une base de données SQL Azure à l’aide de [de l’exportation continue] [ export] et [Azure Stream Analytique](https://azure.microsoft.com/services/stream-analytics/). 

L’exportation continue déplace vos données de télémétrie vers le stockage Azure au format JSON. Nous analyser hello des objets JSON à l’aide d’Analytique de flux de données Azure et créer des lignes dans une table de base de données.

(Plus généralement, l’exportation continue est hello moyen toodo votre propre analyse des données de télémétrie hello tooApplication Insights d’envoi de vos applications. Vous pourriez adapter cette toodo exemple de code autres choses avec les données de télémétrie hello exportée, telles que l’agrégation de données.)

Nous allons commencer par hypothèse hello que vous avez déjà application hello toomonitor.

Dans cet exemple, nous allons utiliser des données d’affichage page hello, mais hello même modèle peut facilement être étendu tooother des types de données tels que les événements personnalisés et les exceptions. 

## <a name="add-application-insights-tooyour-application"></a>Ajouter Application Insights tooyour application
tooget démarré :

1. [Configurer Application Insights pour vos pages web](app-insights-javascript.md). 
   
    (Dans cet exemple, nous allons nous concentrer sur le traitement des données d’affichage de page dans les navigateurs clients hello, mais vous pouvez également configurer Application Insights pour côté serveur hello votre [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) application et le processus de demande dépendances et autres données de télémétrie du serveur.)
2. Publiez votre application et surveillez les données de télémétrie apparaissant dans votre ressource Application Insights.

## <a name="create-storage-in-azure"></a>Création d’un stockage dans Azure
Exportation continue retourne toujours le compte de stockage Azure données tooan, donc vous devez tout d’abord le stockage de hello toocreate.

1. Créer un compte de stockage dans votre abonnement Bonjour [portail Azure][portal].
   
    ![Sur le portail Azure, choisissez Nouveau, Données, Stockage. Sélectionnez Classique, cliquez sur Créer. Fournissez un nom de stockage.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Créez un conteneur.
   
    ![Dans un nouveau stockage hello, sélectionnez les conteneurs, cliquez sur la vignette de conteneurs hello, puis sur Ajouter](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Copiez la clé d’accès de stockage de hello
   
    Vous en aurez besoin dès tooset hello toohello d’entrée flux analytique service.
   
    ![Dans le stockage de hello, ouvrez les paramètres, clés et effectuer une copie de hello clé d’accès primaire](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Démarrer l’exportation continue tooAzure stockage
1. Bonjour portail Azure, parcourir les ressources d’Application Insights toohello que vous avez créé pour votre application.
   
    ![Sélectionnez Parcourir, Application Insights, puis votre application.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Créez une exportation continue.
   
    ![Choisissez Paramètres, Exportation continue, Ajouter.](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Sélectionnez le compte de stockage hello que vous avez créé précédemment :

    ![Définir la destination de l’exportation hello](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Définir les types d’événement hello toosee :

    ![Choisissez les types d’événements.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Laissez les données s'accumuler. Installez-vous confortablement et laissez les utilisateurs utiliser votre application pendant un certain temps. Les données de télémétrie vont vous être transmises et vous permettre d’afficher des graphiques statistiques dans [Metrics explorer](app-insights-metrics-explorer.md) et des événements dans [Recherche de diagnostic](app-insights-diagnostic-search.md). 
   
    Et, en outre, les données de salutation exportera tooyour stockage. 
2. Inspecter les données hello exportée, soit dans le portail de hello - choisir **Parcourir**, sélectionnez votre compte de stockage, puis **conteneurs** - ou dans Visual Studio. Dans Visual Studio, sélectionnez **Afficher / Cloud Explorer**, puis ouvrez Azure / Stockage. (Si vous n’avez pas cette option de menu, vous devez tooinstall hello Azure SDK : ouvrir la boîte de dialogue Nouveau projet hello et ouvrez Visual C# / Cloud / obtenir Microsoft Azure SDK pour .NET.)
   
    ![Dans Visual Studio, ouvrez Explorateur de serveurs, Azure, Stockage](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Prenez note de la partie commune de hello du nom de chemin d’accès de hello, qui est dérivé de la clé de nom et d’instrumentation application hello. 

événements de Hello sont écrits les fichiers de tooblob au format JSON. Chaque fichier peut contenir un ou plusieurs événements. Par conséquent, nous souhaitons les données d’événement tooread hello et filtrer les champs hello. Il existe toutes sortes de choses que nous pouvons faire avec les données de hello, mais notre plan aujourd'hui est toouse flux Analytique toomove hello données tooa base de données SQL. Qui rend un grand nombre de toorun facile de requêtes intéressantes.

## <a name="create-an-azure-sql-database"></a>Création d’une base de données SQL Azure
À nouveau à partir de votre abonnement dans [portail Azure][portal], créer la base de données hello (et un nouveau serveur, sauf si vous avez déjà une) toowhich, vous allez écrire les données de salutation.

![Nouveau, Données, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Assurez-vous que ce serveur de base de données hello autorise l’accès tooAzure services :

![Parcourir, des serveurs, votre serveur, les paramètres, les pare-feu, autoriser l’accès à tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Créer une table dans la base de données SQL Azure
Se connecter toohello de base de données créée dans la section précédente, hello à votre outil de gestion préférés. Dans cette procédure pas à pas, nous utiliserons [Outils d’administration SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Créer une requête et exécutez hello T-SQL suivant :

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

Dans cet exemple, nous utilisons les données issues des affichages de pages. toosee hello d’autres données disponibles, examinez la sortie JSON et voir hello [exporter le modèle de données](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Création d’une instance Azure Stream Analytics
À partir de hello [portail Azure Classic](https://manage.windowsazure.com/), sélectionnez le service d’Analytique de flux de données Azure hello et créer une nouvelle tâche de flux de données Analytique :

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Lors de la création de tâche hello, développer ses détails :

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Définition de l’emplacement des objets blob
Définissez-le entrée tootake à partir de votre objet blob de l’exportation continue :

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Vous devez maintenant hello clé d’accès primaire à partir de votre compte de stockage que vous avez notée précédemment. Définir en tant que clé de compte de stockage de hello.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Définition de la séquence d’octets préfixe du chemin d’accès
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Être hello tooset que Format de Date trop**AAAA-MM-jj** (avec **tirets**).

Hello modèle du préfixe de chemin d’accès spécifie comment Analytique de flux de données recherche les fichiers d’entrée hello dans le stockage hello. Vous devez tooset il toohow toocorrespond de l’exportation continue stocke les données de hello. Définissez-la comme suit :

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Dans cet exemple :

* `webapplication27`est le nom hello Hello ressource Application Insights, **tout en minuscules**. 
* `1234...`est la clé d’instrumentation hello Hello ressource Application Insights **et tirets supprimés**. 
* `PageViews`est hello type de données, nous souhaitons tooanalyze. les types disponibles Hello dépendent de filtre hello que vous définissez dans l’exportation continue. Examiner les autres types disponibles hello de toosee données exportées hello et consultez hello [exporter le modèle de données](app-insights-export-data-model.md).
* `/{date}/{time}` est une séquence écrite de manière littérale.

nom de hello tooget iKey de votre ressource Application Insights, ouvrez Essentials dans sa page de présentation et ouvrir les paramètres.

#### <a name="finish-initial-setup"></a>Fin de l’installation initiale
Vérifiez le format de sérialisation hello :

![Confirmez et fermez l’assistant.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Fermez l’Assistant de hello et attendez hello le programme d’installation toocomplete.

> [!TIP]
> Utilisez hello exemple fonction toocheck que vous avez défini un chemin d’accès d’entrée de hello correctement. En cas d’échec : Vérifiez qu’il existe des données dans le stockage hello pour la plage de temps exemple hello choisis. Modifier la définition d’entrée de hello et définir le compte de stockage hello, préfixe de chemin d’accès et de format de date correctement.
> 
> 

## <a name="set-query"></a>Définition d’une requête
Ouvrez la section de requête hello :

![Dans Stream analytics, sélectionnez Requête.](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Remplacez la requête par défaut de hello avec :

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Notez que hello tout d’abord certaines propriétés sont spécifiques de toopage afficher les données. Les exportations d’autres types de télémétrie disposent de propriétés différentes. Consultez hello [détaillées de référence de modèle de données pour les valeurs et les types de propriété hello.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Configurer la sortie toodatabase
Sélectionnez SQL en tant que sortie de hello.

![Dans Stream analytics, sélectionnez Sorties.](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Spécifiez la base de données SQL hello.

![Renseignez les détails de hello de votre base de données](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Fermez l’Assistant de hello et attendre une notification de sortie de hello a été configuré.

## <a name="start-processing"></a>Démarrage du traitement
Démarrer le travail de hello à partir de la barre d’action hello :

![Dans Stream Analytics, cliquez sur Démarrer.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Vous pouvez choisir si le traitement de toostart hello des données à partir de maintenant, ou toostart avec des données antérieures. Hello ce dernier est utile si vous avez eu l’exportation continue déjà en cours d’exécution pendant un certain temps.

![Dans Stream Analytics, cliquez sur Démarrer.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Après quelques minutes, outils de gestion de serveur tooSQL revenir en arrière et regarder la hello données circulent dans. Utilisez, par exemple, le type de requête suivant :

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Articles connexes
* [TooPowerBI d’exportation à l’aide de flux de données Analytique](app-insights-export-power-bi.md)
* [Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.](app-insights-export-data-model.md)
* [Exportation continue dans Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

