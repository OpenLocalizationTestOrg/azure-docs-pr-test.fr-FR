---
title: "Résolution des problèmes d'Application Insights dans un projet web Java"
description: "Guide de dépannage : surveillance des applications Java en direct avec Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="c67c4-103">Guide de dépannage et questions-réponses concernant Application Insights pour Java</span><span class="sxs-lookup"><span data-stu-id="c67c4-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="c67c4-104">Vous avez des questions concernant [Azure Application Insights dans Java][java] ou vous rencontrez des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="c67c4-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="c67c4-105">Voici quelques conseils.</span><span class="sxs-lookup"><span data-stu-id="c67c4-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="c67c4-106">Erreurs de build</span><span class="sxs-lookup"><span data-stu-id="c67c4-106">Build errors</span></span>
<span data-ttu-id="c67c4-107">**Dans Eclipse, quand j’ajoute le kit de développement logiciel (SDK) Application Insights via Maven ou Gradle, j’obtiens des erreurs de validation de build ou de somme de contrôle.**</span><span class="sxs-lookup"><span data-stu-id="c67c4-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="c67c4-108">Si l’élément <version>de dépendance utilise un modèle avec des caractères génériques (par exemple, (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), essayez de spécifier une version spécifique, comme par exemple  `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="c67c4-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="c67c4-109">Consultez les [notes de publication](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) relatives à la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c67c4-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="c67c4-110">Absence de données</span><span class="sxs-lookup"><span data-stu-id="c67c4-110">No data</span></span>
<span data-ttu-id="c67c4-111">**J’ai ajouté Application Insights sans problème et exécuté mon application, mais je ne vois aucune donnée dans le portail.**</span><span class="sxs-lookup"><span data-stu-id="c67c4-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="c67c4-112">Attendez une minute, puis cliquez sur Actualiser.</span><span class="sxs-lookup"><span data-stu-id="c67c4-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="c67c4-113">Les graphiques s’actualisent à intervalles réguliers, mais vous pouvez également les actualiser manuellement.</span><span class="sxs-lookup"><span data-stu-id="c67c4-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="c67c4-114">L’intervalle d’actualisation dépend de l’intervalle de temps sur lequel porte le graphique.</span><span class="sxs-lookup"><span data-stu-id="c67c4-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="c67c4-115">Vérifiez que vous disposez d'une clé d'instrumentation définie dans le fichier ApplicationInsights.xml (situé dans le dossier de ressources de votre projet)</span><span class="sxs-lookup"><span data-stu-id="c67c4-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="c67c4-116">Vérifiez qu’aucun nœud `<DisableTelemetry>true</DisableTelemetry>` ne se trouve dans le fichier .xml.</span><span class="sxs-lookup"><span data-stu-id="c67c4-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="c67c4-117">Vous devrez ouvrir les ports TCP 80 et 443 de votre pare-feu pour le trafic sortant vers dc.services.visualstudio.com. Consultez la [liste complète des exceptions de pare-feu](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="c67c4-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="c67c4-118">Dans le panneau de démarrage Microsoft Azure, examinez la carte d'état du service.</span><span class="sxs-lookup"><span data-stu-id="c67c4-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="c67c4-119">Si des alertes sont indiquées, attendez qu'elles soient corrigées (OK), puis fermez et rouvrez le volet de votre application Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c67c4-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="c67c4-120">Activez la journalisation dans la fenêtre de console IDE en ajoutant un élément `<SDKLogger />` sous le nœud racine dans le fichier ApplicationInsights.xml (situé dans le dossier de ressources de votre projet), puis vérifiez les entrées précédées du mot [Error].</span><span class="sxs-lookup"><span data-stu-id="c67c4-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="c67c4-121">Assurez-vous que le fichier ApplicationInsights.xml approprié a été correctement chargé par le Kit de développement logiciel (SDK) Java, en vérifiant que le message de sortie de la console « Le fichier de configuration a été trouvé » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c67c4-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="c67c4-122">Si le fichier de configuration est introuvable, vérifiez les messages de sortie pour voir où cette recherche a été effectuée et vous assurer que le fichier ApplicationInsights.xml se trouve dans l’un des emplacements de recherche.</span><span class="sxs-lookup"><span data-stu-id="c67c4-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="c67c4-123">En règle générale, vous pouvez placer le fichier de configuration près du JAR du Kit de développement logiciel (SDK) Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c67c4-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="c67c4-124">Par exemple, il s’agit du dossier WEB-INF/lib dans Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c67c4-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="c67c4-125">Je pouvais voir les données, mais plus maintenant</span><span class="sxs-lookup"><span data-stu-id="c67c4-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="c67c4-126">Vérifiez le [blog d'état](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="c67c4-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="c67c4-127">Vous souhaitez savoir si vous avez atteint votre quota mensuel de points de données ?</span><span class="sxs-lookup"><span data-stu-id="c67c4-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="c67c4-128">Ouvrez Paramètres/Quota et tarification pour le savoir. Le cas échéant, vous pouvez mettre à niveau votre forfait ou payer pour disposer d’une capacité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c67c4-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="c67c4-129">Consultez le [mécanisme de tarification](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c67c4-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="c67c4-130">Je ne vois pas toutes les données que j’attends</span><span class="sxs-lookup"><span data-stu-id="c67c4-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="c67c4-131">Ouvrez le panneau Quotas et tarification et vérifiez si l’ [échantillonnage](app-insights-sampling.md) est activé.</span><span class="sxs-lookup"><span data-stu-id="c67c4-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="c67c4-132">(Une transmission de 100 % signifie que l’échantillonnage n’est pas activé). Le service Application Insights peut être défini pour n’accepter qu’une fraction des données de télémétrie provenant de votre application.</span><span class="sxs-lookup"><span data-stu-id="c67c4-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="c67c4-133">Cela vous permet de respecter votre quota mensuel de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c67c4-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="c67c4-134">Absence de données d'utilisation</span><span class="sxs-lookup"><span data-stu-id="c67c4-134">No usage data</span></span>
<span data-ttu-id="c67c4-135">**Je vois des données concernant les requêtes et les temps de réponse, mais rien concernant les affichages de pages, le navigateur ou les données utilisateur.**</span><span class="sxs-lookup"><span data-stu-id="c67c4-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="c67c4-136">Assurez-vous d'avoir configuré correctement votre application de façon à envoyer la télémétrie depuis le serveur.</span><span class="sxs-lookup"><span data-stu-id="c67c4-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="c67c4-137">L’étape suivante consiste à [configurer vos pages web pour l’envoi de la télémétrie depuis le navigateur web][usage].</span><span class="sxs-lookup"><span data-stu-id="c67c4-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="c67c4-138">Si votre client est une application d’un [téléphone ou d’un autre appareil][platforms], vous pouvez également envoyer la télémétrie à partir de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="c67c4-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="c67c4-139">Utilisez la même clé d'instrumentation pour configurer la télémétrie de votre client et de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="c67c4-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="c67c4-140">Les données apparaîtront dans la même ressource Application Insights, et vous pourrez mettre en corrélation les événements du serveur et du client.</span><span class="sxs-lookup"><span data-stu-id="c67c4-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="c67c4-141">Désactivation de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="c67c4-141">Disabling telemetry</span></span>
<span data-ttu-id="c67c4-142">**Comment puis-je désactiver la collecte télémétrique ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="c67c4-143">Dans le code :</span><span class="sxs-lookup"><span data-stu-id="c67c4-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="c67c4-144">**Ou**</span><span class="sxs-lookup"><span data-stu-id="c67c4-144">**Or**</span></span> 

<span data-ttu-id="c67c4-145">Mettez à jour ApplicationInsights.xml (situé dans le dossier de ressources de votre projet).</span><span class="sxs-lookup"><span data-stu-id="c67c4-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="c67c4-146">Ajoutez le code suivant sous le nœud racine :</span><span class="sxs-lookup"><span data-stu-id="c67c4-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="c67c4-147">À l'aide de la méthode XML, vous devrez redémarrer l'application si vous modifiez la valeur.</span><span class="sxs-lookup"><span data-stu-id="c67c4-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="c67c4-148">Modification de la cible</span><span class="sxs-lookup"><span data-stu-id="c67c4-148">Changing the target</span></span>
<span data-ttu-id="c67c4-149">**Comment puis-je changer la ressource Azure à laquelle mon projet envoie des données ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="c67c4-150">[Obtenez la clé d’instrumentation de la nouvelle ressource.][java]</span><span class="sxs-lookup"><span data-stu-id="c67c4-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="c67c4-151">Si vous avez ajouté Application Insights à votre projet à l’aide du kit de ressources Azure pour Eclipse, cliquez avec le bouton droit sur votre projet web, sélectionnez **Azure**, **Configurer Application Insights**, puis modifiez la clé.</span><span class="sxs-lookup"><span data-stu-id="c67c4-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="c67c4-152">Sinon, mettez à jour la clé du fichier ApplicationInsights.xml (situé dans le dossier de ressources de votre projet).</span><span class="sxs-lookup"><span data-stu-id="c67c4-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="c67c4-153">Données de débogage du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="c67c4-153">Debug data from the SDK</span></span>

<span data-ttu-id="c67c4-154">**Comment puis-je savoir ce que fait le Kit de développement logiciel (SDK) ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="c67c4-155">Pour obtenir plus d’informations sur ce qui se passe dans l’API, ajoutez `<SDKLogger/>` sous le nœud racine du fichier de configuration ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="c67c4-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="c67c4-156">Vous pouvez également demander à l’enregistreur d’événements une sortie vers un fichier :</span><span class="sxs-lookup"><span data-stu-id="c67c4-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="c67c4-157">Vous trouverez les fichiers sous `%temp%\javasdklogs` ou `java.io.tmpdir` si vous utilisez un serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c67c4-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="c67c4-158">L'écran d'accueil Azure</span><span class="sxs-lookup"><span data-stu-id="c67c4-158">The Azure start screen</span></span>
<span data-ttu-id="c67c4-159">**J’ai ouvert [le portail Azure](https://portal.azure.com). Est-ce que la carte fournit des informations concernant mon application ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="c67c4-160">Non, elle montre l'intégrité des serveurs Azure dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="c67c4-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="c67c4-161">*Depuis le panneau de démarrage Azure (l’écran d’accueil), comment trouver les données relatives à mon application ?*</span><span class="sxs-lookup"><span data-stu-id="c67c4-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="c67c4-162">En supposant que vous ayez [configuré votre application pour Application Insights][java], cliquez sur Parcourir, sélectionnez Application Insights, puis sélectionnez la ressource d’application que vous avez créée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="c67c4-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="c67c4-163">Pour aller plus vite la prochaine fois, vous pouvez épingler votre application au panneau de démarrage.</span><span class="sxs-lookup"><span data-stu-id="c67c4-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="c67c4-164">Serveurs intranet</span><span class="sxs-lookup"><span data-stu-id="c67c4-164">Intranet servers</span></span>
<span data-ttu-id="c67c4-165">**Puis-je surveiller un serveur sur mon intranet ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="c67c4-166">Oui, à condition que votre serveur puisse envoyer la télémétrie vers le portail Application Insights via l'Internet public.</span><span class="sxs-lookup"><span data-stu-id="c67c4-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="c67c4-167">Vous devrez ouvrir les ports TCP 80 et 443 de votre pare-feu pour le trafic sortant vers dc.services.visualstudio.com et f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="c67c4-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="c67c4-168">Conservation des données</span><span class="sxs-lookup"><span data-stu-id="c67c4-168">Data retention</span></span>
<span data-ttu-id="c67c4-169">**Combien de temps les données sont-elles conservées dans le portail ? Sont-elles sécurisées ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="c67c4-170">Consultez [Rétention des données et confidentialité][data].</span><span class="sxs-lookup"><span data-stu-id="c67c4-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c67c4-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c67c4-171">Next steps</span></span>
<span data-ttu-id="c67c4-172">**J’ai configuré Application Insights pour mon application serveur Java. Que puis-je faire d’autre ?**</span><span class="sxs-lookup"><span data-stu-id="c67c4-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="c67c4-173">[Surveiller la disponibilité de vos pages web][availability]</span><span class="sxs-lookup"><span data-stu-id="c67c4-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="c67c4-174">[Surveiller l’utilisation des pages web][usage]</span><span class="sxs-lookup"><span data-stu-id="c67c4-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="c67c4-175">[Suivre l’utilisation de vos applications et diagnostiquer les problèmes des applications de vos appareils][platforms]</span><span class="sxs-lookup"><span data-stu-id="c67c4-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="c67c4-176">[Écrire du code pour suivre l’utilisation de votre application][track]</span><span class="sxs-lookup"><span data-stu-id="c67c4-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="c67c4-177">[Capturer les journaux de diagnostic][javalogs]</span><span class="sxs-lookup"><span data-stu-id="c67c4-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="c67c4-178">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="c67c4-178">Get help</span></span>
* [<span data-ttu-id="c67c4-179">Dépassement de capacité de la pile</span><span class="sxs-lookup"><span data-stu-id="c67c4-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

