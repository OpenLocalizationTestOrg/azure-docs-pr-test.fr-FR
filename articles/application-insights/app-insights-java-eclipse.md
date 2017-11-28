---
title: aaaGet en main Azure Application Insights avec Java dans Eclipse | Documents Microsoft
description: "Utilisez hello performances de tooadd plug-in Eclipse et l’utilisation de la surveillance tooyour Java avec Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="aea69-103">Prise en main d’Application Insights avec Java dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="aea69-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="aea69-104">Hello Application Insights SDK envoie les données de télémétrie à partir de votre application web Java afin que vous pouvez analyser les performances et l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="aea69-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="aea69-105">Hello Eclipse plug-in pour Application Insights installe automatiquement hello SDK dans votre projet afin que vous obtenez la télémétrie de zone hello, ainsi qu’une API que vous pouvez utiliser les données de télémétrie personnalisées toowrite.</span><span class="sxs-lookup"><span data-stu-id="aea69-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="aea69-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aea69-106">Prerequisites</span></span>
<span data-ttu-id="aea69-107">Plug-in de hello travaille actuellement pour les projets Maven et des projets Web dynamique dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="aea69-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="aea69-108">([Types de tooother ajouter Application Insights de projet Java][java].)</span><span class="sxs-lookup"><span data-stu-id="aea69-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="aea69-109">Vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aea69-109">You'll need:</span></span>

