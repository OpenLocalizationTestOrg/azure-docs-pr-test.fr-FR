---
title: "Prise en main d’Azure Application Insights avec Java dans Eclipse | Microsoft Docs"
description: "Le plug-in Eclipse permet d’ajouter la surveillance des performances et de l’utilisation de votre site web Java avec Application Insights"
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="e8d75-103">Prise en main d’Application Insights avec Java dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="e8d75-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="e8d75-104">Le Kit de développement logiciel (SDK) Application Insights envoie la télémétrie de votre application web Java afin que vous puissiez en analyser les performances et l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="e8d75-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="e8d75-105">Le plug-in Eclipse pour Application Insights installe automatiquement le Kit de développement logiciel (SDK) dans votre projet pour pouvoir bénéficier de la télémétrie de base, plus une API avec laquelle vous pouvez écrire des éléments de télémétrie personnalisés.</span><span class="sxs-lookup"><span data-stu-id="e8d75-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="e8d75-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e8d75-106">Prerequisites</span></span>
<span data-ttu-id="e8d75-107">Actuellement, le plug-in fonctionne pour les projets Web dynamiques dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e8d75-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="e8d75-108">([Ajout d’Application Insights à d’autres types de projets Java][java].)</span><span class="sxs-lookup"><span data-stu-id="e8d75-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="e8d75-109">Vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e8d75-109">You'll need:</span></span>

