---
title: Microsoft Dynamics CRM et Azure Application Insights | Microsoft Docs
description: "Obtenez des données de télémétrie à partir de Microsoft Dynamics CRM Online à l’aide d’Application Insights. Procédure pas à pas de configuration, obtention de données, visualisation et exportation."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="19b48-104">Procédure pas à pas : activation de télémétrie pour Microsoft Dynamics CRM Online à l’aide d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="19b48-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="19b48-105">Cet article décrit comment obtenir des données de télémétrie à partir de [Microsoft Dynamics CRM Online](https://www.dynamics.com/) à l’aide [d’Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="19b48-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="19b48-106">Nous explorerons le processus complet d’ajout de script Application Insights à votre application, de capture de données et de visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="19b48-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="19b48-107">[Parcourez l’exemple de solution](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="19b48-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="19b48-108">Ajouter Application Insights à une instance de CRM Online nouvelle ou existante</span><span class="sxs-lookup"><span data-stu-id="19b48-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="19b48-109">Pour analyser votre application, vous devez y ajouter un Kit de développement logiciel (SDK) Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19b48-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="19b48-110">Le kit de développement logiciel (SDK) envoie les données de télémétrie au [portail Application Insights](https://portal.azure.com), où vous pouvez utiliser nos puissants outils de diagnostic et d’analyse ou exporter les données vers un emplacement de stockage.</span><span class="sxs-lookup"><span data-stu-id="19b48-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="19b48-111">Créer une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="19b48-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="19b48-112">Obtenez un [compte dans Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="19b48-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="19b48-113">Connectez-vous au [portail Azure](https://portal.azure.com) et ajoutez une nouvelle ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19b48-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="19b48-114">C’est là où vos données seront traitées et affichées.</span><span class="sxs-lookup"><span data-stu-id="19b48-114">This is where your data will be processed and displayed.</span></span>
   
    ![Cliquez sur +, Services de développement, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="19b48-116">Choisissez le type d'application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="19b48-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="19b48-117">Ouvrez la page Mise en route et ouvrez « Analyse et diagnostic côté client ».</span><span class="sxs-lookup"><span data-stu-id="19b48-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Extrait de code pour l’insertion dans votre page web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="19b48-119">**Laissez la page de code ouverte** pendant que vous effectuez l’étape suivante dans une autre fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="19b48-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="19b48-120">Vous aurez bientôt besoin du code.</span><span class="sxs-lookup"><span data-stu-id="19b48-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="19b48-121">Créer une ressource web JavaScript dans Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="19b48-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="19b48-122">Ouvrez votre instance de CRM Online et connectez-vous avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="19b48-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="19b48-123">Ouvrez les paramètres Microsoft Dynamics CRM, Personnalisations, Personnaliser le système</span><span class="sxs-lookup"><span data-stu-id="19b48-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Paramètres Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Paramètres > Personnalisations](./media/app-insights-sample-mscrm/05.png)

    ![Personnalisez l’option de système](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="19b48-127">Créez une ressource JavaScript.</span><span class="sxs-lookup"><span data-stu-id="19b48-127">Create a JavaScript resource.</span></span>
   
    ![Nouvelle boîte de dialogue ressource web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="19b48-129">Donnez-lui un nom, sélectionnez **Script (JScript)** et ouvrez l’éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="19b48-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Ouvrez l’éditeur de texte](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="19b48-131">Copiez le code à partir d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19b48-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="19b48-132">Lors de la copie, veillez à ignorer les balises de script.</span><span class="sxs-lookup"><span data-stu-id="19b48-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="19b48-133">Reportez-vous à la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="19b48-133">Refer below screenshot:</span></span>
   
    ![Définissez votre clé d’instrumentation](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="19b48-135">Le code contient la clé d’instrumentation qui identifie votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19b48-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="19b48-136">Enregistrez et publiez.</span><span class="sxs-lookup"><span data-stu-id="19b48-136">Save and publish.</span></span>
   
    ![Enregistrez et publiez](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="19b48-138">Instrumenter les formulaires</span><span class="sxs-lookup"><span data-stu-id="19b48-138">Instrument Forms</span></span>
1. <span data-ttu-id="19b48-139">Dans Microsoft CRM Online, ouvrez le formulaire Compte.</span><span class="sxs-lookup"><span data-stu-id="19b48-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Formulaire de compte](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="19b48-141">Ouvrez les propriétés de formulaire.</span><span class="sxs-lookup"><span data-stu-id="19b48-141">Open the form Properties</span></span>
   
    ![Propriétés de formulaire](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="19b48-143">Ajoutez la ressource web JavaScript que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="19b48-143">Add the JavaScript web resource that you created</span></span>
   
    ![Ajoutez un menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Ajoutez la ressource web](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="19b48-146">Enregistrez et publiez vos personnalisations de formulaire.</span><span class="sxs-lookup"><span data-stu-id="19b48-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="19b48-147">Mesures capturées</span><span class="sxs-lookup"><span data-stu-id="19b48-147">Metrics captured</span></span>
<span data-ttu-id="19b48-148">Vous avez maintenant configuré la capture de télémétrie pour le formulaire.</span><span class="sxs-lookup"><span data-stu-id="19b48-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="19b48-149">Chaque fois qu’il sera utilisé, des données seront envoyées à votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19b48-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="19b48-150">Voici des exemples de données qui seront affichées.</span><span class="sxs-lookup"><span data-stu-id="19b48-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="19b48-151">Intégrité d’application</span><span class="sxs-lookup"><span data-stu-id="19b48-151">Application health</span></span>
![Exemple de temps de chargement de la page](./media/app-insights-sample-mscrm/15.png)

![Exemple de graphique des affichages de pages](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="19b48-154">Exceptions du navigateur :</span><span class="sxs-lookup"><span data-stu-id="19b48-154">Browser exceptions:</span></span>

![Graphique des exceptions du navigateur](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="19b48-156">Cliquez sur le graphique pour obtenir plus de détails :</span><span class="sxs-lookup"><span data-stu-id="19b48-156">Click the chart to get more detail:</span></span>

![Liste des exceptions](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="19b48-158">Usage</span><span class="sxs-lookup"><span data-stu-id="19b48-158">Usage</span></span>
![Utilisateurs, sessions et affichages de page](./media/app-insights-sample-mscrm/19.png)

![Graphiques de session](./media/app-insights-sample-mscrm/20.png)

![Versions de navigateur](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="19b48-162">Navigateurs</span><span class="sxs-lookup"><span data-stu-id="19b48-162">Browsers</span></span>
![Répartition du temps de chargement de la page](./media/app-insights-sample-mscrm/22.png)

![Nombre de sessions par version de navigateur](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="19b48-165">Géolocalisation</span><span class="sxs-lookup"><span data-stu-id="19b48-165">Geolocation</span></span>
![Nombre de sessions par pays](./media/app-insights-sample-mscrm/24.png)

![Sessions et utilisateurs par pays](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="19b48-168">Demande d’affichage de page</span><span class="sxs-lookup"><span data-stu-id="19b48-168">Inside page view request</span></span>
![Résumé d’affichage de la page](./media/app-insights-sample-mscrm/26.png)

![Recherche sur les événements d’affichage de page](./media/app-insights-sample-mscrm/27.png)

![Affichages de page similaires](./media/app-insights-sample-mscrm/28.png)

![Propriétés d'affichage de la page](./media/app-insights-sample-mscrm/29.png)

![Pages par session](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="19b48-174">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="19b48-174">Sample code</span></span>
<span data-ttu-id="19b48-175">[Parcourez l'exemple de code](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="19b48-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="19b48-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="19b48-176">Power BI</span></span>
<span data-ttu-id="19b48-177">Vous pouvez effectuer une analyse encore plus approfondie si vous [exportez les données vers Microsoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="19b48-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="19b48-178">Exemple de solution Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="19b48-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="19b48-179">[Voici l’exemple de solution implémenté dans Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="19b48-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="19b48-180">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="19b48-180">Learn more</span></span>
* [<span data-ttu-id="19b48-181">Présentation d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="19b48-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="19b48-182">Application Insights pour les pages web</span><span class="sxs-lookup"><span data-stu-id="19b48-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="19b48-183">Plus d'exemples et de procédures pas à pas</span><span class="sxs-lookup"><span data-stu-id="19b48-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
