---
title: "Interface utilisateur d’Azure Mobile Engagement - Critère Reach"
description: "Utilisation des critères de ciblage pour envoyer des campagnes push à un sous-ensemble donné de vos utilisateurs à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 803b44721d0ab1ac7b5a8074e18857fc57adb724
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-targeting-criteria-to-send-push-campaigns-to-a-select-subset-of-your-users"></a><span data-ttu-id="05a33-103">Utilisation des critères de ciblage pour envoyer des campagnes push à un sous-ensemble donné de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="05a33-103">How to use targeting criteria to send push campaigns to a select subset of your users</span></span>
<span data-ttu-id="05a33-104">Le ciblage de votre audience suivant des critères spécifiques à l'aide du bouton « Nouveau critère » est l'un des concepts les plus performants d'Azure Mobile Engagement qui vous permet d'envoyer des notifications Push pertinentes auxquelles les clients répondront, au lieu d'envoyer des courriers indésirables à tout le monde.</span><span class="sxs-lookup"><span data-stu-id="05a33-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span></span> <span data-ttu-id="05a33-105">Vous pouvez limiter votre audience selon des critères standard et simuler des notifications Push pour déterminer combien de personnes recevront ces notifications.</span><span class="sxs-lookup"><span data-stu-id="05a33-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span></span>

<span data-ttu-id="05a33-106">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="05a33-106">**See also:**</span></span>

