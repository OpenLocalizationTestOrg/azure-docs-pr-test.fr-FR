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
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="0be01-103">collectd : métriques de performances Linux dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="0be01-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="0be01-104">les mesures de performances du système tooexplore Linux dans [Application Insights](app-insights-overview.md), installez [collectd](http://collectd.org/), avec ses plug-in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0be01-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="0be01-105">Cette solution open source rassemble diverses statistiques concernant le système et le réseau.</span><span class="sxs-lookup"><span data-stu-id="0be01-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="0be01-106">De manière générale, vous utilisez collectd lorsque vous avez déjà [instrumenté votre service web Java avec Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="0be01-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="0be01-107">Elle vous donne plus données toohelp vous tooenhance les performances de votre application ou diagnostiquer des problèmes.</span><span class="sxs-lookup"><span data-stu-id="0be01-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Exemples de graphiques](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="0be01-109">Récupérer votre clé d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="0be01-109">Get your instrumentation key</span></span>
<span data-ttu-id="0be01-110">Bonjour [portail Microsoft Azure](https://portal.azure.com), ouvrez hello [Application Insights](app-insights-overview.md) ressource où vous souhaitez hello données tooappear.</span><span class="sxs-lookup"><span data-stu-id="0be01-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="0be01-111">(Ou [créez une ressource](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="0be01-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="0be01-112">Création d’une copie de la clé d’instrumentation hello, qui identifie la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="0be01-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Parcourir tout, ouvrez votre ressource, et puis Bonjour Essentials de liste déroulante, sélectionner et copier hello clé d’Instrumentation](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="0be01-114">Installer collectd et hello plug-in</span><span class="sxs-lookup"><span data-stu-id="0be01-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="0be01-115">Sur vos ordinateurs serveurs Linux :</span><span class="sxs-lookup"><span data-stu-id="0be01-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="0be01-116">Installez [collectd](http://collectd.org/) version 5.4.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0be01-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="0be01-117">Télécharger hello [plug-in d’enregistreur Application Insights collectd](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="0be01-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="0be01-118">Notez le numéro de version hello.</span><span class="sxs-lookup"><span data-stu-id="0be01-118">Note hello version number.</span></span>
3. <span data-ttu-id="0be01-119">Copier les plug-in de hello JAR dans `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="0be01-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="0be01-120">Modifiez `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="0be01-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="0be01-121">Vérifiez que [hello plug-in Java](https://collectd.org/wiki/index.php/Plugin:Java) est activé.</span><span class="sxs-lookup"><span data-stu-id="0be01-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="0be01-122">Mettre à jour hello JVMArg pour Bonjour java.class.path tooinclude Bonjour suivant JAR.</span><span class="sxs-lookup"><span data-stu-id="0be01-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="0be01-123">Mise à jour hello version numéro toomatch hello que celle que vous avez téléchargé :</span><span class="sxs-lookup"><span data-stu-id="0be01-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="0be01-124">Ajoutez cet extrait de code, à l’aide de hello clé d’Instrumentation à partir de votre ressource :</span><span class="sxs-lookup"><span data-stu-id="0be01-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="0be01-125">Voici une partie d’un exemple de fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="0be01-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="0be01-126">Configurez d’autres [plug-ins collectd](https://collectd.org/wiki/index.php/Table_of_Plugins)permettant de collecter des données de différentes sources.</span><span class="sxs-lookup"><span data-stu-id="0be01-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="0be01-127">Redémarrez collectd selon tooits [manuelle](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="0be01-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="0be01-128">Afficher les données hello dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="0be01-128">View hello data in Application Insights</span></span>
<span data-ttu-id="0be01-129">Dans votre ressource Application Insights, ouvrez [Metrics Explorer et ajoutez des graphiques][metrics], en sélectionnant les métriques hello souhaité toosee à partir d’une catégorie personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="0be01-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="0be01-130">Par défaut, les métriques de hello sont agrégées sur tous les ordinateurs hôtes à partir de laquelle les métriques de hello ont été collectées.</span><span class="sxs-lookup"><span data-stu-id="0be01-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="0be01-131">métriques de hello tooview par hôte, dans le panneau de détails du graphique hello, activer le regroupement, puis choisissez toogroup par CollectD-hôte.</span><span class="sxs-lookup"><span data-stu-id="0be01-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="0be01-132">téléchargement tooexclude de statistiques spécifiques</span><span class="sxs-lookup"><span data-stu-id="0be01-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="0be01-133">Par défaut, le plug-in de hello Application Insights envoie toutes les données hello collectées par tous les hello activé collectd 'read' plug-ins.</span><span class="sxs-lookup"><span data-stu-id="0be01-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="0be01-134">tooexclude des données à partir de sources de données ou les plug-ins spécifiques :</span><span class="sxs-lookup"><span data-stu-id="0be01-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="0be01-135">Modifier le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="0be01-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="0be01-136">Dans `<Plugin ApplicationInsightsWriter>`, ajoutez les directives suivantes :</span><span class="sxs-lookup"><span data-stu-id="0be01-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="0be01-137">Directive</span><span class="sxs-lookup"><span data-stu-id="0be01-137">Directive</span></span> | <span data-ttu-id="0be01-138">Résultat</span><span class="sxs-lookup"><span data-stu-id="0be01-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="0be01-139">Exclure toutes les données collectées par hello `disk` plug-in</span><span class="sxs-lookup"><span data-stu-id="0be01-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="0be01-140">Exclure des sources de hello nommés `read` et `write` de hello `disk` plug-in.</span><span class="sxs-lookup"><span data-stu-id="0be01-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="0be01-141">Séparez les directives par un saut de ligne.</span><span class="sxs-lookup"><span data-stu-id="0be01-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="0be01-142">Des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="0be01-142">Problems?</span></span>
<span data-ttu-id="0be01-143">*Je ne vois pas les données dans le portail de hello*</span><span class="sxs-lookup"><span data-stu-id="0be01-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="0be01-144">Ouvrez [recherche] [ diagnostic] toosee si des événements bruts hello arrivés.</span><span class="sxs-lookup"><span data-stu-id="0be01-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="0be01-145">Parfois, ils prennent plus de temps tooappear dans metrics explorer.</span><span class="sxs-lookup"><span data-stu-id="0be01-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="0be01-146">Vous devrez peut-être trop[définir des exceptions de pare-feu pour les messages sortants](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="0be01-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="0be01-147">Activer le suivi dans le plug-in de hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0be01-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="0be01-148">Ajoutez la ligne ci-après dans `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="0be01-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="0be01-149">Ouvrez un terminal et démarrer collectd en mode documenté, toosee les problèmes, qu'il est signalé :</span><span class="sxs-lookup"><span data-stu-id="0be01-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="0be01-150">Problème connu</span><span class="sxs-lookup"><span data-stu-id="0be01-150">Known issue</span></span>

<span data-ttu-id="0be01-151">plug-in Application Insights écrire des Hello est incompatible avec certains plug-ins en lecture.</span><span class="sxs-lookup"><span data-stu-id="0be01-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="0be01-152">Parfois, certains plug-ins d’envoi « NaN » où le plug-in Application Insights de hello attend un nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="0be01-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="0be01-153">Symptôme : journal de collectd hello présente les erreurs qui incluent « AI :... SyntaxError: Unexpected token N ».</span><span class="sxs-lookup"><span data-stu-id="0be01-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="0be01-154">Solution de contournement : Exclure les données collectées par le plug-ins écriture hello problème.</span><span class="sxs-lookup"><span data-stu-id="0be01-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


