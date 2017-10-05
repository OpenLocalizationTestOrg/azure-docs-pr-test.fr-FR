---
title: "Dépannage d’Analytics dans Azure Application Insights | Microsoft Docs"
description: "Des problèmes avec Application Insights Analytics ? Démarrer ici. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="7583c-104">Dépannage d’Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="7583c-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="7583c-105">Des problèmes avec [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="7583c-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="7583c-106">Démarrer ici.</span><span class="sxs-lookup"><span data-stu-id="7583c-106">Start here.</span></span> <span data-ttu-id="7583c-107">Analytics est le puissant outil de recherche d’Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7583c-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="7583c-108">Limites</span><span class="sxs-lookup"><span data-stu-id="7583c-108">Limits</span></span>
* <span data-ttu-id="7583c-109">Les résultats de requête sont actuellement limités à une seule semaine de données d’historique.</span><span class="sxs-lookup"><span data-stu-id="7583c-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="7583c-110">Navigateurs que nous testons : dernières versions d’Internet Explorer, Chrome et Edge.</span><span class="sxs-lookup"><span data-stu-id="7583c-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="7583c-111">Extensions du navigateur incompatibles connues</span><span class="sxs-lookup"><span data-stu-id="7583c-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="7583c-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="7583c-112">Ghostery</span></span>

<span data-ttu-id="7583c-113">Désactivez l’extension ou utilisez un autre navigateur.</span><span class="sxs-lookup"><span data-stu-id="7583c-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="7583c-114"><a name="e-a"></a> « Erreur inattendue »</span><span class="sxs-lookup"><span data-stu-id="7583c-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Ecran Erreur inattendue](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="7583c-116">Une erreur interne s’est produite lors de l’exécution du portail : exception non gérée.</span><span class="sxs-lookup"><span data-stu-id="7583c-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="7583c-117">Nettoyez le cache du navigateur.</span><span class="sxs-lookup"><span data-stu-id="7583c-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="7583c-118"><a name="e-b"></a>403... essayez de recharger</span><span class="sxs-lookup"><span data-stu-id="7583c-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403... essayez de recharger](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="7583c-120">Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès).</span><span class="sxs-lookup"><span data-stu-id="7583c-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="7583c-121">Le portail n’a peut-être aucun moyen de récupérer les données sans modifier les paramètres du navigateur.</span><span class="sxs-lookup"><span data-stu-id="7583c-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="7583c-122">Vérifiez que [les cookies tiers sont activés](#cookies) dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="7583c-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="7583c-123"><a name="authentication"></a>403... vérifiez la zone de sécurité</span><span class="sxs-lookup"><span data-stu-id="7583c-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... vérifiez la zone de sécurité](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="7583c-125">Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès).</span><span class="sxs-lookup"><span data-stu-id="7583c-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="7583c-126">Le portail n’a peut-être aucun moyen de récupérer les données sans modifier les paramètres du navigateur.</span><span class="sxs-lookup"><span data-stu-id="7583c-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="7583c-127">Vérifiez que [les cookies tiers sont activés](#cookies) dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="7583c-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="7583c-128">Avez-vous utilisé un favori, un signet ou un lien enregistré pour ouvrir le portail Analytics ?</span><span class="sxs-lookup"><span data-stu-id="7583c-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="7583c-129">Vous êtes-vous connecté avec des informations d’identification différentes de celles utilisées pour enregistrer le lien ?</span><span class="sxs-lookup"><span data-stu-id="7583c-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="7583c-130">Essayez d’utiliser une fenêtre de navigateur privée/anonyme (après avoir fermé toutes les fenêtres de ce type).</span><span class="sxs-lookup"><span data-stu-id="7583c-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="7583c-131">Vous devrez fournir vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7583c-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="7583c-132">Ouvrez une autre fenêtre de navigateur (standard) et accédez à [Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7583c-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="7583c-133">Déconnectez-vous. Ouvrez ensuite votre lien et connectez-vous avec les informations d’identification correctes.</span><span class="sxs-lookup"><span data-stu-id="7583c-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="7583c-134">Les utilisateurs Edge et Internet Explorer peuvent également obtenir cette erreur lorsque les paramètres de la zone de confiance ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7583c-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="7583c-135">Vérifiez que le [portail Analytics](https://analytics.applicationinsights.io) et le [portail Azure Active Directory](https://portal.azure.com) se trouvent dans la même zone de sécurité :</span><span class="sxs-lookup"><span data-stu-id="7583c-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="7583c-136">Dans Internet Explorer, ouvrez **Options Internet**, **Sécurité**, **Sites de confiance**, **Sites** :</span><span class="sxs-lookup"><span data-stu-id="7583c-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Boîte de dialogue Options Internet, ajout d’un site aux sites de confiance](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="7583c-138">Dans la liste des sites Web, si une des URL suivantes est incluse, assurez-vous que les autres le sont également :</span><span class="sxs-lookup"><span data-stu-id="7583c-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="7583c-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="7583c-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="7583c-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7583c-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="7583c-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="7583c-141">https://login.windows.net</span></span>

## <span data-ttu-id="7583c-142"><a name="e-d"></a>404 ... Ressource introuvable</span><span class="sxs-lookup"><span data-stu-id="7583c-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... ressource introuvable](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="7583c-144">Une ressource d’application a été supprimée d’Application Insights et n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="7583c-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="7583c-145">Cela peut se produire si vous avez enregistré l’URL dans la page Analytics.</span><span class="sxs-lookup"><span data-stu-id="7583c-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="7583c-146"><a name="e-e"></a>403 ... Aucune autorisation</span><span class="sxs-lookup"><span data-stu-id="7583c-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... non autorisé](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="7583c-148">Vous n’êtes pas autorisé à ouvrir cette application dans Analytics.</span><span class="sxs-lookup"><span data-stu-id="7583c-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="7583c-149">Avez-vous reçu le lien d’un tiers ?</span><span class="sxs-lookup"><span data-stu-id="7583c-149">Did you get the link from someone else?</span></span> <span data-ttu-id="7583c-150">Si oui, demandez à cette personne de vérifier que vous figurez bien dans les [lecteurs ou contributeurs de ce groupe de ressources](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7583c-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="7583c-151">Avez-vous enregistré le lien en utilisant d’autres informations d’identification ?</span><span class="sxs-lookup"><span data-stu-id="7583c-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="7583c-152">Ouvrez le [portail Azure](https://portal.azure.com), déconnectez-vous, puis essayez à nouveau d’ouvrir ce lien en fournissant les informations d’identification correctes.</span><span class="sxs-lookup"><span data-stu-id="7583c-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="7583c-153"><a name="html-storage"></a>403 ... Stockage HTML5</span><span class="sxs-lookup"><span data-stu-id="7583c-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="7583c-154">Notre portail utilise HTML5 localStorage et sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="7583c-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="7583c-155">Chrome : Paramètres, Confidentialité, Paramètres de content.</span><span class="sxs-lookup"><span data-stu-id="7583c-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="7583c-156">Internet Explorer : Options Internet, onglet Avancé, Sécurité, Activer le stockage DOM</span><span class="sxs-lookup"><span data-stu-id="7583c-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... essayez d’activer le stockage HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="7583c-158"><a name="e-g"></a>404 ... Abonnement introuvable</span><span class="sxs-lookup"><span data-stu-id="7583c-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Abonnement introuvable](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="7583c-160">L’URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="7583c-160">The URL is invalid.</span></span> 

* <span data-ttu-id="7583c-161">Ouvrez la ressource d’application dans le [portail Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7583c-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="7583c-162">Utilisez ensuite le bouton Analytics.</span><span class="sxs-lookup"><span data-stu-id="7583c-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="7583c-163"><a name="e-h"></a>404... page inexistante</span><span class="sxs-lookup"><span data-stu-id="7583c-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Page inexistante](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="7583c-165">L’URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="7583c-165">The URL is invalid.</span></span>

* <span data-ttu-id="7583c-166">Ouvrez la ressource d’application dans le [portail Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7583c-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="7583c-167">Utilisez ensuite le bouton Analytics.</span><span class="sxs-lookup"><span data-stu-id="7583c-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="7583c-168"><a name="cookies"></a>Activer les cookies tiers</span><span class="sxs-lookup"><span data-stu-id="7583c-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="7583c-169">Consultez la page [Comment désactiver les cookies tiers](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), mais notez que nous devons les **activer** .</span><span class="sxs-lookup"><span data-stu-id="7583c-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

