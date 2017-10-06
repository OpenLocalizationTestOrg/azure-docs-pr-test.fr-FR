---
title: "aaaMonitor performances d’application web Java sur Linux - Azure | Documents Microsoft"
description: "Étendue d’analyse des performances des applications de votre site Web de Java avec hello CollectD plug-in pour Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd : métriques de performances Linux dans Application Insights


les mesures de performances du système tooexplore Linux dans [Application Insights](app-insights-overview.md), installez [collectd](http://collectd.org/), avec ses plug-in Application Insights. Cette solution open source rassemble diverses statistiques concernant le système et le réseau.

De manière générale, vous utilisez collectd lorsque vous avez déjà [instrumenté votre service web Java avec Application Insights][java]. Elle vous donne plus données toohelp vous tooenhance les performances de votre application ou diagnostiquer des problèmes. 

![Exemples de graphiques](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>Récupérer votre clé d’instrumentation
Bonjour [portail Microsoft Azure](https://portal.azure.com), ouvrez hello [Application Insights](app-insights-overview.md) ressource où vous souhaitez hello données tooappear. (Ou [créez une ressource](app-insights-create-new-resource.md).)

Création d’une copie de la clé d’instrumentation hello, qui identifie la ressource de hello.

![Parcourir tout, ouvrez votre ressource, et puis Bonjour Essentials de liste déroulante, sélectionner et copier hello clé d’Instrumentation](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Installer collectd et hello plug-in
Sur vos ordinateurs serveurs Linux :

1. Installez [collectd](http://collectd.org/) version 5.4.0 ou ultérieure.
2. Télécharger hello [plug-in d’enregistreur Application Insights collectd](https://aka.ms/aijavasdk). Notez le numéro de version hello.
3. Copier les plug-in de hello JAR dans `/usr/share/collectd/java`.
4. Modifiez `/etc/collectd/collectd.conf`:
   * Vérifiez que [hello plug-in Java](https://collectd.org/wiki/index.php/Plugin:Java) est activé.
   * Mettre à jour hello JVMArg pour Bonjour java.class.path tooinclude Bonjour suivant JAR. Mise à jour hello version numéro toomatch hello que celle que vous avez téléchargé :
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Ajoutez cet extrait de code, à l’aide de hello clé d’Instrumentation à partir de votre ressource :

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

Voici une partie d’un exemple de fichier de configuration :

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Configurez d’autres [plug-ins collectd](https://collectd.org/wiki/index.php/Table_of_Plugins)permettant de collecter des données de différentes sources.

Redémarrez collectd selon tooits [manuelle](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Afficher les données hello dans Application Insights
Dans votre ressource Application Insights, ouvrez [Metrics Explorer et ajoutez des graphiques][metrics], en sélectionnant les métriques hello souhaité toosee à partir d’une catégorie personnalisée hello.

![](./media/app-insights-java-collectd/result.png)

Par défaut, les métriques de hello sont agrégées sur tous les ordinateurs hôtes à partir de laquelle les métriques de hello ont été collectées. métriques de hello tooview par hôte, dans le panneau de détails du graphique hello, activer le regroupement, puis choisissez toogroup par CollectD-hôte.

## <a name="tooexclude-upload-of-specific-statistics"></a>téléchargement tooexclude de statistiques spécifiques
Par défaut, le plug-in de hello Application Insights envoie toutes les données hello collectées par tous les hello activé collectd 'read' plug-ins. 

tooexclude des données à partir de sources de données ou les plug-ins spécifiques :

* Modifier le fichier de configuration hello. 
* Dans `<Plugin ApplicationInsightsWriter>`, ajoutez les directives suivantes :

| Directive | Résultat |
| --- | --- |
| `Exclude disk` |Exclure toutes les données collectées par hello `disk` plug-in |
| `Exclude disk:read,write` |Exclure des sources de hello nommés `read` et `write` de hello `disk` plug-in. |

Séparez les directives par un saut de ligne.

## <a name="problems"></a>Des problèmes ?
*Je ne vois pas les données dans le portail de hello*

* Ouvrez [recherche] [ diagnostic] toosee si des événements bruts hello arrivés. Parfois, ils prennent plus de temps tooappear dans metrics explorer.
* Vous devrez peut-être trop[définir des exceptions de pare-feu pour les messages sortants](app-insights-ip-addresses.md)
* Activer le suivi dans le plug-in de hello Application Insights. Ajoutez la ligne ci-après dans `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Ouvrez un terminal et démarrer collectd en mode documenté, toosee les problèmes, qu'il est signalé :
  * `sudo collectd -f`

## <a name="known-issue"></a>Problème connu

plug-in Application Insights écrire des Hello est incompatible avec certains plug-ins en lecture. Parfois, certains plug-ins d’envoi « NaN » où le plug-in Application Insights de hello attend un nombre à virgule flottante.

Symptôme : journal de collectd hello présente les erreurs qui incluent « AI :... SyntaxError: Unexpected token N ».

Solution de contournement : Exclure les données collectées par le plug-ins écriture hello problème. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


