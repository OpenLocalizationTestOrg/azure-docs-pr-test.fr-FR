---
title: "Interface utilisateur d’Azure Mobile Engagement - Contenu Reach"
description: "Apprenez à gérer le contenu unique des différents types de campagnes de notifications Push dans Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="96f87-103">Gestion du contenu unique des différents types de campagnes de notifications Push</span><span class="sxs-lookup"><span data-stu-id="96f87-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="96f87-104">Vous pouvez utiliser la section Contenu d'une nouvelle campagne Reach pour modifier le contenu de vos annonces, sondages, Push de données et vignettes (Windows Phone uniquement).</span><span class="sxs-lookup"><span data-stu-id="96f87-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="96f87-105">Le paramètre du contenu des campagnes Push est spécifique au type de campagne.</span><span class="sxs-lookup"><span data-stu-id="96f87-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="96f87-106">Types de contenu :</span><span class="sxs-lookup"><span data-stu-id="96f87-106">Content types:</span></span>
* <span data-ttu-id="96f87-107">Annonces</span><span class="sxs-lookup"><span data-stu-id="96f87-107">Announcements</span></span>
* <span data-ttu-id="96f87-108">Sondages</span><span class="sxs-lookup"><span data-stu-id="96f87-108">Polls</span></span>
* <span data-ttu-id="96f87-109">Push de données</span><span class="sxs-lookup"><span data-stu-id="96f87-109">Data pushes</span></span>
* <span data-ttu-id="96f87-110">Vignettes (Windows Phone uniquement)</span><span class="sxs-lookup"><span data-stu-id="96f87-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="96f87-111">Contenu des annonces</span><span class="sxs-lookup"><span data-stu-id="96f87-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="96f87-113">Choisissez le type de votre annonce :</span><span class="sxs-lookup"><span data-stu-id="96f87-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="96f87-114">Notification uniquement : il s’agit d’une simple notification standard.</span><span class="sxs-lookup"><span data-stu-id="96f87-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="96f87-115">Cela signifie que si un utilisateur clique dessus, aucun affichage supplémentaire n'apparaîtra. Seule l'action qui y est associée s'affichera.</span><span class="sxs-lookup"><span data-stu-id="96f87-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="96f87-116">Annonce texte : il s’agit d’une notification qui invite l’utilisateur à regarder une vue de texte.</span><span class="sxs-lookup"><span data-stu-id="96f87-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="96f87-117">Annonce Web : il s’agit d’une notification qui invite l’utilisateur à regarder l’affichage Web.</span><span class="sxs-lookup"><span data-stu-id="96f87-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="96f87-118">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96f87-118">See also</span></span>
* <span data-ttu-id="96f87-119">[Reach - Procédures - Annonces][Link 3]</span><span class="sxs-lookup"><span data-stu-id="96f87-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="96f87-120">À propos des annonces d'affichage Web :</span><span class="sxs-lookup"><span data-stu-id="96f87-120">About Web View Announcements:</span></span>
<span data-ttu-id="96f87-121">Les occurrences du modèle « {deviceid} » dans le code HTML ou le code JavaScript que vous fournissez ici seront automatiquement remplacées par l'identificateur de l'appareil qui affiche l'annonce.</span><span class="sxs-lookup"><span data-stu-id="96f87-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="96f87-122">Il s'agit d'un moyen simple pour récupérer les identificateurs d'appareil Azure Mobile Engagement dans un service Web externe hébergé dans votre arrière-guichet.</span><span class="sxs-lookup"><span data-stu-id="96f87-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="96f87-123">Si vous souhaitez créé un affichage Web plein écran (sans utiliser les boutons par défaut Action et Quitter que nous offrons), vous pouvez utiliser les fonctions suivantes depuis le code JavaScript de votre annonce d'affichage Web :</span><span class="sxs-lookup"><span data-stu-id="96f87-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="96f87-124">effectuer l’action de l’annonce : ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="96f87-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="96f87-125">quitter l’annonce : ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="96f87-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="96f87-126">Choisissez votre action :</span><span class="sxs-lookup"><span data-stu-id="96f87-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="96f87-127">À propos des URL d'action :</span><span class="sxs-lookup"><span data-stu-id="96f87-127">About Action URLs:</span></span>
<span data-ttu-id="96f87-128">Toute URL qui peut être interprétée par le système d'exploitation d'un appareil cible peut être utilisée comme une URL d'action.</span><span class="sxs-lookup"><span data-stu-id="96f87-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="96f87-129">Toute URL dédiée pouvant être prise en charge par votre application (par exemple pour permettre à vos utilisateurs de passer à un écran spécifique) peut également être utilisée comme URL d'action.</span><span class="sxs-lookup"><span data-stu-id="96f87-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="96f87-130">Chaque occurrence du modèle {deviceid} est automatiquement remplacée par l'identificateur de l'appareil réalisant l'action.</span><span class="sxs-lookup"><span data-stu-id="96f87-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="96f87-131">Cela peut être utilisé pour récupérer facilement des identificateurs d'appareil Azure Mobile Engagement via un service Web externe hébergé dans votre arrière-guichet.</span><span class="sxs-lookup"><span data-stu-id="96f87-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="96f87-132">**Actions Android et iOS**</span><span class="sxs-lookup"><span data-stu-id="96f87-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="96f87-133">Ouvrir une page Web</span><span class="sxs-lookup"><span data-stu-id="96f87-133">Open a web page</span></span>
  * <span data-ttu-id="96f87-134">http://\[domaine-site-web\]</span><span class="sxs-lookup"><span data-stu-id="96f87-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="96f87-135">Exemple : http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="96f87-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="96f87-136">Envoyer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="96f87-136">Send an e-mail</span></span>
  * <span data-ttu-id="96f87-137">mailto:\[destinataire-e-mail\]?subject=\[objet\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="96f87-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="96f87-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="96f87-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="96f87-139">Envoyer un SMS</span><span class="sxs-lookup"><span data-stu-id="96f87-139">Send a SMS</span></span>
  * <span data-ttu-id="96f87-140">sms:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="96f87-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="96f87-141">Exemple :sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="96f87-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="96f87-142">Composer un numéro de téléphone</span><span class="sxs-lookup"><span data-stu-id="96f87-142">Dial a phone number</span></span>
  * <span data-ttu-id="96f87-143">tel:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="96f87-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="96f87-144">Exemple :tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="96f87-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="96f87-145">**Actions Android uniquement**</span><span class="sxs-lookup"><span data-stu-id="96f87-145">**Android only actions**</span></span>
  * <span data-ttu-id="96f87-146">Télécharger une application du Play Store</span><span class="sxs-lookup"><span data-stu-id="96f87-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="96f87-147">market://details?id=\[package d’application\]</span><span class="sxs-lookup"><span data-stu-id="96f87-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="96f87-148">Exemple :market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="96f87-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="96f87-149">Démarrer une recherche géolocalisée</span><span class="sxs-lookup"><span data-stu-id="96f87-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="96f87-150">geo:0,0?q=\[requête de recherche\]</span><span class="sxs-lookup"><span data-stu-id="96f87-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="96f87-151">Exemple :geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="96f87-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="96f87-152">**Actions iOS uniquement**</span><span class="sxs-lookup"><span data-stu-id="96f87-152">**iOS only actions**</span></span>
  * <span data-ttu-id="96f87-153">Télécharger une application depuis le Magasin d'applications</span><span class="sxs-lookup"><span data-stu-id="96f87-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="96f87-154">http://itunes.apple.com/[pays]/app/[nom de l’application]/id[ID de l’application]?mt=8</span><span class="sxs-lookup"><span data-stu-id="96f87-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="96f87-155">Exemple: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="96f87-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="96f87-156">Actions Windows</span><span class="sxs-lookup"><span data-stu-id="96f87-156">Windows Actions</span></span>
  * <span data-ttu-id="96f87-157">Ouvrir une page Web</span><span class="sxs-lookup"><span data-stu-id="96f87-157">Open a web page</span></span>
  * <span data-ttu-id="96f87-158">http://\[domaine-site-web\]</span><span class="sxs-lookup"><span data-stu-id="96f87-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="96f87-159">Exemple : http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="96f87-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="96f87-160">Envoyer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="96f87-160">Send an e-mail</span></span>
  * <span data-ttu-id="96f87-161">mailto:\[destinataire-e-mail\]?subject=\[objet\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="96f87-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="96f87-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="96f87-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="96f87-163">Envoyer un SMS (application Skype du Store requise)</span><span class="sxs-lookup"><span data-stu-id="96f87-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="96f87-164">sms:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="96f87-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="96f87-165">Exemple :sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="96f87-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="96f87-166">Composer un numéro de téléphone (application Skype du Store requise)</span><span class="sxs-lookup"><span data-stu-id="96f87-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="96f87-167">tel:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="96f87-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="96f87-168">Exemple :tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="96f87-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="96f87-169">Télécharger une application du Play Store</span><span class="sxs-lookup"><span data-stu-id="96f87-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="96f87-170">ms-windows-store:PDP?PFN=\[ID de package d’application\]</span><span class="sxs-lookup"><span data-stu-id="96f87-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="96f87-171">Exemple :ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="96f87-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="96f87-172">Démarrer une recherche Bing Cartes</span><span class="sxs-lookup"><span data-stu-id="96f87-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="96f87-173">bingmaps:?q=\[requête de recherche\]</span><span class="sxs-lookup"><span data-stu-id="96f87-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="96f87-174">Exemple :bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="96f87-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="96f87-175">Utiliser un modèle personnalisé</span><span class="sxs-lookup"><span data-stu-id="96f87-175">Use a custom scheme</span></span>
  * <span data-ttu-id="96f87-176">\[schéma personnalisé\]://\[paramètres du schéma personnalisé\]</span><span class="sxs-lookup"><span data-stu-id="96f87-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="96f87-177">Exemple :myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="96f87-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="96f87-178">Utiliser un package de données (application du Store pour la lecture d'extension requise)</span><span class="sxs-lookup"><span data-stu-id="96f87-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="96f87-179">\[dossier\]\[données\].\[extension\]</span><span class="sxs-lookup"><span data-stu-id="96f87-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="96f87-180">Exemple :myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="96f87-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="96f87-181">Génération d'une URL de suivi :</span><span class="sxs-lookup"><span data-stu-id="96f87-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="96f87-182">Consultez la section « Paramètres » de la <UI Documentation> pour les instructions relatives à la génération d'une URL de suivi qui permettra aux utilisateurs de télécharger une autre de vos applications.</span><span class="sxs-lookup"><span data-stu-id="96f87-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="96f87-183">Définition du texte de votre annonce</span><span class="sxs-lookup"><span data-stu-id="96f87-183">Define the texts of your announcement</span></span>
<span data-ttu-id="96f87-184">Remplissez le titre, le contenu et le texte des boutons de votre annonce.</span><span class="sxs-lookup"><span data-stu-id="96f87-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="96f87-185">Vous pouvez cibler une audience pour une future campagne suivant les commentaires Reach indiquant la façon dont les utilisateurs ont répondu à cette campagne.</span><span class="sxs-lookup"><span data-stu-id="96f87-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="96f87-186">Le ciblage de l'audience peut se baser sur les commentaires déterminant si la campagne a été envoyée par notification Push, si elle a obtenu une réponse, si elle a été activée ou quittée.</span><span class="sxs-lookup"><span data-stu-id="96f87-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="96f87-187">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96f87-187">See also</span></span>
* <span data-ttu-id="96f87-188">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="96f87-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="96f87-189">Contenu des sondages</span><span class="sxs-lookup"><span data-stu-id="96f87-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="96f87-191">Remplissez le titre, la description et le texte des boutons de votre annonce.</span><span class="sxs-lookup"><span data-stu-id="96f87-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="96f87-192">Ajoutez ensuite des questions et des choix de réponse pour ces questions.</span><span class="sxs-lookup"><span data-stu-id="96f87-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="96f87-193">Vous pouvez cibler une audience pour une future campagne suivant les commentaires Reach indiquant la façon dont les utilisateurs ont répondu à cette campagne.</span><span class="sxs-lookup"><span data-stu-id="96f87-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="96f87-194">Le ciblage de l'audience est déterminé selon que la campagne est issue d'une transmission de type push, qu'elle a obtenu une réponse, qu'elle a été activée ou quittée.</span><span class="sxs-lookup"><span data-stu-id="96f87-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="96f87-195">Le ciblage de l'audience peut également se baser sur les commentaires de réponse du sondage pour lequel la question à choix multiple est utilisée comme critère.</span><span class="sxs-lookup"><span data-stu-id="96f87-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="96f87-196">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96f87-196">See also</span></span>
* <span data-ttu-id="96f87-197">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="96f87-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="96f87-198">Contenu des Push de données</span><span class="sxs-lookup"><span data-stu-id="96f87-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="96f87-200">Choisissez le type de vos données :</span><span class="sxs-lookup"><span data-stu-id="96f87-200">Choose the type of your data:</span></span>
* <span data-ttu-id="96f87-201">Texte</span><span class="sxs-lookup"><span data-stu-id="96f87-201">Text</span></span>
* <span data-ttu-id="96f87-202">Données binaires</span><span class="sxs-lookup"><span data-stu-id="96f87-202">Binary data</span></span>
* <span data-ttu-id="96f87-203">Données Base64</span><span class="sxs-lookup"><span data-stu-id="96f87-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="96f87-204">Définition du contenu de vos données</span><span class="sxs-lookup"><span data-stu-id="96f87-204">Define the content of your data</span></span>
* <span data-ttu-id="96f87-205">Si vous sélectionnez une transmission de type push des données de texte, copiez et collez le texte dans la boîte « contenu ».</span><span class="sxs-lookup"><span data-stu-id="96f87-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="96f87-206">Si vous sélectionnez une transmission de type push de données binaires ou base64, utilisez le bouton « Télécharger votre fichier » pour télécharger votre fichier.</span><span class="sxs-lookup"><span data-stu-id="96f87-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="96f87-207">Vous pouvez cibler une audience pour une future campagne suivant les commentaires Reach indiquant la façon dont les utilisateurs ont répondu à cette campagne.</span><span class="sxs-lookup"><span data-stu-id="96f87-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="96f87-208">Le ciblage de l'audience est déterminé selon que la campagne est issue d'une transmission de type push, qu'elle a obtenu une réponse, qu'elle a été activée ou quittée.</span><span class="sxs-lookup"><span data-stu-id="96f87-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="96f87-209">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96f87-209">See also</span></span>
* <span data-ttu-id="96f87-210">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="96f87-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="96f87-211">Contenu des vignettes (Windows Phone uniquement)</span><span class="sxs-lookup"><span data-stu-id="96f87-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="96f87-213">Définition du contenu de vos vignettes</span><span class="sxs-lookup"><span data-stu-id="96f87-213">Define the content of your tile</span></span>
<span data-ttu-id="96f87-214">La charge utile de la vignette correspond au texte qui s'affichera dans la vignette de votre application sur les appareils Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="96f87-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="96f87-215">Un Push de vignette est la version du service de notifications Push de Microsoft (MPNS) d'un Push natif pour Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="96f87-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="96f87-216">Ce type de Push de vignette est le seul type de push qui n'a pas de réponse. L'audience des futures campagnes ne peut donc pas être déterminée en fonction des résultats d'une campagne de Push de vignette.</span><span class="sxs-lookup"><span data-stu-id="96f87-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="96f87-217">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96f87-217">See also</span></span>
* <span data-ttu-id="96f87-218">[Documentation sur les API - API Reach - Push natif][Link 4]</span><span class="sxs-lookup"><span data-stu-id="96f87-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