* <span data-ttu-id="e8d75-110">Oracle JRE 1.6 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="e8d75-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="e8d75-111">Un abonnement à [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e8d75-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="e8d75-112">[IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/downloads/), Indigo ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e8d75-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="e8d75-113">Windows 7 ou version ultérieure ou Windows Server 2008 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="e8d75-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="e8d75-114">Installer le Kit de développement logiciel (SDK) sur Eclipse (opération unique)</span><span class="sxs-lookup"><span data-stu-id="e8d75-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="e8d75-115">Vous ne devez effectuer cette opération qu’une seule fois par machine.</span><span class="sxs-lookup"><span data-stu-id="e8d75-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="e8d75-116">Cette étape installe un kit de ressources qui peut ensuite ajouter le Kit de développement logiciel (SDK) pour chaque projet web dynamique.</span><span class="sxs-lookup"><span data-stu-id="e8d75-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="e8d75-117">Dans Eclipse, cliquez sur Aide, Installer un nouveau logiciel.</span><span class="sxs-lookup"><span data-stu-id="e8d75-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Aide, installation de nouveaux logiciels](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="e8d75-119">Le Kit de développement logiciel (SDK) est disponible à l'adresse http://dl.microsoft.com/eclipse, sous Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="e8d75-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="e8d75-120">Désactivez l’option **Contacter tous les sites de mise à jour...**</span><span class="sxs-lookup"><span data-stu-id="e8d75-120">Uncheck **Contact all update sites...**</span></span>

    ![Pour le Kit de développement logiciel (SDK) Application Insights, désactivez Contacter tous les sites de mise à jour.](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="e8d75-122">Suivez les étapes restantes pour chaque projet Java.</span><span class="sxs-lookup"><span data-stu-id="e8d75-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="e8d75-123">Créer une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="e8d75-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="e8d75-124">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8d75-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e8d75-125">Créez une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8d75-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="e8d75-126">Définissez le type d’application sur Application web Java.</span><span class="sxs-lookup"><span data-stu-id="e8d75-126">Set the application type to Java web application.</span></span>  

    ![Cliquez sur + et choisissez Ajouter Application Insights.](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="e8d75-128">Obtenez la clé d'instrumentation de la nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="e8d75-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="e8d75-129">Vous devrez la coller rapidement dans le code de votre projet.</span><span class="sxs-lookup"><span data-stu-id="e8d75-129">You'll need to paste this into your code project shortly.</span></span>  

    ![Dans la nouvelle vue d’ensemble des ressources, cliquez sur Propriétés et copiez la clé d’instrumentation.](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="e8d75-131">Ajout de Application Insights à votre projet</span><span class="sxs-lookup"><span data-stu-id="e8d75-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="e8d75-132">Ajoutez Application Insights à partir du menu contextuel de votre projet Web Java.</span><span class="sxs-lookup"><span data-stu-id="e8d75-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![Dans la nouvelle vue d’ensemble des ressources, cliquez sur Propriétés et copiez la clé d’instrumentation.](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="e8d75-134">Collez la clé d’instrumentation que vous avez obtenue sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e8d75-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![Dans la nouvelle vue d’ensemble des ressources, cliquez sur Propriétés et copiez la clé d’instrumentation.](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="e8d75-136">La clé est envoyée avec chaque élément de télémétrie et indique à Application Insights de l’afficher dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="e8d75-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="e8d75-137">Exécuter l’application et consulter les mesures</span><span class="sxs-lookup"><span data-stu-id="e8d75-137">Run the application and see metrics</span></span>
<span data-ttu-id="e8d75-138">Exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="e8d75-138">Run your application.</span></span>

<span data-ttu-id="e8d75-139">Revenez à votre ressource Application Insights dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8d75-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="e8d75-140">Les données des demandes HTTP apparaissent dans le panneau Vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="e8d75-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="e8d75-141">(Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).</span><span class="sxs-lookup"><span data-stu-id="e8d75-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="e8d75-142">Réponse du serveur, nombre de demandes et échecs</span><span class="sxs-lookup"><span data-stu-id="e8d75-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="e8d75-143">Cliquez sur un des graphiques pour afficher des mesures plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="e8d75-143">Click through any chart to see more detailed metrics.</span></span>

![Nombres de demandes par nom](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="e8d75-145">[En savoir plus sur les mesures.][metrics]</span><span class="sxs-lookup"><span data-stu-id="e8d75-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="e8d75-146">Et lorsque vous affichez les propriétés d'une demande, vous voyez les événements de télémétrie associés, par exemple les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="e8d75-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Tous le suivi pour cette demande](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="e8d75-148">Télémétrie côté client</span><span class="sxs-lookup"><span data-stu-id="e8d75-148">Client-side telemetry</span></span>
<span data-ttu-id="e8d75-149">Dans le panneau Démarrage rapide, cliquez sur Obtenir le code pour analyser mes pages web :</span><span class="sxs-lookup"><span data-stu-id="e8d75-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![Dans le panneau de vue d’ensemble de l’application, cliquez sur Démarrage rapide, Obtenir le code pour analyser mes pages web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="e8d75-152">Insérez l'extrait de code dans l’en-tête de vos fichiers HTML.</span><span class="sxs-lookup"><span data-stu-id="e8d75-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="e8d75-153">Affichage des données côté client</span><span class="sxs-lookup"><span data-stu-id="e8d75-153">View client-side data</span></span>
<span data-ttu-id="e8d75-154">Ouvrez et utilisez vos pages web mises à jour.</span><span class="sxs-lookup"><span data-stu-id="e8d75-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="e8d75-155">Attendez une minute ou deux, puis revenez dans Application Insights et ouvrez le panneau d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="e8d75-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="e8d75-156">(Dans le panneau Vue d'ensemble, faites défiler vers le bas et cliquez sur Utilisation.)</span><span class="sxs-lookup"><span data-stu-id="e8d75-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="e8d75-157">Les mesures liées au nombre de consultations de la page, à l’utilisateur et à la session s’affichent dans le panneau d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="e8d75-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Sessions, utilisateurs et affichages de pages](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="e8d75-159">[En savoir plus sur la configuration de la télémétrie côté client.][usage]</span><span class="sxs-lookup"><span data-stu-id="e8d75-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="e8d75-160">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="e8d75-160">Publish your application</span></span>
<span data-ttu-id="e8d75-161">Publiez maintenant votre application sur le serveur, laissez le temps aux usagers de l’utiliser, puis observez les données de télémétrie qui s’affichent sur le portail.</span><span class="sxs-lookup"><span data-stu-id="e8d75-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="e8d75-162">Assurez-vous que votre pare-feu autorise votre application à envoyer les données de télémétrie vers ces ports :</span><span class="sxs-lookup"><span data-stu-id="e8d75-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="e8d75-163">dc.services.VisualStudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e8d75-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="e8d75-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="e8d75-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="e8d75-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e8d75-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="e8d75-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="e8d75-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="e8d75-167">Sur les serveurs Windows, installez :</span><span class="sxs-lookup"><span data-stu-id="e8d75-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="e8d75-168">Redistribuable Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="e8d75-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="e8d75-169">(Cette opération active les compteurs de performances.)</span><span class="sxs-lookup"><span data-stu-id="e8d75-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="e8d75-170">Exceptions et échecs de requêtes</span><span class="sxs-lookup"><span data-stu-id="e8d75-170">Exceptions and request failures</span></span>
<span data-ttu-id="e8d75-171">Les exceptions non gérées sont collectées automatiquement :</span><span class="sxs-lookup"><span data-stu-id="e8d75-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="e8d75-172">Pour collecter les données concernant d’autres exceptions, vous disposez de deux options :</span><span class="sxs-lookup"><span data-stu-id="e8d75-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="e8d75-173">[Insérez des appels à TrackException dans votre code](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="e8d75-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="e8d75-174">[Installez l’agent Java sur votre serveur](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="e8d75-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="e8d75-175">Vous spécifiez les méthodes que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="e8d75-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="e8d75-176">Surveiller les appels de méthode et les dépendances externes</span><span class="sxs-lookup"><span data-stu-id="e8d75-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="e8d75-177">[Installez l’agent Java](app-insights-java-agent.md) pour journaliser les méthodes internes spécifiées et les appels effectués via JDBC, avec des données de minutage.</span><span class="sxs-lookup"><span data-stu-id="e8d75-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="e8d75-178">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="e8d75-178">Performance counters</span></span>
<span data-ttu-id="e8d75-179">Dans le panneau Vue d'ensemble, faites défiler vers le bas et cliquez sur la vignette **Serveurs**.</span><span class="sxs-lookup"><span data-stu-id="e8d75-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="e8d75-180">Vous verrez un ensemble de compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="e8d75-180">You'll see a range of performance counters.</span></span>

![Faites défiler vers le bas pour cliquer sur la vignette des serveurs](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="e8d75-182">Personnaliser la collecte des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="e8d75-182">Customize performance counter collection</span></span>
<span data-ttu-id="e8d75-183">Pour désactiver la collecte du jeu standard de compteurs de performances, ajoutez le code suivant sous le nœud racine du fichier ApplicationInsights.xml :</span><span class="sxs-lookup"><span data-stu-id="e8d75-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="e8d75-184">Collecter des compteurs de performances supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e8d75-184">Collect additional performance counters</span></span>
<span data-ttu-id="e8d75-185">Vous pouvez spécifier d'autres compteurs de performances à collecter.</span><span class="sxs-lookup"><span data-stu-id="e8d75-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="e8d75-186">Compteurs JMX (exposés par la machine virtuelle Java)</span><span class="sxs-lookup"><span data-stu-id="e8d75-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="e8d75-187">`displayName` : nom affiché sur le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8d75-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="e8d75-188">`objectName` : nom de l'objet JMX.</span><span class="sxs-lookup"><span data-stu-id="e8d75-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="e8d75-189">`attribute` attribut du nom d'objet JMX à récupérer</span><span class="sxs-lookup"><span data-stu-id="e8d75-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="e8d75-190">`type` (facultatif) : type d'attribut d'objet JMX :</span><span class="sxs-lookup"><span data-stu-id="e8d75-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="e8d75-191">Par défaut : un type simple, comme int ou long.</span><span class="sxs-lookup"><span data-stu-id="e8d75-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="e8d75-192">`composite`: les données du compteur de performances sont au format « Attribute.Data »</span><span class="sxs-lookup"><span data-stu-id="e8d75-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="e8d75-193">`tabular`: les données du compteur de performances sont au format ligne de tableau</span><span class="sxs-lookup"><span data-stu-id="e8d75-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="e8d75-194">Compteurs de performances Windows</span><span class="sxs-lookup"><span data-stu-id="e8d75-194">Windows performance counters</span></span>
<span data-ttu-id="e8d75-195">Chaque [compteur de performances Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) est un membre d'une catégorie (de la même façon qu'un champ est un membre d'une classe).</span><span class="sxs-lookup"><span data-stu-id="e8d75-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="e8d75-196">Les catégories peuvent être globales ou peuvent avoir des instances numérotées ou nommées.</span><span class="sxs-lookup"><span data-stu-id="e8d75-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="e8d75-197">displayName : nom affiché sur le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8d75-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="e8d75-198">categoryName : catégorie du compteur de performances (objet de performances) à laquelle ce compteur de performances est associé.</span><span class="sxs-lookup"><span data-stu-id="e8d75-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="e8d75-199">counterName : nom du compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="e8d75-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="e8d75-200">instanceName : nom de l'instance de catégorie de compteur de performances ou une chaîne vide ("") si la catégorie contient une seule instance.</span><span class="sxs-lookup"><span data-stu-id="e8d75-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="e8d75-201">Si categoryName est Process et que le compteur de performance que vous souhaitez collecter vient du processus en cours de la JVM sur laquelle votre application s'exécute, spécifiez `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="e8d75-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="e8d75-202">Les compteurs de performances sont visibles en tant que mesures personnalisées dans [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="e8d75-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="e8d75-203">Compteurs de performances Unix</span><span class="sxs-lookup"><span data-stu-id="e8d75-203">Unix performance counters</span></span>
* <span data-ttu-id="e8d75-204">[Installez collectd avec le plug-in Application Insights](app-insights-java-collectd.md) pour obtenir une grande variété de données sur le système et le réseau.</span><span class="sxs-lookup"><span data-stu-id="e8d75-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="e8d75-205">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="e8d75-205">Availability web tests</span></span>
<span data-ttu-id="e8d75-206">Application Insights peut tester votre site web à intervalles réguliers pour vérifier qu’il fonctionne et répond correctement.</span><span class="sxs-lookup"><span data-stu-id="e8d75-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="e8d75-207">Pour exécuter la [configuration][availability], faites défiler la liste vers le bas pour cliquer sur Disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e8d75-207">[To set up][availability], scroll down to click Availability.</span></span>

![Faites défiler vers le bas, cliquez sur Disponibilité, puis sur Ajouter un test web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="e8d75-209">Vous obtenez des graphiques du temps de réponse, ainsi que des notifications par courrier électronique si votre site ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="e8d75-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemple de test web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="e8d75-211">[En savoir plus sur les tests de disponibilité web.][availability]</span><span class="sxs-lookup"><span data-stu-id="e8d75-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="e8d75-212">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e8d75-212">Diagnostic logs</span></span>
<span data-ttu-id="e8d75-213">Si vous utilisez Logback ou Log4J (v1.2 ou v2.0) pour le suivi, vous pouvez faire en sorte que vos journaux de suivi soient envoyés automatiquement à Application Insights, où vous pouvez les explorer et effectuer des recherches.</span><span class="sxs-lookup"><span data-stu-id="e8d75-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="e8d75-214">[En savoir plus sur les journaux de diagnostic][javalogs]</span><span class="sxs-lookup"><span data-stu-id="e8d75-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="e8d75-215">Télémétrie personnalisée</span><span class="sxs-lookup"><span data-stu-id="e8d75-215">Custom telemetry</span></span>
<span data-ttu-id="e8d75-216">Insérez quelques lignes de code dans votre application web Java pour découvrir ce qu’en font les utilisateurs ou pour faciliter le diagnostic des problèmes.</span><span class="sxs-lookup"><span data-stu-id="e8d75-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="e8d75-217">Vous pouvez insérer le code dans le JavaScript de la page web et dans le Java côté serveur.</span><span class="sxs-lookup"><span data-stu-id="e8d75-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="e8d75-218">[En savoir plus sur la télémétrie personnalisée][track]</span><span class="sxs-lookup"><span data-stu-id="e8d75-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8d75-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8d75-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="e8d75-220">Détecter et diagnostiquer les problèmes</span><span class="sxs-lookup"><span data-stu-id="e8d75-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="e8d75-221">[Ajoutez la télémétrie de client web][usage] pour obtenir la télémétrie des performances du client web.</span><span class="sxs-lookup"><span data-stu-id="e8d75-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="e8d75-222">[Configurez les tests web][availability] pour vous assurer que votre application est bien active.</span><span class="sxs-lookup"><span data-stu-id="e8d75-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="e8d75-223">[Recherchez les événements et les journaux][diagnostic] pour diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="e8d75-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="e8d75-224">[Capturez le suivi Log4J ou Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="e8d75-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="e8d75-225">Suivi de l'utilisation</span><span class="sxs-lookup"><span data-stu-id="e8d75-225">Track usage</span></span>
* <span data-ttu-id="e8d75-226">[Ajoutez la télémétrie de client web][usage] pour surveiller les affichages de page et autres mesures des utilisateurs de la version Basic.</span><span class="sxs-lookup"><span data-stu-id="e8d75-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="e8d75-227">[Suivez des événements et des mesures personnalisés](app-insights-web-track-usage.md) pour en savoir plus sur la façon dont votre application est utilisée, à la fois sur le client et sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="e8d75-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