* <span data-ttu-id="aea69-110">Oracle JRE 1.6 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="aea69-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="aea69-111">Un abonnement trop[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="aea69-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="aea69-112">[IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/downloads/), Indigo ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="aea69-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="aea69-113">Windows 7 ou version ultérieure ou Windows Server 2008 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="aea69-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="aea69-114">Installer hello SDK sur Eclipse (une fois)</span><span class="sxs-lookup"><span data-stu-id="aea69-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="aea69-115">Vous ne devez toodo une seule fois par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="aea69-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="aea69-116">Cette étape installe un kit de ressources qui peut ajouter puis hello SDK tooeach projet Web dynamique.</span><span class="sxs-lookup"><span data-stu-id="aea69-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="aea69-117">Dans Eclipse, cliquez sur Aide, Installer un nouveau logiciel.</span><span class="sxs-lookup"><span data-stu-id="aea69-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Aide, installation de nouveaux logiciels](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="aea69-119">Hello SDK est http://dl.microsoft.com/eclipse, dans la boîte à outils Azure.</span><span class="sxs-lookup"><span data-stu-id="aea69-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="aea69-120">Désactivez l’option **Contacter tous les sites de mise à jour...**</span><span class="sxs-lookup"><span data-stu-id="aea69-120">Uncheck **Contact all update sites...**</span></span>

    ![Pour le Kit de développement logiciel (SDK) Application Insights, désactivez Contacter tous les sites de mise à jour.](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="aea69-122">Suivez hello restant comme suit pour chaque projet Java.</span><span class="sxs-lookup"><span data-stu-id="aea69-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="aea69-123">Créer une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="aea69-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="aea69-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aea69-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aea69-125">Créez une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aea69-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="aea69-126">Définissez des applications web tooJava hello application type.</span><span class="sxs-lookup"><span data-stu-id="aea69-126">Set hello application type tooJava web application.</span></span>  

    ![Cliquez sur + et choisissez Ajouter Application Insights.](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="aea69-128">Trouver la clé d’instrumentation hello de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="aea69-129">Vous en aurez besoin toopaste dans votre projet de code dans quelques instants.</span><span class="sxs-lookup"><span data-stu-id="aea69-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="aea69-131">Ajouter Application Insights tooyour projet</span><span class="sxs-lookup"><span data-stu-id="aea69-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="aea69-132">Ajouter Application Insights à partir du menu contextuel de hello du projet web Java.</span><span class="sxs-lookup"><span data-stu-id="aea69-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="aea69-134">Collez la clé d’instrumentation hello que vous avez obtenu hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aea69-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="aea69-136">clé de Hello est envoyé avec chaque élément de données de télémétrie et indique à Application Insights toodisplay dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="aea69-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="aea69-137">Exécutez l’application hello et voir les métriques</span><span class="sxs-lookup"><span data-stu-id="aea69-137">Run hello application and see metrics</span></span>
<span data-ttu-id="aea69-138">Exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="aea69-138">Run your application.</span></span>

<span data-ttu-id="aea69-139">Retourner la ressource d’Application Insights tooyour dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="aea69-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="aea69-140">Les données de demandes HTTP seront affiche sur le panneau de vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="aea69-141">(Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).</span><span class="sxs-lookup"><span data-stu-id="aea69-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="aea69-142">Réponse du serveur, nombre de demandes et échecs</span><span class="sxs-lookup"><span data-stu-id="aea69-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="aea69-143">Cliquez sur via n’importe quel toosee graphique plus des métriques.</span><span class="sxs-lookup"><span data-stu-id="aea69-143">Click through any chart toosee more detailed metrics.</span></span>

![Nombres de demandes par nom](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="aea69-145">[En savoir plus sur les mesures.][metrics]</span><span class="sxs-lookup"><span data-stu-id="aea69-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="aea69-146">Et lorsque vous affichez les propriétés hello d’une demande, vous pouvez voir les événements de télémétrie hello associés tels que les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="aea69-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Tous le suivi pour cette demande](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="aea69-148">Télémétrie côté client</span><span class="sxs-lookup"><span data-stu-id="aea69-148">Client-side telemetry</span></span>
<span data-ttu-id="aea69-149">À partir du Panneau de démarrage rapide de hello, cliquez sur Get code toomonitor Mes pages web :</span><span class="sxs-lookup"><span data-stu-id="aea69-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![Sur votre Panneau de vue d’ensemble des applications, sélectionnez Démarrage rapide, obtenir code toomonitor Mes pages web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="aea69-152">Insérer l’extrait de code hello dans head hello de vos fichiers HTML.</span><span class="sxs-lookup"><span data-stu-id="aea69-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="aea69-153">Affichage des données côté client</span><span class="sxs-lookup"><span data-stu-id="aea69-153">View client-side data</span></span>
<span data-ttu-id="aea69-154">Ouvrez et utilisez vos pages web mises à jour.</span><span class="sxs-lookup"><span data-stu-id="aea69-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="aea69-155">Attendez une ou deux minutes, puis retourner tooApplication Insights et panneau de l’utilisation de hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="aea69-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="aea69-156">(À partir du Panneau de vue d’ensemble de hello, faites défiler la liste et cliquez sur l’utilisation).</span><span class="sxs-lookup"><span data-stu-id="aea69-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="aea69-157">Mesures de session, utilisateur et afficher la page seront affiche sur le panneau de l’utilisation de hello :</span><span class="sxs-lookup"><span data-stu-id="aea69-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Sessions, utilisateurs et affichages de pages](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="aea69-159">[En savoir plus sur la configuration de la télémétrie côté client.][usage]</span><span class="sxs-lookup"><span data-stu-id="aea69-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="aea69-160">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="aea69-160">Publish your application</span></span>
<span data-ttu-id="aea69-161">Maintenant publier le serveur de votre application toohello, permettent aux utilisateurs de l’utiliser et observer les données de télémétrie hello apparaissent dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="aea69-162">Assurez-vous que votre pare-feu autorise votre toosend application ports toothese de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="aea69-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="aea69-163">dc.services.VisualStudio.com:443</span><span class="sxs-lookup"><span data-stu-id="aea69-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="aea69-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="aea69-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="aea69-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="aea69-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="aea69-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="aea69-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="aea69-167">Sur les serveurs Windows, installez :</span><span class="sxs-lookup"><span data-stu-id="aea69-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="aea69-168">Redistribuable Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="aea69-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="aea69-169">(Cette opération active les compteurs de performances.)</span><span class="sxs-lookup"><span data-stu-id="aea69-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="aea69-170">Exceptions et échecs de requêtes</span><span class="sxs-lookup"><span data-stu-id="aea69-170">Exceptions and request failures</span></span>
<span data-ttu-id="aea69-171">Les exceptions non gérées sont collectées automatiquement :</span><span class="sxs-lookup"><span data-stu-id="aea69-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="aea69-172">toocollect des données sur les autres exceptions, vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="aea69-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="aea69-173">[Insérer des appels tooTrackException dans votre code](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="aea69-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="aea69-174">[Installez hello Agent Java sur votre serveur](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="aea69-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="aea69-175">Vous spécifiez des méthodes hello toowatch.</span><span class="sxs-lookup"><span data-stu-id="aea69-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="aea69-176">Surveiller les appels de méthode et les dépendances externes</span><span class="sxs-lookup"><span data-stu-id="aea69-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="aea69-177">[Installer hello Agent Java](app-insights-java-agent.md) toolog spécifié méthodes internes et les appels effectués via JDBC, avec des données de temporisation.</span><span class="sxs-lookup"><span data-stu-id="aea69-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="aea69-178">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="aea69-178">Performance counters</span></span>
<span data-ttu-id="aea69-179">Dans votre Panneau de vue d’ensemble, défiler et cliquez sur hello **serveurs** vignette.</span><span class="sxs-lookup"><span data-stu-id="aea69-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="aea69-180">Vous verrez un ensemble de compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="aea69-180">You'll see a range of performance counters.</span></span>

![Faites défiler la liste en mosaïque de serveurs tooclick hello](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="aea69-182">Personnaliser la collecte des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="aea69-182">Customize performance counter collection</span></span>
<span data-ttu-id="aea69-183">collection de toodisable ensemble standard de hello des compteurs de performances, ajouter hello suivant code sous le nœud racine de hello du fichier de ApplicationInsights.xml hello :</span><span class="sxs-lookup"><span data-stu-id="aea69-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="aea69-184">Collecter des compteurs de performances supplémentaires</span><span class="sxs-lookup"><span data-stu-id="aea69-184">Collect additional performance counters</span></span>
<span data-ttu-id="aea69-185">Vous pouvez spécifier toobe de compteurs de performances supplémentaires collectées.</span><span class="sxs-lookup"><span data-stu-id="aea69-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="aea69-186">Compteurs JMX (exposées par la Machine virtuelle Java de hello)</span><span class="sxs-lookup"><span data-stu-id="aea69-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="aea69-187">`displayName`– nom hello affiché dans le portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="aea69-188">`objectName`– nom de l’objet JMX hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="aea69-189">`attribute`: attribut hello de hello JMX objet nom toofetch</span><span class="sxs-lookup"><span data-stu-id="aea69-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="aea69-190">`type`(facultatif) : hello du type d’attribut de l’objet JMX :</span><span class="sxs-lookup"><span data-stu-id="aea69-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="aea69-191">Par défaut : un type simple, comme int ou long.</span><span class="sxs-lookup"><span data-stu-id="aea69-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="aea69-192">`composite`: des données de compteur de performances hello sont au format hello de 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="aea69-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="aea69-193">`tabular`: des données de compteur de performances hello sont au format hello d’une ligne de table</span><span class="sxs-lookup"><span data-stu-id="aea69-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="aea69-194">Compteurs de performances Windows</span><span class="sxs-lookup"><span data-stu-id="aea69-194">Windows performance counters</span></span>
<span data-ttu-id="aea69-195">Chaque [compteur de performances Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) est un membre d’une catégorie (Bonjour même manière qu’un champ est un membre d’une classe).</span><span class="sxs-lookup"><span data-stu-id="aea69-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="aea69-196">Les catégories peuvent être globales ou peuvent avoir des instances numérotées ou nommées.</span><span class="sxs-lookup"><span data-stu-id="aea69-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="aea69-197">displayName : nom hello affiché dans le portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="aea69-198">nom de la catégorie : catégorie de compteur de performances hello (objet de performance) à laquelle ce compteur de performance est associé.</span><span class="sxs-lookup"><span data-stu-id="aea69-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="aea69-199">counterName – nom hello hello du compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="aea69-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="aea69-200">instanceName – nom hello de l’instance de catégorie de compteur de performance hello ou une chaîne vide (" »), si la catégorie de hello contient une seule instance.</span><span class="sxs-lookup"><span data-stu-id="aea69-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="aea69-201">Si hello categoryName est le processus et compteur de performances hello vous aimeriez toocollect est à partir de processus de machine virtuelle Java hello actuel sur lequel votre application est en cours d’exécution, spécifiez `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="aea69-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="aea69-202">Les compteurs de performances sont visibles en tant que mesures personnalisées dans [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="aea69-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="aea69-203">Compteurs de performances Unix</span><span class="sxs-lookup"><span data-stu-id="aea69-203">Unix performance counters</span></span>
* <span data-ttu-id="aea69-204">[Installer collectd avec le plug-in de hello Application Insights](app-insights-java-collectd.md) tooget une grande variété de données système et réseau.</span><span class="sxs-lookup"><span data-stu-id="aea69-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="aea69-205">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="aea69-205">Availability web tests</span></span>
<span data-ttu-id="aea69-206">Application Insights peuvent tester votre site Web à intervalles réguliers toocheck que c’est et répond bien.</span><span class="sxs-lookup"><span data-stu-id="aea69-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="aea69-207">[tooset des][availability], faites défiler vers le bas tooclick disponibilité.</span><span class="sxs-lookup"><span data-stu-id="aea69-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Faites défiler vers le bas, cliquez sur Disponibilité, puis sur Ajouter un test web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="aea69-209">Vous obtenez des graphiques du temps de réponse, ainsi que des notifications par courrier électronique si votre site ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="aea69-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemple de test web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="aea69-211">[En savoir plus sur les tests de disponibilité web.][availability]</span><span class="sxs-lookup"><span data-stu-id="aea69-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="aea69-212">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="aea69-212">Diagnostic logs</span></span>
<span data-ttu-id="aea69-213">Si vous utilisez Logback ou Log4J (version 1.2 ou version 2.0) pour le suivi, vous pouvez avoir vos journaux de trace envoyés automatiquement tooApplication Insights où vous pouvez Explorer et effectuer des recherches.</span><span class="sxs-lookup"><span data-stu-id="aea69-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="aea69-214">[En savoir plus sur les journaux de diagnostic][javalogs]</span><span class="sxs-lookup"><span data-stu-id="aea69-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="aea69-215">Télémétrie personnalisée</span><span class="sxs-lookup"><span data-stu-id="aea69-215">Custom telemetry</span></span>
<span data-ttu-id="aea69-216">Insérer quelques lignes de code dans votre toofind d’application web Java à ce que les utilisateurs sont en servent ou toohelp diagnostiquer des problèmes.</span><span class="sxs-lookup"><span data-stu-id="aea69-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="aea69-217">Vous pouvez insérer le code JavaScript des pages web et hello côté serveur Java.</span><span class="sxs-lookup"><span data-stu-id="aea69-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="aea69-218">[En savoir plus sur la télémétrie personnalisée][track]</span><span class="sxs-lookup"><span data-stu-id="aea69-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="aea69-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aea69-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="aea69-220">Détecter et diagnostiquer les problèmes</span><span class="sxs-lookup"><span data-stu-id="aea69-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="aea69-221">[Ajouter des données de télémétrie de client web] [ usage] tooget télémétrie des performances à partir du client web de hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="aea69-222">[Configurer des tests web] [ availability] toomake que votre application reste en direct et réactives.</span><span class="sxs-lookup"><span data-stu-id="aea69-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="aea69-223">[Rechercher des événements et journaux] [ diagnostic] toohelp diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="aea69-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="aea69-224">[Capturez le suivi Log4J ou Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="aea69-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="aea69-225">Suivi de l'utilisation</span><span class="sxs-lookup"><span data-stu-id="aea69-225">Track usage</span></span>
* <span data-ttu-id="aea69-226">[Ajouter des données de télémétrie de client web] [ usage] toomonitor page des vues et des mesures de l’utilisateur de base.</span><span class="sxs-lookup"><span data-stu-id="aea69-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="aea69-227">[Effectuer le suivi des événements et métriques personnalisés](app-insights-web-track-usage.md) toolearn sur la façon dont votre application est utilisée, à la fois au client de hello et le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="aea69-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
