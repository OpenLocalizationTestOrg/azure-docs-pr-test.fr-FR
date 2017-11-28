---
title: aaaTroubleshoot Analytique dans Azure Application Insights | Documents Microsoft
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
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="0d5e6-104">Dépannage d’Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d5e6-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="0d5e6-105">Des problèmes avec [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="0d5e6-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="0d5e6-106">Démarrer ici.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-106">Start here.</span></span> <span data-ttu-id="0d5e6-107">Analytique est un outil puissant hello d’aperçus d’Application Azure.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="0d5e6-108">limites</span><span class="sxs-lookup"><span data-stu-id="0d5e6-108">Limits</span></span>
* <span data-ttu-id="0d5e6-109">À l’heure actuelle, ses résultats sont limité toojust plus d’une semaine de données passées.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="0d5e6-110">Navigateurs que nous testons : dernières versions d’Internet Explorer, Chrome et Edge.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="0d5e6-111">Extensions du navigateur incompatibles connues</span><span class="sxs-lookup"><span data-stu-id="0d5e6-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="0d5e6-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="0d5e6-112">Ghostery</span></span>

<span data-ttu-id="0d5e6-113">Désactivation de l’extension de hello ou utilisez un navigateur différent.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="0d5e6-114"><a name="e-a"></a> « Erreur inattendue »</span><span class="sxs-lookup"><span data-stu-id="0d5e6-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Ecran Erreur inattendue](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="0d5e6-116">Une erreur interne s’est produite lors de l’exécution du portail : exception non gérée.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="0d5e6-117">Nettoyer la mémoire cache du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="0d5e6-118"><a name="e-b"></a>403... Veuillez essayer tooreload</span><span class="sxs-lookup"><span data-stu-id="0d5e6-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... Veuillez essayer tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="0d5e6-120">Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="0d5e6-121">portail de Hello ne peut avoir aucun moyen de récupérer trop sans modifier les paramètres du navigateur.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="0d5e6-122">Vérifiez [les cookies tiers sont activés](#cookies) dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="0d5e6-123"><a name="authentication"></a>403... vérifiez la zone de sécurité</span><span class="sxs-lookup"><span data-stu-id="0d5e6-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... vérifiez la zone de sécurité](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="0d5e6-125">Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="0d5e6-126">portail de Hello ne peut avoir aucun moyen de récupérer trop sans modifier les paramètres du navigateur.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="0d5e6-127">Vérifiez [les cookies tiers sont activés](#cookies) dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="0d5e6-128">Vous avez peut-être utilisé un favori, un signet ou un lien enregistré tooopen hello Analytique portail ?</span><span class="sxs-lookup"><span data-stu-id="0d5e6-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="0d5e6-129">Si vous êtes connecté avec différentes informations d’identification que vous avez utilisé lorsque vous avez enregistré le lien de hello ?</span><span class="sxs-lookup"><span data-stu-id="0d5e6-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="0d5e6-130">Essayez d’utiliser une fenêtre de navigateur privée/anonyme (après avoir fermé toutes les fenêtres de ce type).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="0d5e6-131">Vous avez tooprovide vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="0d5e6-132">Ouvrir une autre fenêtre de navigateur (ordinaire) et accédez trop[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="0d5e6-133">Déconnectez-vous. Ouvrez votre lien, puis connectez-vous avec les informations d’identification correctes hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="0d5e6-134">Les utilisateurs Edge et Internet Explorer peuvent également obtenir cette erreur lorsque les paramètres de la zone de confiance ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="0d5e6-135">Vérifiez que les deux [portal d’Analytique](https://analytics.applicationinsights.io) et [portail Azure Active Directory](https://portal.azure.com) sont Bonjour même zone de sécurité :</span><span class="sxs-lookup"><span data-stu-id="0d5e6-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="0d5e6-136">Dans Internet Explorer, ouvrez **Options Internet**, **Sécurité**, **Sites de confiance**, **Sites** :</span><span class="sxs-lookup"><span data-stu-id="0d5e6-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Boîte de dialogue Options Internet, ajout d’un site tooTrusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="0d5e6-138">Dans la liste de sites Web hello, si un des hello URL suivantes sont inclus, assurez-vous que hello d’autres sont également inclus :</span><span class="sxs-lookup"><span data-stu-id="0d5e6-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="0d5e6-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="0d5e6-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="0d5e6-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="0d5e6-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="0d5e6-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="0d5e6-141">https://login.windows.net</span></span>

## <span data-ttu-id="0d5e6-142"><a name="e-d"></a>404 ... Ressource introuvable</span><span class="sxs-lookup"><span data-stu-id="0d5e6-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... ressource introuvable](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="0d5e6-144">Une ressource d’application a été supprimée d’Application Insights et n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="0d5e6-145">Cela peut se produire si vous avez enregistré la page de hello URL toohello Analytique.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="0d5e6-146"><a name="e-e"></a>403 ... Aucune autorisation</span><span class="sxs-lookup"><span data-stu-id="0d5e6-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... non autorisé](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="0d5e6-148">Vous n’avez tooopen d’autorisation de cette application dans Analytique.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="0d5e6-149">Vous avez reçu hello lien à partir d’une autre personne ?</span><span class="sxs-lookup"><span data-stu-id="0d5e6-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="0d5e6-150">Demandez-lui toomake que vous êtes dans hello [lecteurs ou les collaborateurs pour ce groupe de ressources](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="0d5e6-151">Avez-vous enregistré lien hello à l’aide des informations d’identification différentes ?</span><span class="sxs-lookup"><span data-stu-id="0d5e6-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="0d5e6-152">Ouvrez hello [portail Azure](https://portal.azure.com), déconnectez-vous, puis essayez à nouveau, ce lien fournissant les informations d’identification correctes hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="0d5e6-153"><a name="html-storage"></a>403 ... Stockage HTML5</span><span class="sxs-lookup"><span data-stu-id="0d5e6-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="0d5e6-154">Notre portail utilise HTML5 localStorage et sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="0d5e6-155">Chrome : Paramètres, Confidentialité, Paramètres de content.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="0d5e6-156">Internet Explorer : Options Internet, onglet Avancé, Sécurité, Activer le stockage DOM</span><span class="sxs-lookup"><span data-stu-id="0d5e6-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Essayez tooenable HTML5 stockage](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="0d5e6-158"><a name="e-g"></a>404 ... Abonnement introuvable</span><span class="sxs-lookup"><span data-stu-id="0d5e6-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Abonnement introuvable](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="0d5e6-160">URL de Hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="0d5e6-161">Ouvrez la ressource d’application hello dans [portail Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="0d5e6-162">Utilisez ensuite le bouton d’Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="0d5e6-163"><a name="e-h"></a>404... page inexistante</span><span class="sxs-lookup"><span data-stu-id="0d5e6-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Page inexistante](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="0d5e6-165">URL de Hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-165">hello URL is invalid.</span></span>

* <span data-ttu-id="0d5e6-166">Ouvrez la ressource d’application hello dans [portail Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d5e6-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="0d5e6-167">Utilisez ensuite le bouton d’Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="0d5e6-168"><a name="cookies"></a>Activer les cookies tiers</span><span class="sxs-lookup"><span data-stu-id="0d5e6-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="0d5e6-169">Consultez [toodisable tiers comment les cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), mais nous devons trop**activer** les.</span><span class="sxs-lookup"><span data-stu-id="0d5e6-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

