---
title: "analyse d’aaaUsage pour les applications web avec Azure Application Insights | Documents Microsoft"
description: "Comprenez vos utilisateurs et ce qu’ils font avec votre application web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Analyse de l’utilisation des applications web avec Application Insights

Quelles sont les fonctionnalités de votre application web les plus populaires ? Vos utilisateurs atteignent-ils leurs objectifs avec votre application ? Disparaissent-ils à des stades spécifiques, et reviennent-ils plus tard ?  [Azure Application Insights](app-insights-overview.md) vous permet d’obtenir un aperçu utile sur l’utilisation de votre application web. Chaque fois que vous mettez à jour votre application, vous pouvez évaluer son bon fonctionnement pour les utilisateurs. Grâce à ces informations, vous pouvez prendre des décisions basées sur des données sur les cycles de développement suivants.

## <a name="send-telemetry-from-your-app"></a>Envoyer des données de télémétrie à partir de votre application

meilleure expérience de Hello est obtenu en installant l’Application Insights à la fois dans le code de votre serveur d’application et vos pages web. Hello composants client et serveur de votre application d’envoi toohello arrière de télémétrie portail Azure pour l’analyse.

1. **Code de serveur :** module approprié hello d’installation pour votre [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), ou [autres](app-insights-platforms.md) application.

    * *Code de serveur tooinstall ne voulez pas ? Vous pouvez simplement [créer une ressource Azure Application Insights](app-insights-create-new-resource.md).*