* <span data-ttu-id="05a33-107">[Documentation de l’interface utilisateur - Reach - Nouvelle campagne Push][Link 27]</span><span class="sxs-lookup"><span data-stu-id="05a33-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="05a33-108">Les critères d’audience peuvent inclure :</span><span class="sxs-lookup"><span data-stu-id="05a33-108">Audience criteria can include:</span></span>
* <span data-ttu-id="05a33-109">** Technicals : ** vous pouvez cibler basé sur les mêmes informations techniques que vous pouvez voir dans les sections Analytique et d’analyse.</span><span class="sxs-lookup"><span data-stu-id="05a33-109">**Technicals: ** You can target based on the same technical information you can see in the Analytics and Monitor sections.</span></span> <span data-ttu-id="05a33-110">**Voir aussi :** [Documentation de l’interface utilisateur - Analyse][Link 15], [Documentation de l’interface utilisateur - Moniteur][Link 16]</span><span class="sxs-lookup"><span data-stu-id="05a33-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="05a33-111">**Emplacement :** les applications qui utilisent un « rapport de localisation en temps réel » avec géorepérage peuvent utiliser l’emplacement géographique en tant que critère pour cibler une audience à partir de l’emplacement GPS.</span><span class="sxs-lookup"><span data-stu-id="05a33-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span></span> <span data-ttu-id="05a33-112">Un « rapport de localisation de zone différé » peut également être utilisé pour cibler une audience à partir de la localisation du téléphone cellulaire (Le « rapport de localisation en temps réel » et le « rapport de localisation de zone différé » doivent être activés à partir du Kit de développement logiciel (SDK)).</span><span class="sxs-lookup"><span data-stu-id="05a33-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span></span> <span data-ttu-id="05a33-113">**Consultez également :** [Documentation du Kit de développement logiciel (SDK) - iOS - Intégration][Link 5], [Documentation relative au Kit de développement logiciel (SDK) - Android - Intégration][Link 5]</span><span class="sxs-lookup"><span data-stu-id="05a33-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="05a33-114">**Commentaire Reach :** vous pouvez cibler votre audience selon les commentaires des précédentes notifications Reach via les commentaires Reach dans les sections Annonces, Sondages et Push de données.</span><span class="sxs-lookup"><span data-stu-id="05a33-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="05a33-115">Cela vous permet de mieux cibler votre audience après deux ou trois campagnes Reach, en comparaison à la première.</span><span class="sxs-lookup"><span data-stu-id="05a33-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span></span> <span data-ttu-id="05a33-116">Cela peut aussi être utilisé pour filtrer les utilisateurs qui ont déjà reçu une notification avec un contenu similaire, en définissant une campagne à NE PAS envoyer aux utilisateurs ayant déjà reçu une campagne spécifique précédente.</span><span class="sxs-lookup"><span data-stu-id="05a33-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span></span> <span data-ttu-id="05a33-117">Vous pouvez même exclure les utilisateurs faisant partie d’une campagne spécifique toujours active, afin qu’ils ne reçoivent pas de nouvelles notifications Push.</span><span class="sxs-lookup"><span data-stu-id="05a33-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="05a33-118">**Consultez également :** [Documentation sur l’interface utilisateur - Reach - Contenu Push][Link 29]</span><span class="sxs-lookup"><span data-stu-id="05a33-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="05a33-119">**Installation du suivi :** vous pouvez suivre des informations selon l’emplacement où les utilisateurs ont installé votre application.</span><span class="sxs-lookup"><span data-stu-id="05a33-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="05a33-120">**Consultez également :** [Documentation sur l’interface utilisateur - Paramètres][Link 20]</span><span class="sxs-lookup"><span data-stu-id="05a33-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="05a33-121">**Profil utilisateur :** vous pouvez cibler votre audience en fonction des informations d’utilisateur standard et des informations d’application personnalisées que vous avez créées.</span><span class="sxs-lookup"><span data-stu-id="05a33-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span></span> <span data-ttu-id="05a33-122">Cela inclut les utilisateurs qui sont actuellement connectés et les utilisateurs qui ont répondu à des questions spécifiques que vous leur avez demandé de définir dans l’application même, plutôt que leurs réponses aux campagnes précédentes.</span><span class="sxs-lookup"><span data-stu-id="05a33-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span></span> <span data-ttu-id="05a33-123">Toutes les informations définies pour votre application sont indiquées dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="05a33-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="05a33-124">Segments : vous pouvez également cibler votre audience en fonction des segments que vous avez créés suivant le comportement spécifique des utilisateurs et contenant des critères multiples.</span><span class="sxs-lookup"><span data-stu-id="05a33-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="05a33-125">Tous les segments définis pour votre application sont indiqués dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="05a33-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="05a33-126">**Consultez également :** [Documentation sur l’interface utilisateur - Segments][Link 18]</span><span class="sxs-lookup"><span data-stu-id="05a33-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="05a33-127">**Informations relatives à l’application :** les balises d’informations personnalisées relatives à l’application peuvent être créées depuis la section « Paramètres » afin de suivre le comportement des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="05a33-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span></span> <span data-ttu-id="05a33-128">**Consultez également :** [Documentation sur l’interface utilisateur - Paramètres][Link 20]</span><span class="sxs-lookup"><span data-stu-id="05a33-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="05a33-129">Exemple :</span><span class="sxs-lookup"><span data-stu-id="05a33-129">Example:</span></span>
<span data-ttu-id="05a33-130">Si vous souhaitez effectuer une transmission de type Push pour faire une annonce uniquement à un sous-ensemble de vos utilisateurs qui ont réalisé un achat dans l’application.</span><span class="sxs-lookup"><span data-stu-id="05a33-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="05a33-131">Rendez-vous sur la page des paramètres de l’application, sélectionnez le menu « Informations relatives à l’application » puis sélectionnez « Nouvelle information relative à l’application ».</span><span class="sxs-lookup"><span data-stu-id="05a33-131">Go to your application settings page, select the "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="05a33-132">Enregistrez une nouvelle information booléenne relative à l'application appelée « inAppPurchase ».</span><span class="sxs-lookup"><span data-stu-id="05a33-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="05a33-133">Cette information relative à l’application doit être définie sur « true » par votre application lorsque l’utilisateur réussit à réaliser un achat dans l’application (à l’aide de la fonction sendAppInfo (« inAppPurchase », ...)).</span><span class="sxs-lookup"><span data-stu-id="05a33-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="05a33-134">Si vous ne souhaitez pas faire cela depuis votre application, vous pouvez le faire depuis le serveur principal à l'aide de l'API de l'appareil.</span><span class="sxs-lookup"><span data-stu-id="05a33-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span></span>
5. <span data-ttu-id="05a33-135">Vous n'aurez ensuite qu'à créer votre annonce avec un critère limitant votre audience aux utilisateurs ayant « inAppPurchase » défini sur « vrai ».</span><span class="sxs-lookup"><span data-stu-id="05a33-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span></span>

