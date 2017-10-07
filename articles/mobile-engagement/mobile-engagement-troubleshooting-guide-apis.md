---
title: aaaAzure Mobile Engagement Troubleshooting Guide - API
description: "Guides de dépannage pour Azure Mobile Engagement : les API"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="6ebe4-103">Guide de résolution des problèmes pour les problèmes d'API</span><span class="sxs-lookup"><span data-stu-id="6ebe4-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="6ebe4-104">Hello Voici les problèmes possibles, que vous pouvez rencontrer avec les administrateurs interagissent Azure Mobile Engagement via hello API.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-104">hello following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via hello APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="6ebe4-105">Problèmes de syntaxe</span><span class="sxs-lookup"><span data-stu-id="6ebe4-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="6ebe4-106">Problème</span><span class="sxs-lookup"><span data-stu-id="6ebe4-106">Issue</span></span>
* <span data-ttu-id="6ebe4-107">Erreurs de syntaxe à l’aide des API de hello (ou un comportement inattendu).</span><span class="sxs-lookup"><span data-stu-id="6ebe4-107">Syntax Errors using hello API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="6ebe4-108">Causes</span><span class="sxs-lookup"><span data-stu-id="6ebe4-108">Causes</span></span>
* <span data-ttu-id="6ebe4-109">Problèmes de syntaxe :</span><span class="sxs-lookup"><span data-stu-id="6ebe4-109">Syntax issues:</span></span>
  * <span data-ttu-id="6ebe4-110">Vérifiez que hello toocheck syntaxe de hello les API spécifiques que vous utilisez tooconfirm qui hello option est disponible.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-110">Make sure toocheck hello Syntax of hello specific API you are using tooconfirm that hello option is available.</span></span>
  * <span data-ttu-id="6ebe4-111">Un problème courant avec l’utilisation de l’API est tooconfuse hello portée API et hello API Push (la plupart des tâches doit être effectuée avec hello API couverture au lieu de l’API de Push de hello).</span><span class="sxs-lookup"><span data-stu-id="6ebe4-111">A common issue with API usage is tooconfuse hello Reach API and hello Push API (most tasks should be performed with hello Reach API instead of hello Push API).</span></span> 
  * <span data-ttu-id="6ebe4-112">Un autre problème courant avec l’intégration du Kit de développement logiciel et l’utilisation de l’API est tooconfuse hello clé du SDK et hello clé API.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-112">Another common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>
  * <span data-ttu-id="6ebe4-113">Les scripts qui se connectent toohello API doivent toosend données au moins toutes les 10 minutes ou une connexion de hello expire (notamment le cas dans les scripts d’analyse API à l’écoute pour les données).</span><span class="sxs-lookup"><span data-stu-id="6ebe4-113">Scripts that connect toohello APIs need toosend data at least every 10 minutes or hello connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="6ebe4-114">tooprevent des délais d’attente, avoir votre envoi script un ping XMPP chaque session de hello 10 minutes tookeep active avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-114">tooprevent timeouts, have your script send an XMPP ping every 10 minutes tookeep hello session alive with hello server.</span></span>

### <a name="see-also"></a><span data-ttu-id="6ebe4-115">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6ebe4-115">See also</span></span>
* <span data-ttu-id="6ebe4-116">[Documentation de l’API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="6ebe4-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="6ebe4-117">Informations sur le protocole XMPP</span><span class="sxs-lookup"><span data-stu-id="6ebe4-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a><span data-ttu-id="6ebe4-118">Impossible de toouse hello API tooperform hello même action disponible Bonjour Azure Mobile Engagement UI</span><span class="sxs-lookup"><span data-stu-id="6ebe4-118">Unable toouse hello API tooperform hello same action available in hello Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="6ebe4-119">Problème</span><span class="sxs-lookup"><span data-stu-id="6ebe4-119">Issue</span></span>
* <span data-ttu-id="6ebe4-120">Une action qui travaille à partir de hello Qu'azure Mobile Engagement UI ne fonctionne pas à partir de hello liés à Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-120">An action that works from hello Azure Mobile Engagement UI doesn't work from hello related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="6ebe4-121">Causes</span><span class="sxs-lookup"><span data-stu-id="6ebe4-121">Causes</span></span>
* <span data-ttu-id="6ebe4-122">Confirmer que vous puissiez effectuer la même action de hello Azure Mobile Engagement interface montre que vous avez correctement intégré cette fonctionnalité d’Azure Mobile Engagement avec hello hello SDK.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-122">Confirming that you can perform hello same action from hello Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with hello SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="6ebe4-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6ebe4-123">See also</span></span>
* <span data-ttu-id="6ebe4-124">[Documentation sur l’interface utilisateur][Link 1]</span><span class="sxs-lookup"><span data-stu-id="6ebe4-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="6ebe4-125">Messages d'erreur</span><span class="sxs-lookup"><span data-stu-id="6ebe4-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="6ebe4-126">Problème</span><span class="sxs-lookup"><span data-stu-id="6ebe4-126">Issue</span></span>
* <span data-ttu-id="6ebe4-127">Codes d’erreur à l’aide des API hello affichée lors de l’exécution ou dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-127">Error codes using hello API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="6ebe4-128">Causes</span><span class="sxs-lookup"><span data-stu-id="6ebe4-128">Causes</span></span>
* <span data-ttu-id="6ebe4-129">Voici une liste composite de numéros de codes d'état d'API courants pour référence et dépannage préliminaire :</span><span class="sxs-lookup"><span data-stu-id="6ebe4-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a><span data-ttu-id="6ebe4-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6ebe4-130">See also</span></span>
* <span data-ttu-id="6ebe4-131">[Documentation sur les API : pour connaître le détail des erreurs de chaque API spécifique][Link 4]</span><span class="sxs-lookup"><span data-stu-id="6ebe4-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="6ebe4-132">Échecs silencieux</span><span class="sxs-lookup"><span data-stu-id="6ebe4-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="6ebe4-133">Problème</span><span class="sxs-lookup"><span data-stu-id="6ebe4-133">Issue</span></span>
* <span data-ttu-id="6ebe4-134">L'action de l'API échoue et aucun message d'erreur ne s'affiche lors de l'exécution ou dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="6ebe4-135">Causes</span><span class="sxs-lookup"><span data-stu-id="6ebe4-135">Causes</span></span>
* <span data-ttu-id="6ebe4-136">Nombre d’éléments sera désactivé dans l’interface utilisateur de Azure Mobile Engagement s’ils ne sont pas intégrés correctement, mais échoueront silencieusement hello API, par conséquent, n’oubliez pas de hello tootest hello même fonctionnalité à partir de hello UI toosee si elle fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-136">Many items will be disabled in hello Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from hello API, so remember tootest hello same functionality from hello UI toosee if it works.</span></span>
* <span data-ttu-id="6ebe4-137">Azure Mobile Engagement et nombreuses fonctionnalités avancées d’Azure Mobile Engagement vous essayez de toouse, toobe besoin individuellement intégré dans votre application avec le Kit de développement logiciel de hello séparément avant de pouvoir les utiliser.</span><span class="sxs-lookup"><span data-stu-id="6ebe4-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting toouse, need toobe individually integrated into your app with hello SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="6ebe4-138">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6ebe4-138">See also</span></span>
* <span data-ttu-id="6ebe4-139">[Guide de résolution des problèmes - Kit de développement logiciel (SDK)][Link 25]</span><span class="sxs-lookup"><span data-stu-id="6ebe4-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