2. **Code de page Web :** hello ouvrir [portail Azure](https://portal.azure.com), ouvrez la ressource d’Application Insights hello pour votre application, puis ouvrez **prise en main > analyse et diagnostiquer côté Client**. 

    ![Copiez les script hello head hello de votre page web master.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Obtenez la télémétrie :** exécuter votre projet en mode débogage pendant quelques minutes, puis examinez les résultats dans le panneau de vue d’ensemble de hello dans Application Insights.

    Publier votre application toomonitor les performances de votre application et de savoir ce que font vos utilisateurs avec votre application.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Inclure l’ID d’utilisateur et l’ID de session dans votre télémétrie
utilisateurs tootrack au fil du temps, Application Insights requiert un tooidentify de façon les. Événements de Hello est de l’outil hello seul outil d’utilisation qui ne nécessite pas un ID d’utilisateur ou un ID de session.

Commencez à envoyer ces ID [ici](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Explorer des données démographiques et des statistiques de l’utilisation
Découvrez quand des personnes utilisent votre application, les pages qui les intéressent le plus, où vos utilisateurs se trouvent, les navigateurs et les systèmes d’exploitation qu’ils utilisent. 

rapports d’utilisateurs et des Sessions Hello filtrer vos données par les pages ou des événements personnalisés et les segment par propriétés, telles que l’emplacement, l’environnement et page. Vous pouvez également ajouter vos propres filtres.

![Utilisateurs](./media/app-insights-usage-overview/users.png)  

Des informations sur la droite de hello souligner des motifs intéressants dans le jeu de hello de données.  

* Hello **utilisateurs** rapport nombres hello d’utilisateurs uniques qui accèdent à vos pages au sein de vos périodes de temps choisie. (Les utilisateurs sont comptés avec les cookies. Si un utilisateur accède à votre site avec différents navigateurs ou ordinateurs clients, ou efface ses cookies, il sera compté plusieurs fois.)
* Hello **Sessions** rapport nombre hello de sessions utilisateur qui accèdent à votre site. Une session est une période d’activité d’un utilisateur, qui se termine par une période d’inactivité de plus d’une demi-heure.

[En savoir plus sur les outils d’utilisateurs, les Sessions et les événements hello](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Affichages de page

À partir du Panneau de l’utilisation de hello, parcourez tooget de vignette de vues de Page hello une répartition de vos pages les plus populaires :

![À partir du Panneau de vue d’ensemble de hello, cliquez sur hello graphique de vues de Page](./media/app-insights-usage-overview/05-games.png)

exemple Hello ci-dessus est d’un site web de jeux. À partir de graphiques de hello, nous pouvons voir instantanément :

* L’utilisation n’a pas encore améliorées dans hello semaine dernière. Peut-être que nous devrions envisager une optimisation pour les moteurs de recherche ?
* Raquettes est la page de jeu les plus populaires hello. Concentrons-nous sur la page de toothis d’améliorations supplémentaires.
* En moyenne, les utilisateurs, visitez hello Tennis page environ trois fois par semaine. (Il y a près de trois fois plus de sessions que d’utilisateurs.)
* La plupart des utilisateurs le site hello au cours de la semaine de travail hello des États-Unis et les heures de travail. Par exemple, nous devons fournir un bouton « Masquer rapide » sur la page web de hello.
* Hello [annotations](app-insights-annotations.md) sur le graphique de hello s’affichent lorsque les nouvelles versions du site Web de hello ont été déployées. Aucun des déploiements récents de hello a un effet notable sur l’utilisation.

Que se passe-t-il si vous souhaitez des sites à tooyour tooinvestigate hello trafic plus en détail, telles que le fractionnement d’une propriété personnalisée, que votre site expédie dans son télémétrie des consultations de page ?

1. Ouvrez hello **événements** outil dans le menu de ressource Application Insights hello. Cet outil vous permet d’analyser combien de pages consultées et d’événements personnalisés ont été envoyés à partir de votre application, sur la base des différentes options de filtrage, cohorte et segmentation.
2. Bonjour « Qui a utilisé » la liste déroulante, sélectionnez « N’importe quelle Page de vue ».
3. Dans la liste déroulante de « Fractionnement par » hello, sélectionnez une propriété qui toosplit votre page Afficher télémétrie.

## <a name="retention---how-many-users-come-back"></a>Rétention - Combien d’utilisateurs reviennent ?

Rétention vous permet de comprendre la fréquence à laquelle vos utilisateurs retournent toouse leur application basée sur les cohortes d’utilisateurs qui a exécuté une action entreprise pendant un certain intervalle de planification. 

- Comprendre les fonctionnalités spécifiques entraînent l’arrière toocome plus que d’autres utilisateurs 
- Formuler des hypothèses en fonction des données utilisateur réel 
- Déterminer si la rétention est un problème dans votre produit 

![Rétention](./media/app-insights-usage-overview/retention.png) 

contrôles de rétention de Hello haut permettent de vous toodefine des événements spécifiques et rétention de toocalculate de plage de temps. graphique de milieu de hello Hello donne une représentation visuelle de hello du pourcentage de rétention globale par hello plage de temps spécifié. graphique de Hello sous hello représente rétention individuel dans une période donnée. Ce niveau de détail vous permet de toounderstand votre quels utilisateurs et ce qui peut affecter les utilisateurs le retour à une granularité plus détaillée.  

[Plus d’informations sur l’outil de conservation hello](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Événements personnalisés

tooget conscience de ce que les utilisateurs à votre application web, il s’agit des lignes tooinsert utile des événements personnalisés toolog de code. Ces événements peuvent suivre quoi que ce soit à partir d’actions utilisateur détaillé en cliquant sur les boutons, événements d’importants de l’activité de toomore tels que d’un achat ou gagnante d’un jeu. 

Bien que les pages consultées puissent représenter des événements utiles, cela n’est en général pas le cas. Un utilisateur peut ouvrir une page de produit sans acheter le produit de hello. 

Grâce aux événements spécifiques, vous pouvez représenter la progression de vos utilisateurs sur votre site. Vous pouvez connaître leurs préférences sur les différentes options et où ils abandonnent ou rencontrent des difficultés. Avec cette base de connaissances, vous prendre des décisions sur les priorités de hello dans votre backlog de développement.

Événements peuvent être enregistrés dans la page web de hello :

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

Ou côté serveur hello hello web app :

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

Vous pouvez joindre des événements de toothese de valeurs de propriété, afin que vous pouvez filtrer ou fractionner des événements hello lorsque vous examinez les dans le portail de hello. En outre, un ensemble standard de propriétés est attaché tooeach événement, telles que des ID d’utilisateur anonyme, ce qui vous permet de séquence de hello tootrace des activités d’un utilisateur individuel.

En savoir plus sur les [événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent) et les [propriétés](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Segmenter et traiter les événements

Dans les outils d’utilisateurs, les Sessions et les événements de hello, vous pouvez découper et manipulent des événements personnalisés par utilisateur, nom de l’événement et propriétés.
![Utilisateurs](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Télémétrie hello de conception avec l’application hello

Lorsque vous concevez chaque fonctionnalité de votre application, pensez comment vous allez toomeasure son succès avec vos utilisateurs. Décider ce que vous devez toorecord et le code hello de suivi des appels pour les événements dans votre application à partir de hello des événements commerciaux Démarrer.

## <a name="a--b-testing"></a>Test A | B
Si vous ne connaissez pas variante d’une fonctionnalité sera plus efficace, relâchez les deux, rendre chaque toodifferent accessible. Mesurer la réussite de hello de chacun, puis déplacez les version unifiée tooa.

Cette technique, vous attacher propriété distinctes valeurs tooall hello données de télémétrie envoyé par chaque version de votre application. C’est également en définissant des propriétés Bonjour TelemetryContext active. Ces propriétés par défaut sont ajoutées au message de télémétrie tooevery hello application envoie - non seulement vos messages personnalisés, mais également les télémétrie standard hello.

Dans le portail Application Insights hello, filtrer et diviser vos données sur des valeurs de propriété hello, ainsi que les différentes versions de toocompare hello.

toodo, [configurer un initialiseur de télémétrie](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

Dans l’initialiseur d’application hello web tels que Global.asax.cs :

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

TelemetryClients de nouveau tous les ajoute automatiquement la valeur de propriété hello que vous spécifiez. Événements de télémétrie individuels peuvent remplacer les valeurs par défaut hello.

## <a name="next-steps"></a>Étapes suivantes
   - [Utilisateurs, sessions, événements](app-insights-usage-segmentation.md)
   - [Entonnoirs](usage-funnels.md)
   - [Rétention](app-insights-usage-retention.md)
   - [Flux d’utilisateurs](app-insights-usage-flows.md)
   - [Classeurs](app-insights-usage-workbooks.md)
   - [Ajouter du contexte utilisateur](app-insights-usage-send-user-context.md)
