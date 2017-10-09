---
title: "télémétrie aaaSeparating du développement, tester et publier dans Azure Application Insights | Documents Microsoft"
description: "Ressources toodifferent de télémétrie directe pour les marqueurs de développement, test et de production."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Séparation des télémétries de développement, de test et de production

Lorsque vous développez une prochaine version de hello d’une application web, vous ne souhaitez pas toomix des hello [Application Insights](app-insights-overview.md) télémétrie à partir de la version de nouveau hello et hello déjà libéré. tooavoid confusions, envoi hello télémétrie développement différents stades tooseparate des ressources Application Insights, avec des clés de l’instrumentation distinct (ikeys). toomake il déplace de clé d’instrumentation toochange hello plus facilement en tant que version à partir d’une seule phase tooanother, il peut être ikey de hello tooset utiles dans le code plutôt que dans le fichier de configuration hello. 

(Si votre système est un service cloud Azure, il existe [une autre méthode pour configurer des iKeys distinctes](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>À propos des ressources et des clés d’instrumentation

Lorsque vous définissez un suivi Application Insights pour votre application web, vous créez une *ressource* Application Insights dans Microsoft Azure. Ouvrez cette ressource Bonjour portail Azure dans l’ordre toosee et analysez la télémétrie hello collecté à partir de votre application. ressource de Hello est identifié par un *clé d’instrumentation* (ikey). Lorsque vous installez hello Application Insights package toomonitor votre application, vous configurez avec la clé d’instrumentation hello, afin qu’il sache où toosend hello télémétrie.

Vous choisissez généralement des ressources distinctes toouse ou une ressource partagée unique dans différents scénarios :

* Applications différentes, indépendantes : utilisez une ressource et une ikey séparées pour chaque application.
* Plusieurs composants ou les rôles d’application d’une entreprise - utiliser un [unique ressource partagée](app-insights-monitor-multi-role-apps.md) pour tous les hello des applications de composant. Télémétrie peut être filtrée ou segmentée par une propriété de cloud_RoleName hello.
* Développement, Test et mise en production - utilisent ikey de ressources distinct pour les versions du système hello dans « horodatage » ou une phase de production.
* Test A | B : utilisez une seule ressource. Créer un tooadd TelemetryInitializer une télémétrie toohello de propriété qui identifie les variantes hello.


## <a name="dynamic-ikey"></a> Clé d'instrumentation dynamique

toomake plus facilement ikey de hello toochange en tant que code de hello se déplace entre des étapes de la production, définie dans le code à la place de dans le fichier de configuration hello.

Clé d’ensemble hello dans une méthode d’initialisation, par exemple global.aspx.cs dans un service ASP.NET :

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

Dans cet exemple, ikeys hello pour différentes ressources de hello sont placés dans les différentes versions du fichier de configuration web hello. Permutation fichier de configuration web hello - que vous pouvez effectuer dans le cadre du script de mise en production hello - échangera ressource cible de hello.

### <a name="web-pages"></a>Pages web
Hello iKey est également utilisé dans les pages web de votre application, Bonjour [script que vous avez obtenu à partir du Panneau de démarrage rapide de hello](app-insights-javascript.md). Au lieu de la rédaction du code littéralement dans le script de hello, vous devez le générer à partir de l’état du serveur hello. Par exemple, dans une application ASP.NET :

*JavaScript dans Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Créer des ressource Application Insights supplémentaires
les données de télémétrie tooseparate pour différents composants d’applications, ou pour différents horodatages (développement/test/production) de hello même composant, puis que vous aurez toocreate une nouvelle ressource Application Insights.

Bonjour [portal.azure.com](https://portal.azure.com), ajouter une ressource Application Insights :

![Cliquez sur Nouveau > Application Insights](./media/app-insights-separate-resources/01-new.png)

* **Type d’application** affecte ce que vous voyez sur le panneau de vue d’ensemble de hello et propriétés hello disponibles dans [explorer métrique](app-insights-metrics-explorer.md). Si vous ne voyez pas votre type d’application, choisissez un des types de web hello pour les pages web.
* **Groupe de ressources** facilite la gestion des propriétés telles que le [contrôle d’accès](app-insights-resources-roles-access-control.md). Vous pouvez utiliser des groupes de ressources distincts pour le développement, le test et la production.
* **Abonnement** est votre compte de paiement dans Azure.
* **Emplacement** correspond à l’endroit où nous conservons vos données. Actuellement, il n’est pas possible de le modifier. 
* **Ajouter toodashboard** place une vignette d’accès rapide pour vos ressources sur votre page d’accueil Azure. 

La création de ressources de hello prend quelques secondes. Une alerte vous prévient lorsque l’opération est terminée.

(Vous pouvez écrire un [script PowerShell](app-insights-powershell-script-create-resource.md) toocreate une ressource automatiquement.)

### <a name="getting-hello-instrumentation-key"></a>Mise en route de la clé d’instrumentation hello
clé d’instrumentation Hello identifie la ressource hello que vous avez créé. 

![Cliquez sur Essentials, hello clé d’Instrumentation, CTRL + C](./media/app-insights-separate-resources/02-props.png)

Vous avez besoin de clés d’instrumentation de hello de tous les toowhich de ressources hello votre application envoie des données.

## <a name="filter-on-build-number"></a>Filtrer sur le numéro de build
Lorsque vous publiez une nouvelle version de votre application, vous souhaiterez toobe tooseparate en mesure des données de télémétrie hello à partir de différentes générations.

Vous pouvez définir la propriété de Version de l’Application hello afin que vous pouvez filtrer [recherche](app-insights-diagnostic-search.md) et [explorer métrique](app-insights-metrics-explorer.md) résultats.

![Filtrage sur une propriété](./media/app-insights-separate-resources/050-filter.png)

Il existe différentes méthodes de définition de propriété de Version de l’Application hello.

* Définissez directement :

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Encapsuler cette ligne dans un [initialiseur de télémétrie](app-insights-api-custom-events-metrics.md#defaults) tooensure toutes les instances de TelemetryClient sont définies de manière cohérente.
* (ASP.NET) Définir la version hello dans `BuildInfo.config`. le module web Hello intègrent la version hello à partir du nœud de BuildLabel hello. Inclure ce fichier dans votre projet et n’oubliez pas de propriété tooset hello toujours copier dans l’Explorateur de solutions.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] Générez automatiquement BuildInfo.config dans MSBuild. toodo, ajoutez quelques lignes tooyour `.csproj` fichier :

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Cela génère un fichier appelé *Votre_nom_de_projet*. Hello BuildInfo.config. processus de publication renomme tooBuildInfo.config.

    étiquette de build Hello contient un espace réservé (AutoGen_...) lorsque vous générez avec Visual Studio. Mais lors de la génération avec MSBuild, il est rempli avec le numéro de version correct hello.

    comme les tooallow numéros de version de MSBuild toogenerate, définir la version hello `1.0.*` dans AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Suivi de la version
version de l’application hello tootrack, assurez-vous que `buildinfo.config` est généré par votre processus de Microsoft Build Engine. Dans votre fichier .csproj, ajoutez :  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Lorsqu’il a des informations de build hello, module de web Application Insights hello ajoute automatiquement **version de l’Application** comme élément propriété tooevery de télémétrie. Qui vous permet de toofilter par version lorsque vous effectuez [recherches diagnostic](app-insights-diagnostic-search.md), ou lorsque vous [Explorer métriques](app-insights-metrics-explorer.md).

Toutefois, notez que le numéro de version de build hello est généré uniquement par hello Microsoft Build Engine, pas par le développeur de hello construisez dans Visual Studio.

### <a name="release-annotations"></a>Annotations de version
Si vous utilisez Visual Studio Team Services, vous pouvez [obtenir un marqueur d’annotation](app-insights-annotations.md) ajouté tooyour graphiques chaque fois que vous publiez une nouvelle version. Hello suivant image montre comment ce marqueur s’affiche.

![Capture d’écran d’un exemple d’annotation de version sur un graphique](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Étapes suivantes

* [Ressources partagées pour plusieurs rôles](app-insights-monitor-multi-role-apps.md)
* [Créer un toodistinguish initialiseur de télémétrie A | Variantes B](app-insights-api-filtering-sampling.md#add-properties)
