---
title: "Interface utilisateur d'Azure Mobile Engagement - Campagne Reach"
description: "Découvrez comment créer et gérer les campagnes de notifications Push à l'aide d'Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="b5a2d-103">Création et gestion des campagnes de notification Push</span><span class="sxs-lookup"><span data-stu-id="b5a2d-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="b5a2d-104">Vous pouvez utiliser la section Reach de l'interface utilisateur pour créer une nouvelle campagne Push à l'aide d'une formule complexe en indiquant toutes les informations dont vous avez besoin pour envoyer une notification Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="b5a2d-105">Les options d'une campagne Push varient quelque peu selon les quatre types de campagne : Annonces, Sondages, Push de données et Vignettes (Windows Phone uniquement).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="b5a2d-106">L'option s'applique à :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-106">Option Applies to:</span></span>
* <span data-ttu-id="b5a2d-107">Langues : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-108">Campagne : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-109">Notification : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="b5a2d-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="b5a2d-110">Contenu : unique pour chaque type de campagne</span><span class="sxs-lookup"><span data-stu-id="b5a2d-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="b5a2d-111">Audience : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-112">Délai d’exécution : Annonces, Sondages et Vignettes</span><span class="sxs-lookup"><span data-stu-id="b5a2d-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="b5a2d-113">Test : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="b5a2d-115">Langues</span><span class="sxs-lookup"><span data-stu-id="b5a2d-115">Languages</span></span>
<span data-ttu-id="b5a2d-116">Vous pouvez utiliser le menu déroulant Langues pour envoyer une version différente de votre notification Push vers des appareils configurés pour d'autres langues.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="b5a2d-117">Par défaut, tous les appareils reçoivent la même notification Push, quelle que soit la langue pour laquelle ils sont configurés.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="b5a2d-118">Les utilisateurs qui disposent d'un appareil configuré pour une autre langue recevront la version de la notification Push dans la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="b5a2d-119">De nombreuses options de campagne Push vous permettent de spécifier un contenu différent pour chaque langue supplémentaire que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="b5a2d-121">Les différences linguistiques s'appliquent à :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-121">Language differences apply to:</span></span>
* <span data-ttu-id="b5a2d-122">Langues : des langues uniques peuvent être sélectionnées en complément de la langue par défaut</span><span class="sxs-lookup"><span data-stu-id="b5a2d-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="b5a2d-123">Campagne : identique pour toutes les langues</span><span class="sxs-lookup"><span data-stu-id="b5a2d-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="b5a2d-124">Notification : unique pour chaque langue ajoutée en complément de la langue par défaut</span><span class="sxs-lookup"><span data-stu-id="b5a2d-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="b5a2d-125">Contenu : unique pour chaque langue ajoutée en complément de la langue par défaut</span><span class="sxs-lookup"><span data-stu-id="b5a2d-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="b5a2d-126">Audience : peut être filtrée par un critère de langue distinct</span><span class="sxs-lookup"><span data-stu-id="b5a2d-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="b5a2d-127">Délai d’exécution : identique pour toutes les langues</span><span class="sxs-lookup"><span data-stu-id="b5a2d-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="b5a2d-128">Test : peut être envoyé pour chaque langue en même temps</span><span class="sxs-lookup"><span data-stu-id="b5a2d-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="b5a2d-129">Langues prises en charge :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-129">Supported Languages:</span></span>
* <span data-ttu-id="b5a2d-130">Arabe (ar)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-130">Arabic (ar)</span></span> 
* <span data-ttu-id="b5a2d-131">Bulgare (bg)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="b5a2d-132">Catalan (ca)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-132">Catalan (ca)</span></span> 
* <span data-ttu-id="b5a2d-133">Chinois (zh)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-133">Chinese (zh)</span></span> 
* <span data-ttu-id="b5a2d-134">Croate (hr)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-134">Croatian (hr)</span></span> 
* <span data-ttu-id="b5a2d-135">Tchèque (cs)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-135">Czech (cs)</span></span> 
* <span data-ttu-id="b5a2d-136">Danois (da)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-136">Danish (da)</span></span> 
* <span data-ttu-id="b5a2d-137">Néerlandais (nl)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-137">Dutch (nl)</span></span> 
* <span data-ttu-id="b5a2d-138">Anglais (en)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-138">English (en)</span></span> 
* <span data-ttu-id="b5a2d-139">Finnois (fi)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-139">Finnish (fi)</span></span> 
* <span data-ttu-id="b5a2d-140">Français (fr)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-140">French (fr)</span></span> 
* <span data-ttu-id="b5a2d-141">Allemand (de)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-141">German (de)</span></span> 
* <span data-ttu-id="b5a2d-142">Grec (el)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-142">Greek (el)</span></span> 
* <span data-ttu-id="b5a2d-143">Hébreu (he)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-143">Hebrew (he)</span></span> 
* <span data-ttu-id="b5a2d-144">Hindi (hi)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-144">Hindi (hi)</span></span> 
* <span data-ttu-id="b5a2d-145">Hongrois (hu)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="b5a2d-146">Indonésien (id)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-146">Indonesian (id)</span></span> 
* <span data-ttu-id="b5a2d-147">Italien (it)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-147">Italian (it)</span></span> 
* <span data-ttu-id="b5a2d-148">Japonais (ja)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-148">Japanese (ja)</span></span> 
* <span data-ttu-id="b5a2d-149">Coréen (ko)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-149">Korean (ko)</span></span> 
* <span data-ttu-id="b5a2d-150">Letton (lv)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-150">Latvian (lv)</span></span> 
* <span data-ttu-id="b5a2d-151">Lituanien (lt)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="b5a2d-152">Malais (macro-langue) (ms)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="b5a2d-153">Norvégien Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="b5a2d-154">Polonais (pl)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-154">Polish (pl)</span></span> 
* <span data-ttu-id="b5a2d-155">Portugais (pt)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="b5a2d-156">Roumain (ro)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-156">Romanian (ro)</span></span> 
* <span data-ttu-id="b5a2d-157">Russe (ru)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-157">Russian (ru)</span></span> 
* <span data-ttu-id="b5a2d-158">Serbe (sr)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-158">Serbian (sr)</span></span> 
* <span data-ttu-id="b5a2d-159">Slovaque (sk)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-159">Slovak (sk)</span></span> 
* <span data-ttu-id="b5a2d-160">Slovène (sl)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="b5a2d-161">Espagnol (es)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-161">Spanish (es)</span></span> 
* <span data-ttu-id="b5a2d-162">Suédois (sv)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-162">Swedish (sv)</span></span> 
* <span data-ttu-id="b5a2d-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="b5a2d-164">Thaï (th)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-164">Thai (th)</span></span> 
* <span data-ttu-id="b5a2d-165">Turc (tr)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-165">Turkish (tr)</span></span> 
* <span data-ttu-id="b5a2d-166">Ukrainien (uk)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="b5a2d-167">Vietnamien (vi)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="b5a2d-168">Campagne</span><span class="sxs-lookup"><span data-stu-id="b5a2d-168">Campaign</span></span>
<span data-ttu-id="b5a2d-169">Vous pouvez utiliser la section Campagne pour définir le nom et la catégorie de votre campagne et si vous envisagez d'ignorer la section Audience d'une campagne Push et d'envoyer cette campagne via l'API Reach (et certains éléments de l'API Push de bas niveau).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="b5a2d-170">Des catégories peuvent être utilisées avec un modèle de notification personnalisé pour contrôler les notifications dans l'application suivant des paramètres prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="b5a2d-171">Vous pouvez obtenir une liste de vos « Catégories » existantes via l'API Reach.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="b5a2d-172">Si vous utilisez l'option « Ignorer l'audience, la notification Push sera envoyée aux utilisateurs via l'API Reach » dans la section « Campagne » de la campagne Reach, cette campagne ne sera pas automatiquement envoyée. Vous devrez l'envoyer manuellement via l'API Reach.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="b5a2d-174">L'option s'applique à :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-174">Option Applies to:</span></span>
* <span data-ttu-id="b5a2d-175">Nom : toutes</span><span class="sxs-lookup"><span data-stu-id="b5a2d-175">Name:    All</span></span>
* <span data-ttu-id="b5a2d-176">Catégorie : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="b5a2d-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="b5a2d-177">Ignorer l’audience, la notification Push sera envoyée aux utilisateurs via l’API : toutes</span><span class="sxs-lookup"><span data-stu-id="b5a2d-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="b5a2d-178">Notification</span><span class="sxs-lookup"><span data-stu-id="b5a2d-178">Notification</span></span>
<span data-ttu-id="b5a2d-179">Utilisez la section Notification pour définir les paramètres de base pour votre notification Push, y compris : le titre de la notification Push, le message, une image dans l'application ou si elle peut être révocable.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="b5a2d-180">De nombreux paramètres de notification sont spécifiques à la plateforme de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="b5a2d-181">Vous pouvez choisir d'envoyer votre notification Push depuis l'application ou en dehors de l'application, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="b5a2d-182">(N'oubliez pas que les utilisateurs peuvent accepter ou refuser les notifications Push envoyées en dehors de l'application au niveau du système d'exploitation de leurs appareils. Azure Mobile Engagement ne peut pas remplacer ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="b5a2d-183">Rappelez-vous également que l'API Reach gère les notifications Push dans et en dehors de l'application</span><span class="sxs-lookup"><span data-stu-id="b5a2d-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="b5a2d-184">L'API Push peut également être utilisée pour gérer les notifications Push envoyées en dehors de l'application.) Les notifications Push peuvent être personnalisées avec des images ou du contenu HTML, notamment des liens ciblés menant hors de votre application ou vers un autre emplacement dans votre application (Kit de développement logiciel (SDK) Android 2.1.0 ou catégories d'intention ultérieures requises).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="b5a2d-185">Vous pouvez modifier l'icône ou le badge iOS et envoyer du texte ou du contenu Web (une fenêtre contextuelle avec du contenu HTML, un lien URL vers un autre emplacement dans ou en dehors de l'application).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="b5a2d-186">Vous pouvez aussi faire sonner ou vibrer les appareils Android avec la notification Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="b5a2d-187">(Rappelez-vous que vous aurez besoin des bonnes autorisations du Kit de développement logiciel (SDK) dans votre fichier manifeste Android pour faire sonner ou vibrer un appareil.) Il n'y a actuellement aucune norme industrielle pour les tailles « Grand format » puisque la taille des écrans est différente pour chaque appareil. Toutefois, les images 400 x 100 fonctionnent sur presque toutes les tailles d'écran.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="b5a2d-188">Types d'envoi :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-188">Delivery Types:</span></span>
* <span data-ttu-id="b5a2d-189">En dehors de l'application uniquement : la notification sera envoyée lorsque l'utilisateur n'utilisera pas son application.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="b5a2d-190">Ce type de notification requiert un certificat d'Apple ou de Google (certificat APNs ou GCM).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="b5a2d-191">Dans l'application uniquement : la notification apparaît uniquement lorsque l'application est exécutée.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="b5a2d-192">Cette notification utilise le système de messagerie Capptain pour contacter l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="b5a2d-193">Vous pouvez personnaliser entièrement l'affichage ou la disposition de votre notification Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="b5a2d-194">À tout moment : cette option garantit l'envoi de votre notification, que l'application soit exécutée ou non.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="b5a2d-196">L'option s'applique à :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-196">Option Applies to:</span></span>
* <span data-ttu-id="b5a2d-197">Notification : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="b5a2d-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="b5a2d-198">Contenu</span><span class="sxs-lookup"><span data-stu-id="b5a2d-198">Content</span></span>
<span data-ttu-id="b5a2d-199">Vous pouvez utiliser la section Contenu pour modifier le contenu de vos annonces, de vos sondages, de vos Push de données et de vos vignettes (Windows Phone uniquement).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="b5a2d-200">Le paramètre Contenu de vos campagnes Push est spécifique à chaque type de campagne.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="b5a2d-201">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b5a2d-201">See also</span></span>
* <span data-ttu-id="b5a2d-202">[Documentation de l’interface utilisateur - Reach - Contenu Push][Link 29]</span><span class="sxs-lookup"><span data-stu-id="b5a2d-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="b5a2d-204">Public ciblé</span><span class="sxs-lookup"><span data-stu-id="b5a2d-204">Audience</span></span>
<span data-ttu-id="b5a2d-205">Utilisez la section Audience pour définir une liste d'éléments standard pour limiter votre campagne ou pour définir les limites de votre campagne en fonction des critères personnalisés.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="b5a2d-206">L'ensemble des options standard pour limiter votre audience vous permet d'envoyer des notifications Push aux nouveaux ou aux anciens utilisateurs, ou aux utilisateurs des Push natifs uniquement.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="b5a2d-207">Vous pouvez également définir un quota pour limiter le nombre d'utilisateurs recevant la notification Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="b5a2d-208">Vous pouvez modifier manuellement l'expression pour définir la façon dont votre campagne est filtrée afin d'inclure un ou plusieurs critères pour les utilisateurs cibles.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="b5a2d-209">Vous pouvez taper manuellement une expression d'audience.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-209">You can manually type an audience expression.</span></span> <span data-ttu-id="b5a2d-210">Ce type d'expression doit définir explicitement la relation entre les critères.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="b5a2d-211">Un critère est décrit par un identificateur qui doit commencer par une majuscule et ne peut pas contenir d'espace.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="b5a2d-212">La relation entre les critères peut être décrite à l'aide des opérateurs and, or, not (et, ou, pas) ainsi que '(', ')'.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="b5a2d-213">Exemple : « Critère1 ou (Critère1 sans Critère2) ».</span><span class="sxs-lookup"><span data-stu-id="b5a2d-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="b5a2d-214">Si l'audience incluse dans les campagnes est importante, l'analyse de ciblage côté serveur peut être lente, en particulier si vous essayez de démarrer plusieurs campagnes en même temps.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="b5a2d-215">Si possible, ne démarrez qu'une campagne à la fois.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="b5a2d-216">Tout au plus, ne démarrez que quatre campagnes en même temps.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="b5a2d-217">Envoyez des notifications Push à vos utilisateurs actifs uniquement (case à cocher « Solliciter seulement les utilisateurs qui peuvent être contactés via un Push natif » et « Solliciter seulement les utilisateurs actifs ») de façon à ce que seuls les utilisateurs qui ont installé votre application et l'utilisent toujours doivent être analysés.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="b5a2d-218">Une fois votre audience définie, vous pouvez utiliser le bouton de simulation pour savoir combien d'utilisateurs recevront cette notification Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="b5a2d-219">Ce bouton calculera le nombre d'utilisateurs connus potentiellement ciblés par cette audience (il s'agit d'une estimation basée sur un échantillon aléatoire d'utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="b5a2d-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="b5a2d-220">Notez que les utilisateurs qui ont désinstallé l'application font également partie de l'audience mais ne peuvent pas être contactés.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5a2d-221">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b5a2d-221">See also</span></span>
* <span data-ttu-id="b5a2d-222">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="b5a2d-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="b5a2d-224">Modifier l'expression</span><span class="sxs-lookup"><span data-stu-id="b5a2d-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="b5a2d-226">L'option de limitation de votre audience s'applique à :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="b5a2d-227">Solliciter uniquement un sous-ensemble d’utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-228">Solliciter uniquement d’anciens utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-229">Solliciter uniquement de nouveaux utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-230">Solliciter uniquement des utilisateurs inactifs : Annonces, Sondages et Vignettes</span><span class="sxs-lookup"><span data-stu-id="b5a2d-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="b5a2d-231">Solliciter uniquement des utilisateurs actifs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="b5a2d-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b5a2d-232">Solliciter uniquement des utilisateurs qui peuvent être contactés via un Push natif : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="b5a2d-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="b5a2d-233">Délai d'exécution</span><span class="sxs-lookup"><span data-stu-id="b5a2d-233">Time Frame</span></span>
<span data-ttu-id="b5a2d-234">Vous pouvez utiliser la section Délai d'exécution pour définir à quel moment la notification Push sera envoyée ou vous pouvez laisser le champ Délai d'exécution vide pour démarrer immédiatement la campagne.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="b5a2d-235">Notez que l'utilisation du fuseau horaire de l'utilisateur final peut faire démarrer la campagne un jour plus tôt que prévu pour vos utilisateurs en Asie et envoyer des petits lots de notifications Push à une certaine heure jusqu'à ce que tous les fuseaux horaires du monde correspondent au délai d'exécution défini pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="b5a2d-236">L'utilisation du fuseau horaire des utilisateurs finaux peut également entraîner des retards dans les campagnes puisque cela nécessite de connaître l'heure du téléphone avant de démarrer l'envoi des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a2d-237">Les campagnes qui n'ont pas de date de fin peuvent mettre en cache des notifications Push localement et continuer de les afficher une fois que vous avez terminé manuellement ces campagnes.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="b5a2d-238">Pour éviter cela, indiquer une date de fin pour ces campagnes.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5a2d-239">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b5a2d-239">See also</span></span>
* <span data-ttu-id="b5a2d-240">[Reach - Procédures - Planification][Link 3]</span><span class="sxs-lookup"><span data-stu-id="b5a2d-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="b5a2d-242">Les paramètres s'appliquent à :</span><span class="sxs-lookup"><span data-stu-id="b5a2d-242">Settings Apply to:</span></span>
* <span data-ttu-id="b5a2d-243">Délai d’exécution : Annonces, Sondages et Vignettes</span><span class="sxs-lookup"><span data-stu-id="b5a2d-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="b5a2d-244">Test</span><span class="sxs-lookup"><span data-stu-id="b5a2d-244">Test</span></span>
<span data-ttu-id="b5a2d-245">Vous pouvez utiliser la section Test pour envoyer cette notification Push à votre propre appareil de test avant d'enregistrer la campagne.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="b5a2d-246">Si vous avez configuré des langues personnalisées pour cette campagne, vous pouvez tester la notification Push pour ces langues.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="b5a2d-247">Vous pouvez configurer un appareil de test depuis « Mon compte ».</span><span class="sxs-lookup"><span data-stu-id="b5a2d-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a2d-248">Aucune donnée côté serveur n'est enregistrée lorsque vous utilisez le bouton pour « tester » les notifications Push. Les données sont enregistrées uniquement pour les vraies campagnes de notification Push.</span><span class="sxs-lookup"><span data-stu-id="b5a2d-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5a2d-249">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b5a2d-249">See also</span></span>
* <span data-ttu-id="b5a2d-250">[Documentation sur l’interface utilisateur - Mon compte][Link 14]</span><span class="sxs-lookup"><span data-stu-id="b5a2d-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach-Campaign9][28]

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

