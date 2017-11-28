---
title: aaaTroubleshoot Application Insights dans un projet de web Java
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="f8134-103">Guide de dépannage et questions-réponses concernant Application Insights pour Java</span><span class="sxs-lookup"><span data-stu-id="f8134-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="f8134-104">Vous avez des questions concernant [Azure Application Insights dans Java][java] ou vous rencontrez des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="f8134-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="f8134-105">Voici quelques conseils.</span><span class="sxs-lookup"><span data-stu-id="f8134-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="f8134-106">Erreurs de build</span><span class="sxs-lookup"><span data-stu-id="f8134-106">Build errors</span></span>
<span data-ttu-id="f8134-107">**Dans Eclipse, lors de l’ajout de hello Application Insights SDK via Maven ou Gradle, j’obtiens build ou la somme de contrôle des erreurs de validation.**</span><span class="sxs-lookup"><span data-stu-id="f8134-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="f8134-108">Si hello dépendance <version> élément utilise un modèle avec des caractères génériques (par exemple, (Maven) `<version>[1.0,)</version>` ou (Gradle) `version:'1.0.+'`), essayez de spécifier une version spécifique à la place comme `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="f8134-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="f8134-109">Consultez hello [notes de publication](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) pour la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="f8134-110">Absence de données</span><span class="sxs-lookup"><span data-stu-id="f8134-110">No data</span></span>
<span data-ttu-id="f8134-111">**J’ai ajouté Application Insights avec succès et que vous avez exécuté mon application, mais j’ai constaté jamais de données dans le portail de hello.**</span><span class="sxs-lookup"><span data-stu-id="f8134-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="f8134-112">Attendez une minute, puis cliquez sur Actualiser.</span><span class="sxs-lookup"><span data-stu-id="f8134-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="f8134-113">graphiques de Hello eux-mêmes actualiser régulièrement, mais vous pouvez également actualiser manuellement.</span><span class="sxs-lookup"><span data-stu-id="f8134-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="f8134-114">intervalle d’actualisation Hello dépend de la plage de temps hello du graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="f8134-115">Vérifiez que vous disposez d’une clé d’instrumentation définie dans le fichier de ApplicationInsights.xml hello (dans le dossier de ressources hello dans votre projet)</span><span class="sxs-lookup"><span data-stu-id="f8134-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="f8134-116">Vérifiez qu’il y a aucune `<DisableTelemetry>true</DisableTelemetry>` nœud hello du fichier xml.</span><span class="sxs-lookup"><span data-stu-id="f8134-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="f8134-117">Dans votre pare-feu, vous pouvez avoir tooopen les ports TCP 80 et 443 pour toodc.services.visualstudio.com de trafic sortant. Consultez hello [la liste complète des exceptions de pare-feu](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="f8134-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="f8134-118">Bonjour Microsoft Azure démarrer du tableau, examinez le mappage d’état service hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="f8134-119">S’il existe certaines indications d’alerte, patientez jusqu'à ce qu’ils ont retourné tooOK puis fermez et rouvrez le panneau des applications Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f8134-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="f8134-120">Activer la journalisation de fenêtre de console toohello IDE, en ajoutant un `<SDKLogger />` élément sous le nœud racine de hello dans le fichier de ApplicationInsights.xml hello (dans le dossier de ressources hello dans votre projet) et pour les entrées précédés [erreur].</span><span class="sxs-lookup"><span data-stu-id="f8134-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="f8134-121">Vérifiez que hello correct ApplicationInsights.xml fichier a été chargé avec succès par hello Kit de développement logiciel Java, en examinant les messages de sortie de la console hello pour une instruction « fichier de Configuration a été trouvé ».</span><span class="sxs-lookup"><span data-stu-id="f8134-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="f8134-122">Si le fichier de configuration hello est introuvable, vérifiez toosee de messages de sortie hello où le fichier de configuration hello est recherché et assurez-vous que hello Qu'applicationinsights.XML se trouve dans un de ces emplacements de recherche.</span><span class="sxs-lookup"><span data-stu-id="f8134-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="f8134-123">En règle générale, vous pouvez placer le fichier de configuration hello près de fichiers JAR les SDK Insights de l’Application hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="f8134-124">Par exemple : dans Tomcat, cela signifie que le dossier WEB-INF/lib de hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="f8134-125">J’ai utilisé toosee données, mais il s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="f8134-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="f8134-126">Vérifiez hello [blog de l’état](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="f8134-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="f8134-127">Vous souhaitez savoir si vous avez atteint votre quota mensuel de points de données ?</span><span class="sxs-lookup"><span data-stu-id="f8134-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="f8134-128">Ouvrez Paramètres/Quota et toofind tarification out. Le cas échéant, vous pouvez mettre à niveau votre forfait ou payer pour disposer d’une capacité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="f8134-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="f8134-129">Consultez hello [tarification schéma](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="f8134-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="f8134-130">Je ne vois pas toutes les données hello que je suis attendu</span><span class="sxs-lookup"><span data-stu-id="f8134-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="f8134-131">Ouvrez hello Quotas et la tarification de lames et vérifiez si [échantillonnage](app-insights-sampling.md) est dans l’opération.</span><span class="sxs-lookup"><span data-stu-id="f8134-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="f8134-132">(transmission de 100 % signifie que l’échantillonnage n’est pas dans l’opération). Hello service Application Insights peut être ensemble tooaccept qu’une fraction des données de télémétrie hello qui arrive à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="f8134-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="f8134-133">Cela vous permet de respecter votre quota mensuel de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f8134-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="f8134-134">Absence de données d'utilisation</span><span class="sxs-lookup"><span data-stu-id="f8134-134">No usage data</span></span>
<span data-ttu-id="f8134-135">**Je vois des données concernant les requêtes et les temps de réponse, mais rien concernant les affichages de pages, le navigateur ou les données utilisateur.**</span><span class="sxs-lookup"><span data-stu-id="f8134-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="f8134-136">Vous définissez correctement vos données de télémétrie application toosend à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="f8134-137">À présent, votre prochaine étape trop[configurer votre télémétrie toosend de pages web à partir du navigateur web de hello][usage].</span><span class="sxs-lookup"><span data-stu-id="f8134-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="f8134-138">Si votre client est une application d’un [téléphone ou d’un autre appareil][platforms], vous pouvez également envoyer la télémétrie à partir de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="f8134-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="f8134-139">Utilisez hello même tooset clé d’instrumentation de télémétrie de votre client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="f8134-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="f8134-140">les données de salutation apparaîtront dans hello même ressource Application Insights, et vous pourrez événements toocorrelate en mesure de client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="f8134-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="f8134-141">Désactivation de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="f8134-141">Disabling telemetry</span></span>
<span data-ttu-id="f8134-142">**Comment puis-je désactiver la collecte télémétrique ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="f8134-143">Dans le code :</span><span class="sxs-lookup"><span data-stu-id="f8134-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="f8134-144">**Ou**</span><span class="sxs-lookup"><span data-stu-id="f8134-144">**Or**</span></span> 

<span data-ttu-id="f8134-145">Mettre à jour ApplicationInsights.xml (dans le dossier de ressources hello dans votre projet).</span><span class="sxs-lookup"><span data-stu-id="f8134-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="f8134-146">Ajoutez les éléments suivants de hello sous le nœud racine de hello :</span><span class="sxs-lookup"><span data-stu-id="f8134-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="f8134-147">À l’aide de la méthode de hello XML, vous avez application hello de toorestart lorsque vous modifiez la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="f8134-148">Modification de la cible de hello</span><span class="sxs-lookup"><span data-stu-id="f8134-148">Changing hello target</span></span>
<span data-ttu-id="f8134-149">**Comment puis-je changer la ressource Azure à laquelle mon projet envoie des données ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="f8134-150">[Obtenir la clé d’instrumentation hello de ressource hello.][java]</span><span class="sxs-lookup"><span data-stu-id="f8134-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="f8134-151">Si vous avez ajouté Application Insights tooyour projet hello boîte à outils Azure pour Eclipse, cliquez avec le bouton droit sur votre projet web, sélectionnez **Azure**, **configurer Application Insights**et modifier la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="f8134-152">Sinon, mettre à jour de clé hello dans ApplicationInsights.xml dans le dossier de ressources hello dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="f8134-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="f8134-153">Déboguer des données à partir de hello SDK</span><span class="sxs-lookup"><span data-stu-id="f8134-153">Debug data from hello SDK</span></span>

<span data-ttu-id="f8134-154">**Comment puis-je savoir quel hello effectue un kit de développement logiciel ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="f8134-155">Ajout de plus d’informations sur ce qui se passe dans hello API, tooget `<SDKLogger/>` sous le nœud racine de hello hello ApplicationInsights.xml du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="f8134-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="f8134-156">Vous pouvez également demander à fichier de tooa toooutput hello enregistreur d’événements :</span><span class="sxs-lookup"><span data-stu-id="f8134-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="f8134-157">Vous trouverez les fichiers Hello sous `%temp%\javasdklogs` ou `java.io.tmpdir` en cas de serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f8134-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="f8134-158">écran de démarrage Azure Hello</span><span class="sxs-lookup"><span data-stu-id="f8134-158">hello Azure start screen</span></span>
<span data-ttu-id="f8134-159">**Je regarde [hello Azure portal](https://portal.azure.com). Mappage de hello indique quelque chose sur mon application ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="f8134-160">Non, il affiche la santé des serveurs Windows Azure hello monde hello.</span><span class="sxs-lookup"><span data-stu-id="f8134-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="f8134-161">*À partir du tableau de démarrage Azure hello (écran d’accueil), comment rechercher données relatives à mon application ?*</span><span class="sxs-lookup"><span data-stu-id="f8134-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="f8134-162">En supposant que vous [configurer votre application pour Application Insights][java], cliquez sur Parcourir, sélectionnez Application Insights et sélectionnez les ressources d’application hello vous avez créé pour votre application.</span><span class="sxs-lookup"><span data-stu-id="f8134-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="f8134-163">tooget il plus rapidement à l’avenir, vous pouvez épingler votre application toohello démarrer votre tableau.</span><span class="sxs-lookup"><span data-stu-id="f8134-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="f8134-164">Serveurs intranet</span><span class="sxs-lookup"><span data-stu-id="f8134-164">Intranet servers</span></span>
<span data-ttu-id="f8134-165">**Puis-je surveiller un serveur sur mon intranet ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="f8134-166">Oui, la condition de votre serveur peut envoyer le portail d’Application Insights toohello télémétrie via hello internet public.</span><span class="sxs-lookup"><span data-stu-id="f8134-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="f8134-167">Dans votre pare-feu, vous pouvez avoir tooopen les ports TCP 80 et 443 pour toodc.services.visualstudio.com de trafic sortant et f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="f8134-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="f8134-168">Conservation des données</span><span class="sxs-lookup"><span data-stu-id="f8134-168">Data retention</span></span>
<span data-ttu-id="f8134-169">**La durée pendant laquelle les données sont conservées dans le portail de hello ? Sont-elles sécurisées ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="f8134-170">Consultez [Rétention des données et confidentialité][data].</span><span class="sxs-lookup"><span data-stu-id="f8134-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8134-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8134-171">Next steps</span></span>
<span data-ttu-id="f8134-172">**J’ai configuré Application Insights pour mon application serveur Java. Que puis-je faire d’autre ?**</span><span class="sxs-lookup"><span data-stu-id="f8134-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="f8134-173">[Surveiller la disponibilité de vos pages web][availability]</span><span class="sxs-lookup"><span data-stu-id="f8134-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="f8134-174">[Surveiller l’utilisation des pages web][usage]</span><span class="sxs-lookup"><span data-stu-id="f8134-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="f8134-175">[Suivre l’utilisation de vos applications et diagnostiquer les problèmes des applications de vos appareils][platforms]</span><span class="sxs-lookup"><span data-stu-id="f8134-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="f8134-176">[Écrire l’utilisation tootrack du code de votre application][track]</span><span class="sxs-lookup"><span data-stu-id="f8134-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="f8134-177">[Capturer les journaux de diagnostic][javalogs]</span><span class="sxs-lookup"><span data-stu-id="f8134-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="f8134-178">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="f8134-178">Get help</span></span>
* [<span data-ttu-id="f8134-179">Dépassement de capacité de la pile</span><span class="sxs-lookup"><span data-stu-id="f8134-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

