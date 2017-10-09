---
title: "aaaExport tooPower BI à partir de l’Application Insights | Documents Microsoft"
description: "Les requêtes Analytics peuvent être affichées dans Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="38c11-103">Alimentation de Power BI à partir d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="38c11-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="38c11-104">[Power BI](http://www.powerbi.com/) est une suite d’outils d’analyse métiers permettant d’analyser les données et de partager les informations.</span><span class="sxs-lookup"><span data-stu-id="38c11-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="38c11-105">Chaque périphérique bénéficie de tableaux de bord riches.</span><span class="sxs-lookup"><span data-stu-id="38c11-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="38c11-106">Vous pouvez combiner des données provenant de nombreuses sources, notamment des requêtes Analytics d’[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38c11-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="38c11-107">Il existe trois méthodes recommandées de l’exportation des données de Application Insights tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="38c11-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="38c11-108">Vous pouvez les utiliser séparément ou ensemble.</span><span class="sxs-lookup"><span data-stu-id="38c11-108">You can use them separately or together.</span></span>

* <span data-ttu-id="38c11-109">[**Adaptateur Power BI**](#power-pi-adapter) : configurez un tableau de bord complet des données de télémétrie à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="38c11-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="38c11-110">ensemble de Hello de graphiques est prédéfinie, mais vous pouvez ajouter vos propres requêtes à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="38c11-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="38c11-111">[**Exporter des requêtes d’Analytique** ](#export-analytics-queries) -écrire une requête de votre choix à l’aide d’Analytique, exportez-le tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="38c11-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="38c11-112">Vous pouvez placer cette requête sur un tableau de bord, avec d’autres données.</span><span class="sxs-lookup"><span data-stu-id="38c11-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="38c11-113">[**Exportation continue et flux de données Analytique** ](app-insights-export-stream-analytics.md) -cela implique tooset de travail plus haut.</span><span class="sxs-lookup"><span data-stu-id="38c11-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="38c11-114">Il est utile si vous souhaitez que tookeep vos données pendant de longues périodes.</span><span class="sxs-lookup"><span data-stu-id="38c11-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="38c11-115">Dans le cas contraire, hello autres méthodes sont recommandées.</span><span class="sxs-lookup"><span data-stu-id="38c11-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="38c11-116">Adaptateur Power BI</span><span class="sxs-lookup"><span data-stu-id="38c11-116">Power BI adapter</span></span>
<span data-ttu-id="38c11-117">Cette méthode crée un tableau de bord complet des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="38c11-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="38c11-118">jeu de données initial Hello est prédéfinie, mais vous pouvez ajouter plusieurs tooit de données.</span><span class="sxs-lookup"><span data-stu-id="38c11-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="38c11-119">Obtenir de l’adaptateur hello</span><span class="sxs-lookup"><span data-stu-id="38c11-119">Get hello adapter</span></span>
1. <span data-ttu-id="38c11-120">Connectez-vous trop[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="38c11-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="38c11-121">Ouvrez **Obtenir des données**, **Services**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="38c11-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Obtenir à partir d’une source de données Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="38c11-123">Fournissent des détails de votre ressource Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="38c11-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Obtenir à partir d’une source de données Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="38c11-125">Patientez une minute ou deux pour hello toobe de données importée.</span><span class="sxs-lookup"><span data-stu-id="38c11-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Adaptateur Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="38c11-127">Vous pouvez modifier du tableau de bord hello, en combinant des graphiques d’Application Insights hello avec ceux d’autres sources et avec les requêtes d’Analytique.</span><span class="sxs-lookup"><span data-stu-id="38c11-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="38c11-128">Il existe une galerie de visualisation où vous pouvez obtenir plus de graphiques. Chaque graphique comporte des paramètres que vous pouvez définir.</span><span class="sxs-lookup"><span data-stu-id="38c11-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="38c11-129">Une fois l’importation initiale de hello, tableau de bord hello et rapports de hello continuent tooupdate tous les jours.</span><span class="sxs-lookup"><span data-stu-id="38c11-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="38c11-130">Vous pouvez contrôler la planification d’actualisation hello hello le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="38c11-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="38c11-131">Exporter des requêtes Analytics</span><span class="sxs-lookup"><span data-stu-id="38c11-131">Export Analytics queries</span></span>
<span data-ttu-id="38c11-132">Cet itinéraire permet toowrite tout Analytique de requête vous le souhaitez et puis exporter ce tableau de bord Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="38c11-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="38c11-133">(Vous pouvez ajouter toohello le tableau de bord créé par l’adaptateur de hello.)</span><span class="sxs-lookup"><span data-stu-id="38c11-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="38c11-134">Une fois : installez Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="38c11-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="38c11-135">tooimport votre requête d’Application Insights, vous utilisez la version de bureau hello de Power BI.</span><span class="sxs-lookup"><span data-stu-id="38c11-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="38c11-136">Mais, puis vous pouvez le publier toohello web ou tooyour espace de travail de cloud Power BI.</span><span class="sxs-lookup"><span data-stu-id="38c11-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="38c11-137">Installez [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="38c11-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="38c11-138">Exporter une requête Analytics</span><span class="sxs-lookup"><span data-stu-id="38c11-138">Export an Analytics query</span></span>
1. <span data-ttu-id="38c11-139">[Ouvrez Analytics et écrivez votre requête](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="38c11-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="38c11-140">Tester et affiner la requête de hello jusqu'à ce que vous êtes satisfait des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="38c11-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="38c11-141">**Assurez-vous que cette requête hello s’exécute correctement dans Analytique avant d’exporter.**</span><span class="sxs-lookup"><span data-stu-id="38c11-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="38c11-142">Sur hello **exporter** menu, choisissez **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="38c11-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="38c11-143">Enregistrez le fichier de texte hello.</span><span class="sxs-lookup"><span data-stu-id="38c11-143">Save hello text file.</span></span>
   
    ![Exporter une requête Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="38c11-145">Dans Power BI Desktop, sélectionnez **obtenir des données, la requête vide** et puis Bonjour éditeur de requête, sous **vue** sélectionnez **éditeur de requêtes avancé**.</span><span class="sxs-lookup"><span data-stu-id="38c11-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="38c11-146">Script de langage M coller hello exportée dans hello éditeur de requêtes avancé.</span><span class="sxs-lookup"><span data-stu-id="38c11-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Éditeur de requêtes avancé](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="38c11-148">Vous pouvez avoir tooprovide informations d’identification tooallow Power BI tooaccess Azure.</span><span class="sxs-lookup"><span data-stu-id="38c11-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="38c11-149">Utilisez toosign de compte de société avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38c11-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Fournir des informations d’identification Azure tooenable Power BI toorun votre requête d’Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="38c11-151">(Si vous avez besoin des informations d’identification de tooverify hello, utilisez commande de menu des paramètres de Source de données hello Bonjour éditeur de requête.</span><span class="sxs-lookup"><span data-stu-id="38c11-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="38c11-152">Attention toospecify hello informations d’identification que vous utilisez pour Azure, ce qui peut être différent de vos informations d’identification pour Power BI.)</span><span class="sxs-lookup"><span data-stu-id="38c11-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="38c11-153">Choisissez une visualisation pour votre requête et sélectionnez des champs de hello pour l’axe x, y et segmentation de dimension.</span><span class="sxs-lookup"><span data-stu-id="38c11-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Sélectionner une visualisation](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="38c11-155">Publier votre espace de travail rapports tooyour Power BI cloud.</span><span class="sxs-lookup"><span data-stu-id="38c11-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="38c11-156">À partir de là, vous pouvez incorporer une version synchronisée dans d’autres pages web.</span><span class="sxs-lookup"><span data-stu-id="38c11-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Sélectionner une visualisation](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="38c11-158">Actualiser les rapports hello manuellement à des intervalles, ou configurer une actualisation planifiée sur la page d’options hello.</span><span class="sxs-lookup"><span data-stu-id="38c11-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="38c11-159">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="38c11-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="38c11-160">401 ou 403 non autorisé</span><span class="sxs-lookup"><span data-stu-id="38c11-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="38c11-161">Cela peut se produire si votre jeton d’actualisation n’a pas été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="38c11-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="38c11-162">Essayez ces tooensure étapes que vous avez toujours accès.</span><span class="sxs-lookup"><span data-stu-id="38c11-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="38c11-163">Si vous avez accès et les informations d’identification de hello refershing ne fonctionne pas, ouvrez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="38c11-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="38c11-164">Connectez-vous à hello portail Azure et assurez-vous que vous pouvez accéder à des ressources de hello</span><span class="sxs-lookup"><span data-stu-id="38c11-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="38c11-165">Essayez les informations d’identification de toorefresh hello pour hello du tableau de bord</span><span class="sxs-lookup"><span data-stu-id="38c11-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="38c11-166">502 Passerelle incorrecte</span><span class="sxs-lookup"><span data-stu-id="38c11-166">502 Bad Gateway</span></span>
<span data-ttu-id="38c11-167">Cela est généralement dû à une requête Analytics qui renvoie trop de données.</span><span class="sxs-lookup"><span data-stu-id="38c11-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="38c11-168">Il est conseillé à l’aide d’une plus petite plage de temps ou à l’aide de hello [il y a](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) fonctions uniquement [projet](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello des champs dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="38c11-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="38c11-169">Si la réduction hello le jeu de données provenant d’une requête Analytique de hello ne répond pas à vos besoins vous devez envisager d’utiliser hello [API](https://dev.applicationinsights.io/documentation/overview) toopull un plus grand jeu de données.</span><span class="sxs-lookup"><span data-stu-id="38c11-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="38c11-170">Vous trouverez ici les instructions comment tooconvert hello M-requête exporter toouse hello API.</span><span class="sxs-lookup"><span data-stu-id="38c11-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="38c11-171">Créez une [clé d’API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).</span><span class="sxs-lookup"><span data-stu-id="38c11-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="38c11-172">Hello de mise à jour Power BI M script que vous avez exporté à partir de l’Analytique en remplaçant hello ARM des URL avec les API AI (voir l’exemple ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="38c11-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="38c11-173">Remplacez **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="38c11-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="38c11-174">par **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="38c11-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="38c11-175">Enfin, mettre à jour les informations d’identification toobasic et utiliser votre clé API</span><span class="sxs-lookup"><span data-stu-id="38c11-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="38c11-176">**Script existant**</span><span class="sxs-lookup"><span data-stu-id="38c11-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="38c11-177">**Script mis à jour**</span><span class="sxs-lookup"><span data-stu-id="38c11-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="38c11-178">À propos de l’échantillonnage</span><span class="sxs-lookup"><span data-stu-id="38c11-178">About sampling</span></span>
<span data-ttu-id="38c11-179">Si votre application envoie une grande quantité de données, fonctionnalité d’adaptative d’échantillonnage de hello peut fonctionner et envoyer seulement un pourcentage de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="38c11-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="38c11-180">Hello que même a la valeur true si vous avez manuellement défini d’échantillonnage Bonjour SDK ou ingestion.</span><span class="sxs-lookup"><span data-stu-id="38c11-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="38c11-181">En savoir plus sur l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="38c11-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="38c11-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38c11-182">Next steps</span></span>
* [<span data-ttu-id="38c11-183">Power BI - En savoir plus</span><span class="sxs-lookup"><span data-stu-id="38c11-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="38c11-184">Didacticiel Analytics</span><span class="sxs-lookup"><span data-stu-id="38c11-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