> [!NOTE]
> <span data-ttu-id="05a33-136">Le ciblage basé sur un autre critère que les balises d'informations relatives à l'application nécessite un regroupement d'informations par Azure Mobile Engagement à partir des appareils de vos utilisateurs avant que la notification Push ne soit envoyée et qu'elle n'entraîne un retard.</span><span class="sxs-lookup"><span data-stu-id="05a33-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span></span> <span data-ttu-id="05a33-137">Les options de configuration de notifications Push complexes (telles que la mise à jour des badges) peuvent également entraîner des retards.</span><span class="sxs-lookup"><span data-stu-id="05a33-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="05a33-138">L'utilisation de la campagne unique depuis l'API Push est la méthode Push la plus rapide dans Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="05a33-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="05a33-139">L'utilisation des balises d'informations relatives à l'application en tant que critères Push pour une campagne Reach (depuis l'API Reach ou l'IU) est la deuxième méthode la plus rapide puisque ces balises d'informations sont stockées côté serveur.</span><span class="sxs-lookup"><span data-stu-id="05a33-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span></span> <span data-ttu-id="05a33-140">L'utilisation d'autres critères de ciblage pour une campagne Push est la méthode la plus flexible mais la plus lente, car Azure Mobile Engagement doit interroger les appareils afin d'envoyer la campagne.</span><span class="sxs-lookup"><span data-stu-id="05a33-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="05a33-142">Les options de critère s'appliquent à :</span><span class="sxs-lookup"><span data-stu-id="05a33-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="05a33-143">**Informations techniques**</span><span class="sxs-lookup"><span data-stu-id="05a33-143">**Technicals**</span></span>     
* <span data-ttu-id="05a33-144">Nom du microprogramme : nom du microprogramme</span><span class="sxs-lookup"><span data-stu-id="05a33-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="05a33-145">Version du microprogramme : version du microprogramme</span><span class="sxs-lookup"><span data-stu-id="05a33-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="05a33-146">Modèle de l’appareil : modèle de l’appareil</span><span class="sxs-lookup"><span data-stu-id="05a33-146">Device model:    Device model</span></span>
* <span data-ttu-id="05a33-147">Fabricant de l’appareil : fabricant de l’appareil</span><span class="sxs-lookup"><span data-stu-id="05a33-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="05a33-148">Version de l’application : version de l’application</span><span class="sxs-lookup"><span data-stu-id="05a33-148">Application version:    Application version</span></span>
* <span data-ttu-id="05a33-149">Nom de l’opérateur : nom de l’opérateur, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="05a33-150">Pays de l’opérateur : pays de l’opérateur, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="05a33-151">Type de réseau : type de réseau</span><span class="sxs-lookup"><span data-stu-id="05a33-151">Network type:    Network type</span></span>
* <span data-ttu-id="05a33-152">Paramètres régionaux : paramètres régionaux</span><span class="sxs-lookup"><span data-stu-id="05a33-152">Locale:    Locale</span></span>
* <span data-ttu-id="05a33-153">Taille de l’écran : taille de l’écran</span><span class="sxs-lookup"><span data-stu-id="05a33-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="05a33-154">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="05a33-154">**Location**</span></span>      
* <span data-ttu-id="05a33-155">Dernière région connue : pays, région, localité</span><span class="sxs-lookup"><span data-stu-id="05a33-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="05a33-156">Géofencing en temps réel : liste des POI (points d’intérêts) (nom, actions), POI circulaires (nom, latitude, longitude, rayon en mètres)</span><span class="sxs-lookup"><span data-stu-id="05a33-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="05a33-157">**Commentaire Reach**</span><span class="sxs-lookup"><span data-stu-id="05a33-157">**Reach feedback**</span></span>     
* <span data-ttu-id="05a33-158">Commentaire de l’annonce : annonce, commentaire</span><span class="sxs-lookup"><span data-stu-id="05a33-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="05a33-159">Commentaire du sondage : sondage, commentaire</span><span class="sxs-lookup"><span data-stu-id="05a33-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="05a33-160">Commentaire de réponse du sondage : commentaire de réponse du sondage, question, choix</span><span class="sxs-lookup"><span data-stu-id="05a33-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="05a33-161">Commentaire du Push de données : Push de données, commentaire</span><span class="sxs-lookup"><span data-stu-id="05a33-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="05a33-162">**Installation du suivi**</span><span class="sxs-lookup"><span data-stu-id="05a33-162">**Install Tracking**</span></span>     
* <span data-ttu-id="05a33-163">Store : Store, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="05a33-164">Source: source, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="05a33-165">**Profil utilisateur**</span><span class="sxs-lookup"><span data-stu-id="05a33-165">**User profile**</span></span>     
* <span data-ttu-id="05a33-166">Sexe : masculin ou féminin, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="05a33-167">Date de naissance : opérateur, date, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="05a33-168">Accepter : vrai ou faux, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="05a33-169">**Informations sur l’application**</span><span class="sxs-lookup"><span data-stu-id="05a33-169">**App Info**</span></span>      
* <span data-ttu-id="05a33-170">Chaîne : chaîne, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-170">String:    String, undefined</span></span>
* <span data-ttu-id="05a33-171">Date : opérateur, date, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="05a33-172">Entier : opérateur, nombre, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="05a33-173">Booléen : true ou false, non défini</span><span class="sxs-lookup"><span data-stu-id="05a33-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="05a33-174">**Segment**</span><span class="sxs-lookup"><span data-stu-id="05a33-174">**Segment**</span></span>    
* <span data-ttu-id="05a33-175">Nom des segments (de la liste déroulante), exclusion (utilisateurs cibles qui ne font pas partie de ce segment).</span><span class="sxs-lookup"><span data-stu-id="05a33-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
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

