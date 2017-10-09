---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - atteindre la campagne"
description: "Laern comment toocreate et gérer des campagnes de notification push à l’aide d’Azure Mobile Engagement"
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
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="f93b1-103">Comment toocreate et gérer des campagnes de notification push</span><span class="sxs-lookup"><span data-stu-id="f93b1-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="f93b1-104">Vous pouvez utiliser hello section portée de l’interface utilisateur de hello toocreate une nouvelle campagne de Push avec une formule complexe en fournissant toutes les informations de hello vous devez toosend une notification push.</span><span class="sxs-lookup"><span data-stu-id="f93b1-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="f93b1-105">Hello options d’une campagne de Push varient légèrement en fonction des types de campagne hello quatre : annonces, sondages, exécute un push de données et des vignettes (Windows Phone uniquement).</span><span class="sxs-lookup"><span data-stu-id="f93b1-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="f93b1-106">L'option s'applique à :</span><span class="sxs-lookup"><span data-stu-id="f93b1-106">Option Applies to:</span></span>
* <span data-ttu-id="f93b1-107">Langues : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-108">Campagne : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-109">Notification : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="f93b1-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="f93b1-110">Contenu : unique pour chaque type de campagne</span><span class="sxs-lookup"><span data-stu-id="f93b1-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="f93b1-111">Audience : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-112">Délai d’exécution : Annonces, Sondages et Vignettes</span><span class="sxs-lookup"><span data-stu-id="f93b1-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="f93b1-113">Test : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="f93b1-115">Langues</span><span class="sxs-lookup"><span data-stu-id="f93b1-115">Languages</span></span>
<span data-ttu-id="f93b1-116">Vous pouvez utiliser hello déroulante langues menu toosend une version différente de votre toodevices par émission de données qui sont définies toouse différentes langues.</span><span class="sxs-lookup"><span data-stu-id="f93b1-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="f93b1-117">Par défaut, tous les appareils recevront hello même Push quelle que soit la langue qu’ils sont toouse.</span><span class="sxs-lookup"><span data-stu-id="f93b1-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="f93b1-118">Utilisateurs avec leur appareils ensemble tooa autre langue reçoivent une version de langue par défaut hello Hello par émission de données.</span><span class="sxs-lookup"><span data-stu-id="f93b1-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="f93b1-119">La plupart des options de campagne push hello permettent toospecify un contenu de remplacement pour chacune des langues supplémentaires hello que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="f93b1-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="f93b1-121">Les différences linguistiques s'appliquent à :</span><span class="sxs-lookup"><span data-stu-id="f93b1-121">Language differences apply to:</span></span>
* <span data-ttu-id="f93b1-122">Langues : Langues Unique peuvent être sélectionnés dans la langue par défaut de toohello Ajout</span><span class="sxs-lookup"><span data-stu-id="f93b1-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="f93b1-123">Campagne : identique pour toutes les langues</span><span class="sxs-lookup"><span data-stu-id="f93b1-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="f93b1-124">Notification : Uniques pour chaque langue en outre toohello langue par défaut</span><span class="sxs-lookup"><span data-stu-id="f93b1-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="f93b1-125">Contenu : Uniques pour chaque langue en outre toohello langue par défaut</span><span class="sxs-lookup"><span data-stu-id="f93b1-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="f93b1-126">Audience : peut être filtrée par un critère de langue distinct</span><span class="sxs-lookup"><span data-stu-id="f93b1-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="f93b1-127">Délai d’exécution : identique pour toutes les langues</span><span class="sxs-lookup"><span data-stu-id="f93b1-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="f93b1-128">Test : Tooeach langue à la fois peuvent être envoyés</span><span class="sxs-lookup"><span data-stu-id="f93b1-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="f93b1-129">Langues prises en charge :</span><span class="sxs-lookup"><span data-stu-id="f93b1-129">Supported Languages:</span></span>
* <span data-ttu-id="f93b1-130">Arabe (ar)</span><span class="sxs-lookup"><span data-stu-id="f93b1-130">Arabic (ar)</span></span> 
* <span data-ttu-id="f93b1-131">Bulgare (bg)</span><span class="sxs-lookup"><span data-stu-id="f93b1-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="f93b1-132">Catalan (ca)</span><span class="sxs-lookup"><span data-stu-id="f93b1-132">Catalan (ca)</span></span> 
* <span data-ttu-id="f93b1-133">Chinois (zh)</span><span class="sxs-lookup"><span data-stu-id="f93b1-133">Chinese (zh)</span></span> 
* <span data-ttu-id="f93b1-134">Croate (hr)</span><span class="sxs-lookup"><span data-stu-id="f93b1-134">Croatian (hr)</span></span> 
* <span data-ttu-id="f93b1-135">Tchèque (cs)</span><span class="sxs-lookup"><span data-stu-id="f93b1-135">Czech (cs)</span></span> 
* <span data-ttu-id="f93b1-136">Danois (da)</span><span class="sxs-lookup"><span data-stu-id="f93b1-136">Danish (da)</span></span> 
* <span data-ttu-id="f93b1-137">Néerlandais (nl)</span><span class="sxs-lookup"><span data-stu-id="f93b1-137">Dutch (nl)</span></span> 
* <span data-ttu-id="f93b1-138">Anglais (en)</span><span class="sxs-lookup"><span data-stu-id="f93b1-138">English (en)</span></span> 
* <span data-ttu-id="f93b1-139">Finnois (fi)</span><span class="sxs-lookup"><span data-stu-id="f93b1-139">Finnish (fi)</span></span> 
* <span data-ttu-id="f93b1-140">Français (fr)</span><span class="sxs-lookup"><span data-stu-id="f93b1-140">French (fr)</span></span> 
* <span data-ttu-id="f93b1-141">Allemand (de)</span><span class="sxs-lookup"><span data-stu-id="f93b1-141">German (de)</span></span> 
* <span data-ttu-id="f93b1-142">Grec (el)</span><span class="sxs-lookup"><span data-stu-id="f93b1-142">Greek (el)</span></span> 
* <span data-ttu-id="f93b1-143">Hébreu (he)</span><span class="sxs-lookup"><span data-stu-id="f93b1-143">Hebrew (he)</span></span> 
* <span data-ttu-id="f93b1-144">Hindi (hi)</span><span class="sxs-lookup"><span data-stu-id="f93b1-144">Hindi (hi)</span></span> 
* <span data-ttu-id="f93b1-145">Hongrois (hu)</span><span class="sxs-lookup"><span data-stu-id="f93b1-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="f93b1-146">Indonésien (id)</span><span class="sxs-lookup"><span data-stu-id="f93b1-146">Indonesian (id)</span></span> 
* <span data-ttu-id="f93b1-147">Italien (it)</span><span class="sxs-lookup"><span data-stu-id="f93b1-147">Italian (it)</span></span> 
* <span data-ttu-id="f93b1-148">Japonais (ja)</span><span class="sxs-lookup"><span data-stu-id="f93b1-148">Japanese (ja)</span></span> 
* <span data-ttu-id="f93b1-149">Coréen (ko)</span><span class="sxs-lookup"><span data-stu-id="f93b1-149">Korean (ko)</span></span> 
* <span data-ttu-id="f93b1-150">Letton (lv)</span><span class="sxs-lookup"><span data-stu-id="f93b1-150">Latvian (lv)</span></span> 
* <span data-ttu-id="f93b1-151">Lituanien (lt)</span><span class="sxs-lookup"><span data-stu-id="f93b1-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="f93b1-152">Malais (macro-langue) (ms)</span><span class="sxs-lookup"><span data-stu-id="f93b1-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="f93b1-153">Norvégien Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="f93b1-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="f93b1-154">Polonais (pl)</span><span class="sxs-lookup"><span data-stu-id="f93b1-154">Polish (pl)</span></span> 
* <span data-ttu-id="f93b1-155">Portugais (pt)</span><span class="sxs-lookup"><span data-stu-id="f93b1-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="f93b1-156">Roumain (ro)</span><span class="sxs-lookup"><span data-stu-id="f93b1-156">Romanian (ro)</span></span> 
* <span data-ttu-id="f93b1-157">Russe (ru)</span><span class="sxs-lookup"><span data-stu-id="f93b1-157">Russian (ru)</span></span> 
* <span data-ttu-id="f93b1-158">Serbe (sr)</span><span class="sxs-lookup"><span data-stu-id="f93b1-158">Serbian (sr)</span></span> 
* <span data-ttu-id="f93b1-159">Slovaque (sk)</span><span class="sxs-lookup"><span data-stu-id="f93b1-159">Slovak (sk)</span></span> 
* <span data-ttu-id="f93b1-160">Slovène (sl)</span><span class="sxs-lookup"><span data-stu-id="f93b1-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="f93b1-161">Espagnol (es)</span><span class="sxs-lookup"><span data-stu-id="f93b1-161">Spanish (es)</span></span> 
* <span data-ttu-id="f93b1-162">Suédois (sv)</span><span class="sxs-lookup"><span data-stu-id="f93b1-162">Swedish (sv)</span></span> 
* <span data-ttu-id="f93b1-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="f93b1-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="f93b1-164">Thaï (th)</span><span class="sxs-lookup"><span data-stu-id="f93b1-164">Thai (th)</span></span> 
* <span data-ttu-id="f93b1-165">Turc (tr)</span><span class="sxs-lookup"><span data-stu-id="f93b1-165">Turkish (tr)</span></span> 
* <span data-ttu-id="f93b1-166">Ukrainien (uk)</span><span class="sxs-lookup"><span data-stu-id="f93b1-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="f93b1-167">Vietnamien (vi)</span><span class="sxs-lookup"><span data-stu-id="f93b1-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="f93b1-168">Campagne</span><span class="sxs-lookup"><span data-stu-id="f93b1-168">Campaign</span></span>
<span data-ttu-id="f93b1-169">Vous pouvez utiliser hello campagne section tooset hello nom et la catégorie de votre campagne ainsi que si vous envisagez de section d’audience hello tooignore d’une campagne de Push et que vous envoyez à la place de cette campagne via hello API couverture (et certains éléments de niveau de faible hello API de Push).</span><span class="sxs-lookup"><span data-stu-id="f93b1-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="f93b1-170">Catégories peuvent être utilisées avec une notification personnalisée modèle toocontrol dans l’application des notifications en fonction des paramètres prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="f93b1-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="f93b1-171">Vous pouvez obtenir une liste de vos « catégories » via l’API couverture de hello.</span><span class="sxs-lookup"><span data-stu-id="f93b1-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="f93b1-172">Si vous utilisez option de « Ignorer Audience, push seront envoyés toousers via hello API » hello de section de « De la campagne » hello d’une couverture campagne, campagne de hello n’envoie pas automatiquement, vous devez toosend manuellement via l’API couverture de hello.</span><span class="sxs-lookup"><span data-stu-id="f93b1-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="f93b1-174">L'option s'applique à :</span><span class="sxs-lookup"><span data-stu-id="f93b1-174">Option Applies to:</span></span>
* <span data-ttu-id="f93b1-175">Nom : toutes</span><span class="sxs-lookup"><span data-stu-id="f93b1-175">Name:    All</span></span>
* <span data-ttu-id="f93b1-176">Catégorie : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="f93b1-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="f93b1-177">Ignorer l’Audience push seront envoyés toousers via hello API : tous les</span><span class="sxs-lookup"><span data-stu-id="f93b1-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="f93b1-178">Notification</span><span class="sxs-lookup"><span data-stu-id="f93b1-178">Notification</span></span>
<span data-ttu-id="f93b1-179">Vous pouvez utiliser les paramètres de base hello Notification section tooset pour votre commande, notamment : hello titre Hello Push, le message de type hello, une image dans l’application, ou si elle est révocables.</span><span class="sxs-lookup"><span data-stu-id="f93b1-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="f93b1-180">De nombreux paramètres de notification sont toohello spécifique à la plateforme de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="f93b1-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="f93b1-181">Vous pouvez choisir d'envoyer votre notification Push depuis l'application ou en dehors de l'application, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="f93b1-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="f93b1-182">(N’oubliez pas que les utilisateurs peuvent « opt-in » ou « annuler » de « hors de l’application » transmet au système d’exploitation de hello niveau sur leurs appareils, Azure Mobile Engagement à ne pas être en mesure de toooverride ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="f93b1-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="f93b1-183">Également n’oubliez pas que gère les API de portée hello « dans l’application » exécute un push de « hors de l’application ».</span><span class="sxs-lookup"><span data-stu-id="f93b1-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="f93b1-184">Hello API de Push peut être utilisé toohandle « du délai d’attente d’application » exécute un push de trop.) Push peut être personnalisée avec des images ou du contenu HTML, y compris des liens ciblés pour la liaison en dehors de votre application ou tooanother l’emplacement dans votre application (Kit de développement logiciel Android 2.1.0 ou ultérieure catégories intentionnels requis).</span><span class="sxs-lookup"><span data-stu-id="f93b1-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="f93b1-185">Vous pouvez modifier le badge d’icône ou iOS hello et envoyer le contenu de texte ou web (un popup avec html, URL lien tooanother emplacement du contenu à l’intérieur ou en dehors de l’application hello).</span><span class="sxs-lookup"><span data-stu-id="f93b1-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="f93b1-186">Vous pouvez également faire sonner des appareils Android ou faire vibrer avec hello par émission de données.</span><span class="sxs-lookup"><span data-stu-id="f93b1-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="f93b1-187">(N’oubliez pas que vous serez peut-être hello correcte des autorisations dans votre Android SDK tooring du fichier de manifeste ou faire vibrer un appareil). Il n'y a actuellement aucune norme industrielle pour les tailles « Grand format » puisque la taille des écrans est différente pour chaque appareil. Toutefois, les images 400 x 100 fonctionnent sur presque toutes les tailles d'écran.</span><span class="sxs-lookup"><span data-stu-id="f93b1-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="f93b1-188">Types d'envoi :</span><span class="sxs-lookup"><span data-stu-id="f93b1-188">Delivery Types:</span></span>
* <span data-ttu-id="f93b1-189">Hors de l’application uniquement : hello notification arrive lorsque l’utilisateur de hello n’utilise pas l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f93b1-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="f93b1-190">Hello hors de notification uniquement de l’application requiert un certificat à partir d’Apple ou Google (certificat APN ou GCM).</span><span class="sxs-lookup"><span data-stu-id="f93b1-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="f93b1-191">Dans l’application uniquement : notification de hello s’affiche uniquement lorsque l’application hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="f93b1-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="f93b1-192">notification de Hello utilise hello Capptain remise système tooreach hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f93b1-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="f93b1-193">Vous pouvez entièrement personnaliser hello disposition/affichage visuel de votre publication.</span><span class="sxs-lookup"><span data-stu-id="f93b1-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="f93b1-194">À tout moment : Cette option permet de s’assurer que vous envoyez une notification de que l’application hello est en cours d’exécution ou non.</span><span class="sxs-lookup"><span data-stu-id="f93b1-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="f93b1-196">L'option s'applique à :</span><span class="sxs-lookup"><span data-stu-id="f93b1-196">Option Applies to:</span></span>
* <span data-ttu-id="f93b1-197">Notification : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="f93b1-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="f93b1-198">Contenu</span><span class="sxs-lookup"><span data-stu-id="f93b1-198">Content</span></span>
<span data-ttu-id="f93b1-199">Vous pouvez utiliser le contenu de hello toomodify hello section de contenu des annonces, sondages, exécute un push de données et des vignettes (Windows Phone uniquement).</span><span class="sxs-lookup"><span data-stu-id="f93b1-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="f93b1-200">le paramètre de contenu Hello de campagnes Push est type toohello spécifique de campagne.</span><span class="sxs-lookup"><span data-stu-id="f93b1-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="f93b1-201">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f93b1-201">See also</span></span>
* <span data-ttu-id="f93b1-202">[Documentation de l’interface utilisateur - Reach - Contenu Push][Link 29]</span><span class="sxs-lookup"><span data-stu-id="f93b1-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="f93b1-204">Public ciblé</span><span class="sxs-lookup"><span data-stu-id="f93b1-204">Audience</span></span>
<span data-ttu-id="f93b1-205">Vous pouvez utiliser hello Audience section toodefine une liste standard des éléments toolimit votre campagne ou les limites de votre campagne en fonction de critères personnalisés.</span><span class="sxs-lookup"><span data-stu-id="f93b1-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="f93b1-206">Hello standard d’options tooLimit votre Audience vous permet d’utilisateurs de nouveau ou ancien de tooeither toopush ou push natif uniquement.</span><span class="sxs-lookup"><span data-stu-id="f93b1-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="f93b1-207">Vous pouvez également définir un nombre de hello toolimit quota des utilisateurs qui reçoivent les push hello.</span><span class="sxs-lookup"><span data-stu-id="f93b1-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="f93b1-208">Vous pouvez modifier manuellement l’expression hello pour comment votre campagne est filtré tooinclude un ou plusieurs utilisateurs tootarget de critère.</span><span class="sxs-lookup"><span data-stu-id="f93b1-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="f93b1-209">Vous pouvez taper manuellement une expression d'audience.</span><span class="sxs-lookup"><span data-stu-id="f93b1-209">You can manually type an audience expression.</span></span> <span data-ttu-id="f93b1-210">Une telle expression doit définir explicitement la relation hello entre les critères.</span><span class="sxs-lookup"><span data-stu-id="f93b1-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="f93b1-211">Un critère est décrit par un identificateur qui doit commencer par une majuscule et ne peut pas contenir d'espace.</span><span class="sxs-lookup"><span data-stu-id="f93b1-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="f93b1-212">relation Hello entre les critères de hello peut être décrite à l’aide de 'and', 'or', 'not' opérateurs ainsi que '(',')'.</span><span class="sxs-lookup"><span data-stu-id="f93b1-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="f93b1-213">Exemple : « Critère1 ou (Critère1 sans Critère2) ».</span><span class="sxs-lookup"><span data-stu-id="f93b1-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="f93b1-214">Avec un grand public inclus dans les campagnes, SSI hello ciblage d’analyse peut être lent, surtout si vous essayez de toostart plusieurs campagnes à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="f93b1-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="f93b1-215">Si possible, ne démarrez qu'une campagne à la fois.</span><span class="sxs-lookup"><span data-stu-id="f93b1-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="f93b1-216">À hello plus uniquement démarrer quatre campagnes à la fois.</span><span class="sxs-lookup"><span data-stu-id="f93b1-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="f93b1-217">Transmettre uniquement les utilisateurs actifs tooyour (case à cocher « retenir uniquement les utilisateurs qui peuvent être atteints à l’aide de Push natif » et « Retenir uniquement les utilisateurs actifs ») afin que seuls vos utilisateurs ayant toujours application hello installée et l’utiliser doivent toobe analysé.</span><span class="sxs-lookup"><span data-stu-id="f93b1-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="f93b1-218">Une fois que votre audience est défini, vous pouvez utiliser hello simuler toofind bouton out combien d’utilisateurs recevront cette opération Push.</span><span class="sxs-lookup"><span data-stu-id="f93b1-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="f93b1-219">Il calcule le nombre hello d’utilisateurs connus potentiellement ciblé par cette audience (Ceci est une estimation basée sur un échantillon aléatoire d’utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="f93b1-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="f93b1-220">N’oubliez pas que les utilisateurs qui ont désinstallé l’application hello font également partie de cette audience, mais qu’il ne peut pas être atteint.</span><span class="sxs-lookup"><span data-stu-id="f93b1-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="f93b1-221">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f93b1-221">See also</span></span>
* <span data-ttu-id="f93b1-222">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="f93b1-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="f93b1-224">Modifier l'expression</span><span class="sxs-lookup"><span data-stu-id="f93b1-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="f93b1-226">L'option de limitation de votre audience s'applique à :</span><span class="sxs-lookup"><span data-stu-id="f93b1-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="f93b1-227">Solliciter uniquement un sous-ensemble d’utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-228">Solliciter uniquement d’anciens utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-229">Solliciter uniquement de nouveaux utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-230">Solliciter uniquement des utilisateurs inactifs : Annonces, Sondages et Vignettes</span><span class="sxs-lookup"><span data-stu-id="f93b1-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="f93b1-231">Solliciter uniquement des utilisateurs actifs : toutes (Annonces, Sondages, Push de données et Vignettes)</span><span class="sxs-lookup"><span data-stu-id="f93b1-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="f93b1-232">Solliciter uniquement des utilisateurs qui peuvent être contactés via un Push natif : Annonces et Sondages</span><span class="sxs-lookup"><span data-stu-id="f93b1-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="f93b1-233">Délai d'exécution</span><span class="sxs-lookup"><span data-stu-id="f93b1-233">Time Frame</span></span>
<span data-ttu-id="f93b1-234">Vous pouvez utiliser hello laps de temps section tooset lorsque hello push seront envoyés, ou vous pouvez laisser immédiatement campagne de hello toostart vide hello laps de temps.</span><span class="sxs-lookup"><span data-stu-id="f93b1-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="f93b1-235">N’oubliez pas qu’à l’aide du fuseau horaire d’utilisateurs finaux hello peut démarrer hello campagne un jour plus tôt que prévu pour vos utilisateurs finaux en Asie et envoyer des lots de petite taille de push à la fois jusqu'à ce que tous les fuseaux horaires dans le laps de temps hello hello world correspondance définie pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="f93b1-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="f93b1-236">À l’aide du fuseau horaire de hello utilisateurs peut également entraîner des retards dans les campagnes, car elle comprend le temps de hello toorequest à partir de téléphone de hello avant de push de hello.</span><span class="sxs-lookup"><span data-stu-id="f93b1-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="f93b1-237">Les campagnes qui n'ont pas de date de fin peuvent mettre en cache des notifications Push localement et continuer de les afficher une fois que vous avez terminé manuellement ces campagnes.</span><span class="sxs-lookup"><span data-stu-id="f93b1-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="f93b1-238">tooavoid ce comportement, le spécifique à une heure de fin pour les campagnes.</span><span class="sxs-lookup"><span data-stu-id="f93b1-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="f93b1-239">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f93b1-239">See also</span></span>
* <span data-ttu-id="f93b1-240">[Reach - Procédures - Planification][Link 3]</span><span class="sxs-lookup"><span data-stu-id="f93b1-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="f93b1-242">Les paramètres s'appliquent à :</span><span class="sxs-lookup"><span data-stu-id="f93b1-242">Settings Apply to:</span></span>
* <span data-ttu-id="f93b1-243">Délai d’exécution : Annonces, Sondages et Vignettes</span><span class="sxs-lookup"><span data-stu-id="f93b1-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="f93b1-244">Test</span><span class="sxs-lookup"><span data-stu-id="f93b1-244">Test</span></span>
<span data-ttu-id="f93b1-245">Vous pouvez utiliser hello Test section toosend cet appareil de test propre tooyour par émission de données avant d’enregistrer la campagne de hello.</span><span class="sxs-lookup"><span data-stu-id="f93b1-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="f93b1-246">Si vous avez configuré des langues personnalisées pour cette campagne, vous pouvez tester hello push dans chaque langue.</span><span class="sxs-lookup"><span data-stu-id="f93b1-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="f93b1-247">Vous pouvez configurer un appareil de test depuis « Mon compte ».</span><span class="sxs-lookup"><span data-stu-id="f93b1-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="f93b1-248">Exécute un push d’aucun côté serveur données sont enregistrées lorsque vous utilisez le bouton de hello trop « ne test », les données sont enregistrées uniquement pour les campagnes push réel.</span><span class="sxs-lookup"><span data-stu-id="f93b1-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="f93b1-249">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f93b1-249">See also</span></span>
* <span data-ttu-id="f93b1-250">[Documentation sur l’interface utilisateur - Mon compte][Link 14]</span><span class="sxs-lookup"><span data-stu-id="f93b1-250">[UI Documentation - My Account][Link 14]</span></span>

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

