---
title: aaaMicrosoft Dynamics CRM et Azure Application Insights | Documents Microsoft
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
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="c0626-104">Procédure pas à pas : activation de télémétrie pour Microsoft Dynamics CRM Online à l’aide d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0626-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="c0626-105">Cet article vous montre comment les données de télémétrie tooget de [Microsoft Dynamics CRM Online](https://www.dynamics.com/) à l’aide de [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c0626-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="c0626-106">Nous examinerons hello ensemble du processus de l’ajout d’Application Insights script tooyour application, la capture des données et visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="c0626-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="c0626-107">[Parcourir l’exemple de solution hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c0626-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="c0626-108">Ajouter Application Insights toonew ou l’instance existante de CRM Online</span><span class="sxs-lookup"><span data-stu-id="c0626-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="c0626-109">toomonitor votre application, vous ajoutez une application de tooyour Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="c0626-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="c0626-110">Hello SDK envoie télémétrie toohello [portail Application Insights](https://portal.azure.com), où vous pouvez utiliser nos puissantes analyses et les outils de diagnostic, ou exporter hello données toostorage.</span><span class="sxs-lookup"><span data-stu-id="c0626-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="c0626-111">Créer une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="c0626-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="c0626-112">Obtenez un [compte dans Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="c0626-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="c0626-113">L’authentification à hello [portail Azure](https://portal.azure.com) et ajouter une nouvelle ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0626-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="c0626-114">C’est là où vos données seront traitées et affichées.</span><span class="sxs-lookup"><span data-stu-id="c0626-114">This is where your data will be processed and displayed.</span></span>
   
    ![Cliquez sur +, Services de développement, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="c0626-116">Choisissez ASP.NET en tant que type de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c0626-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="c0626-117">Ouvrez la page de prise en main de hello « analyse et de diagnostiquer côté client ».</span><span class="sxs-lookup"><span data-stu-id="c0626-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Extrait de code pour l’insertion dans votre page web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="c0626-119">**Maintenir la page de codes hello** pendant que vous hello étape suivante dans une autre fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="c0626-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="c0626-120">Vous devez les code hello bientôt.</span><span class="sxs-lookup"><span data-stu-id="c0626-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="c0626-121">Créer une ressource web JavaScript dans Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="c0626-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="c0626-122">Ouvrez votre instance de CRM Online et connectez-vous avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c0626-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="c0626-123">Ouvrez Microsoft Dynamics CRM paramètres, des personnalisations, personnaliser hello système</span><span class="sxs-lookup"><span data-stu-id="c0626-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Paramètres Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Paramètres > Personnalisations](./media/app-insights-sample-mscrm/05.png)

    ![Personnaliser l’option de système de hello](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="c0626-127">Créez une ressource JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c0626-127">Create a JavaScript resource.</span></span>
   
    ![Nouvelle boîte de dialogue ressource web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="c0626-129">Donnez-lui un nom, sélectionnez **Script (JScript)** et éditeur de texte hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="c0626-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Éditeur de texte hello ouvert](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="c0626-131">Copiez le code de hello d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0626-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="c0626-132">Lors de la copie que les balises de script que tooignore.</span><span class="sxs-lookup"><span data-stu-id="c0626-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="c0626-133">Reportez-vous à la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c0626-133">Refer below screenshot:</span></span>
   
    ![Définissez votre clé d’instrumentation](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="c0626-135">code de Hello inclut la clé d’instrumentation hello qui identifie votre ressource Application insights.</span><span class="sxs-lookup"><span data-stu-id="c0626-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="c0626-136">Enregistrez et publiez.</span><span class="sxs-lookup"><span data-stu-id="c0626-136">Save and publish.</span></span>
   
    ![Enregistrez et publiez](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="c0626-138">Instrumenter les formulaires</span><span class="sxs-lookup"><span data-stu-id="c0626-138">Instrument Forms</span></span>
1. <span data-ttu-id="c0626-139">Dans Microsoft CRM Online, ouvrez le formulaire de compte hello</span><span class="sxs-lookup"><span data-stu-id="c0626-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Formulaire de compte](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="c0626-141">Ouvrez l’écran hello propriétés</span><span class="sxs-lookup"><span data-stu-id="c0626-141">Open hello form Properties</span></span>
   
    ![Propriétés de formulaire](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="c0626-143">Ajouter hello ressource web JavaScript que vous avez créé</span><span class="sxs-lookup"><span data-stu-id="c0626-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Ajoutez un menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Ajouter une ressource web de hello](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="c0626-146">Enregistrez et publiez vos personnalisations de formulaire.</span><span class="sxs-lookup"><span data-stu-id="c0626-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="c0626-147">Mesures capturées</span><span class="sxs-lookup"><span data-stu-id="c0626-147">Metrics captured</span></span>
<span data-ttu-id="c0626-148">Vous avez maintenant configuré la capture de données de télémétrie pour écran de hello.</span><span class="sxs-lookup"><span data-stu-id="c0626-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="c0626-149">Chaque fois qu’il est utilisé, les données sont envoyées ressource d’Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="c0626-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="c0626-150">Voici les exemples de données hello qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c0626-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="c0626-151">Intégrité d’application</span><span class="sxs-lookup"><span data-stu-id="c0626-151">Application health</span></span>
![Exemple de temps de chargement de la page](./media/app-insights-sample-mscrm/15.png)

![Exemple de graphique des affichages de pages](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="c0626-154">Exceptions du navigateur :</span><span class="sxs-lookup"><span data-stu-id="c0626-154">Browser exceptions:</span></span>

![Graphique des exceptions du navigateur](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="c0626-156">Cliquez sur hello graphique tooget plus en détail :</span><span class="sxs-lookup"><span data-stu-id="c0626-156">Click hello chart tooget more detail:</span></span>

![Liste des exceptions](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="c0626-158">Usage</span><span class="sxs-lookup"><span data-stu-id="c0626-158">Usage</span></span>
![Utilisateurs, sessions et affichages de page](./media/app-insights-sample-mscrm/19.png)

![Graphiques de session](./media/app-insights-sample-mscrm/20.png)

![Versions de navigateur](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="c0626-162">Navigateurs</span><span class="sxs-lookup"><span data-stu-id="c0626-162">Browsers</span></span>
![Répartition du temps de chargement de la page](./media/app-insights-sample-mscrm/22.png)

![Nombre de sessions par version de navigateur](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="c0626-165">Géolocalisation</span><span class="sxs-lookup"><span data-stu-id="c0626-165">Geolocation</span></span>
![Nombre de sessions par pays](./media/app-insights-sample-mscrm/24.png)

![Sessions et utilisateurs par pays](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="c0626-168">Demande d’affichage de page</span><span class="sxs-lookup"><span data-stu-id="c0626-168">Inside page view request</span></span>
![Résumé d’affichage de la page](./media/app-insights-sample-mscrm/26.png)

![Recherche sur les événements d’affichage de page](./media/app-insights-sample-mscrm/27.png)

![Affichages de page similaires](./media/app-insights-sample-mscrm/28.png)

![Propriétés d'affichage de la page](./media/app-insights-sample-mscrm/29.png)

![Pages par session](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="c0626-174">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="c0626-174">Sample code</span></span>
<span data-ttu-id="c0626-175">[Parcourir le code d’exemple hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c0626-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="c0626-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="c0626-176">Power BI</span></span>
<span data-ttu-id="c0626-177">Vous pouvez faire de même effectuer une analyse si vous [exporter les données de hello tooMicrosoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c0626-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="c0626-178">Exemple de solution Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="c0626-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="c0626-179">[Voici les solutions d’exemple hello implémentée dans Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c0626-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c0626-180">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="c0626-180">Learn more</span></span>
* [<span data-ttu-id="c0626-181">Présentation d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0626-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="c0626-182">Application Insights pour les pages web</span><span class="sxs-lookup"><span data-stu-id="c0626-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="c0626-183">Plus d'exemples et de procédures pas à pas</span><span class="sxs-lookup"><span data-stu-id="c0626-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
