---
title: Surveiller les performances des applications web Java sur Linux - Azure | Microsoft Docs
description: "Surveillance étendue des performances des applications de votre site web Java avec le plug-in collectd pour Application Insights."
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
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="71d91-103">collectd : métriques de performances Linux dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="71d91-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="71d91-104">Pour explorer les métriques de performances d’un système Linux dans [Application Insights](app-insights-overview.md), installez [collectd](http://collectd.org/) et son plug-in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71d91-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="71d91-105">Cette solution open source rassemble diverses statistiques concernant le système et le réseau.</span><span class="sxs-lookup"><span data-stu-id="71d91-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="71d91-106">De manière générale, vous utilisez collectd lorsque vous avez déjà [instrumenté votre service web Java avec Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="71d91-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="71d91-107">Il vous donne davantage de données pour vous aider à améliorer les performances de votre application ou à diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="71d91-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![Exemples de graphiques](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="71d91-109">Récupérer votre clé d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="71d91-109">Get your instrumentation key</span></span>
<span data-ttu-id="71d91-110">Dans le [Portail Microsoft Azure](https://portal.azure.com), ouvrez la ressource [Application Insights](app-insights-overview.md) dans laquelle vous souhaitez afficher les données.</span><span class="sxs-lookup"><span data-stu-id="71d91-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="71d91-111">(Ou [créez une ressource](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="71d91-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="71d91-112">Effectuez une copie de la clé d’instrumentation, qui identifie la ressource.</span><span class="sxs-lookup"><span data-stu-id="71d91-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![Parcourez tous les éléments, ouvrez votre ressource, puis, dans la liste déroulante « Essentials », sélectionnez et copiez la clé d’instrumentation.](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="71d91-114">Installer le plug-in et collectd</span><span class="sxs-lookup"><span data-stu-id="71d91-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="71d91-115">Sur vos ordinateurs serveurs Linux :</span><span class="sxs-lookup"><span data-stu-id="71d91-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="71d91-116">Installez [collectd](http://collectd.org/) version 5.4.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="71d91-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="71d91-117">Téléchargez le [plug-in d'écriture collectd Application Insights](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="71d91-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="71d91-118">Notez le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="71d91-118">Note the version number.</span></span>
3. <span data-ttu-id="71d91-119">Copiez le fichier JAR du plug-in dans `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="71d91-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="71d91-120">Modifiez `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="71d91-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="71d91-121">Vérifiez que [le plug-in Java](https://collectd.org/wiki/index.php/Plugin:Java) est activé.</span><span class="sxs-lookup"><span data-stu-id="71d91-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="71d91-122">Mettez à jour l’élément JVMArg pour java.class.path afin d’inclure le fichier JAR suivant.</span><span class="sxs-lookup"><span data-stu-id="71d91-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="71d91-123">Mettez à jour le numéro de version afin qu’il corresponde à celui que vous avez téléchargé :</span><span class="sxs-lookup"><span data-stu-id="71d91-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="71d91-124">Ajoutez cet extrait de code à l’aide de la clé d’instrumentation provenant de votre ressource :</span><span class="sxs-lookup"><span data-stu-id="71d91-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="71d91-125">Voici une partie d’un exemple de fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="71d91-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="71d91-126">Configurez d’autres [plug-ins collectd](https://collectd.org/wiki/index.php/Table_of_Plugins)permettant de collecter des données de différentes sources.</span><span class="sxs-lookup"><span data-stu-id="71d91-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="71d91-127">Redémarrez collectd selon les instructions de son [manuel](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="71d91-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="71d91-128">Visualiser les données dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="71d91-128">View the data in Application Insights</span></span>
<span data-ttu-id="71d91-129">Dans votre ressource Application Insights, ouvrez [Metrics Explorer et ajoutez des graphiques][metrics] en sélectionnant les métriques que vous souhaitez afficher à partir de la catégorie Personnalisé.</span><span class="sxs-lookup"><span data-stu-id="71d91-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="71d91-130">Par défaut, les métriques sont agrégés sur toutes les machines hôtes à partir desquelles ils ont été collectés.</span><span class="sxs-lookup"><span data-stu-id="71d91-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="71d91-131">Pour visualiser les métriques par hôte, dans le panneau des détails du graphique, activez le regroupement, puis choisissez un groupement de type CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="71d91-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="71d91-132">Pour exclure le chargement de statistiques spécifiques</span><span class="sxs-lookup"><span data-stu-id="71d91-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="71d91-133">Par défaut, le plug-in Application Insights envoie toutes les données collectées par tous les plug-ins de lecture collectd activés.</span><span class="sxs-lookup"><span data-stu-id="71d91-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="71d91-134">Pour exclure des données provenant de plug-ins ou de sources de données spécifiques :</span><span class="sxs-lookup"><span data-stu-id="71d91-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="71d91-135">Modifiez le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="71d91-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="71d91-136">Dans `<Plugin ApplicationInsightsWriter>`, ajoutez les directives suivantes :</span><span class="sxs-lookup"><span data-stu-id="71d91-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="71d91-137">Directive</span><span class="sxs-lookup"><span data-stu-id="71d91-137">Directive</span></span> | <span data-ttu-id="71d91-138">Résultat</span><span class="sxs-lookup"><span data-stu-id="71d91-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="71d91-139">Exclusion de toutes les données collectées par le plug-in `disk` .</span><span class="sxs-lookup"><span data-stu-id="71d91-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="71d91-140">Exclusion des sources nommées `read` et `write` du plug-in `disk`.</span><span class="sxs-lookup"><span data-stu-id="71d91-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="71d91-141">Séparez les directives par un saut de ligne.</span><span class="sxs-lookup"><span data-stu-id="71d91-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="71d91-142">Des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="71d91-142">Problems?</span></span>
<span data-ttu-id="71d91-143">*Je ne vois pas les données dans le portail*</span><span class="sxs-lookup"><span data-stu-id="71d91-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="71d91-144">Ouvrez [Rechercher][diagnostic] pour vérifier si les événements bruts sont arrivés.</span><span class="sxs-lookup"><span data-stu-id="71d91-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="71d91-145">Ils mettent parfois du temps à apparaître dans Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="71d91-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="71d91-146">Vous devrez peut-être [définir des exceptions de pare-feu pour les données sortantes](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="71d91-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="71d91-147">Activez le suivi dans le plug-in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71d91-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="71d91-148">Ajoutez la ligne ci-après dans `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="71d91-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="71d91-149">Ouvrez un terminal et démarrez collectd en mode détaillé pour vérifier si des problèmes ont été signalés :</span><span class="sxs-lookup"><span data-stu-id="71d91-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="71d91-150">Problème connu</span><span class="sxs-lookup"><span data-stu-id="71d91-150">Known issue</span></span>

<span data-ttu-id="71d91-151">Le plug-in d’écriture Application Insights n’est pas compatible avec certains plug-ins de lecture.</span><span class="sxs-lookup"><span data-stu-id="71d91-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="71d91-152">Certains plug-ins envoient parfois « NaN » alors que le plug-in Application Insights s’attend à recevoir un nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="71d91-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="71d91-153">Symptôme : le journal collectd affiche des erreurs incluant « AI: ... SyntaxError: Unexpected token N ».</span><span class="sxs-lookup"><span data-stu-id="71d91-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="71d91-154">Solution de contournement : exclure les données collectées par les plug-ins d’écriture à l’origine du problème.</span><span class="sxs-lookup"><span data-stu-id="71d91-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


