---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - atteindre le contenu"
description: "Découvrez comment toomanage un contenu unique hello hello différents types de notifications push campagnes dans Azure Mobile Engagement"
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
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="6e5e8-103">Comment toomanage hello contenu unique de hello différents types de campagnes de notification push</span><span class="sxs-lookup"><span data-stu-id="6e5e8-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="6e5e8-104">Vous pouvez utiliser la section de contenu hello d’un nouveau couvertures campagne toomodify hello de contenu des annonces, sondages, exécute un push de données et des vignettes (Windows Phone uniquement).</span><span class="sxs-lookup"><span data-stu-id="6e5e8-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="6e5e8-105">le paramètre de contenu Hello de campagnes Push est type toohello spécifique de campagne.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="6e5e8-106">Types de contenu :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-106">Content types:</span></span>
* <span data-ttu-id="6e5e8-107">Annonces</span><span class="sxs-lookup"><span data-stu-id="6e5e8-107">Announcements</span></span>
* <span data-ttu-id="6e5e8-108">Sondages</span><span class="sxs-lookup"><span data-stu-id="6e5e8-108">Polls</span></span>
* <span data-ttu-id="6e5e8-109">Push de données</span><span class="sxs-lookup"><span data-stu-id="6e5e8-109">Data pushes</span></span>
* <span data-ttu-id="6e5e8-110">Vignettes (Windows Phone uniquement)</span><span class="sxs-lookup"><span data-stu-id="6e5e8-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="6e5e8-111">Contenu des annonces</span><span class="sxs-lookup"><span data-stu-id="6e5e8-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="6e5e8-113">Choisissez le type hello de l’annonce :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="6e5e8-114">Notification uniquement : il s’agit d’une simple notification standard.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="6e5e8-115">Ce qui signifie que si un utilisateur clique dessus, aucun affichage supplémentaire ne s’affiche, mais seulement l’action hello associée tooit se produira.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="6e5e8-116">Annonce de texte : il est une notification qui engage hello utilisateur toohave examiner une vue de texte.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="6e5e8-117">Annonce de Web : il est une notification qui engage hello utilisateur toohave examiner un affichage web.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="6e5e8-118">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6e5e8-118">See also</span></span>
* <span data-ttu-id="6e5e8-119">[Reach - Procédures - Annonces][Link 3]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="6e5e8-120">À propos des annonces d'affichage Web :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-120">About Web View Announcements:</span></span>
<span data-ttu-id="6e5e8-121">Occurrences de modèle hello « {deviceid} » dans le code de hello HTML ou le code JavaScript que vous fournissez ici seront automatiquement remplacées par identificateur hello du périphérique hello affichant l’annonce de type hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="6e5e8-122">Il s’agit d’un identificateurs d’appareil Azure Mobile Engagement tooretrieve facilement dans un externe de votre arrière-guichet de service web.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="6e5e8-123">Si vous voulez toocreate un plein écran affichage web (sans hello Action et quitter boutons que nous fournissons) vous pouvez utiliser hello suivant des fonctions à partir du code JavaScript de l’annonce de votre vue de web :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="6e5e8-124">effectuer l’action d’annonce hello : ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="6e5e8-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="6e5e8-125">sortie de l’annonce de type hello : ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="6e5e8-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="6e5e8-126">Choisissez votre action :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="6e5e8-127">À propos des URL d'action :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-127">About Action URLs:</span></span>
<span data-ttu-id="6e5e8-128">Toute URL qui peut être interprétée par le système d'exploitation d'un appareil cible peut être utilisée comme une URL d'action.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="6e5e8-129">Toute URL dédiée par votre application peut prise en charge (par exemple, les utilisateurs toomake raccourcis tooa écran en particulier) peut également servir comme une URL d’action.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="6e5e8-130">Chaque occurrence de hello {deviceid} pattern est automatiquement remplacé par identificateur hello du périphérique hello action de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="6e5e8-131">Cela peut être des identificateurs d’appareil Azure Mobile Engagement tooeasily utilisé récupérer via un service web externe de votre arrière-guichet.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="6e5e8-132">**Actions Android et iOS**</span><span class="sxs-lookup"><span data-stu-id="6e5e8-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="6e5e8-133">Ouvrir une page Web</span><span class="sxs-lookup"><span data-stu-id="6e5e8-133">Open a web page</span></span>
  * <span data-ttu-id="6e5e8-134">http://\[domaine-site-web\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="6e5e8-135">Exemple : http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="6e5e8-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="6e5e8-136">Envoyer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="6e5e8-136">Send an e-mail</span></span>
  * <span data-ttu-id="6e5e8-137">mailto:\[destinataire-e-mail\]?subject=\[objet\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="6e5e8-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="6e5e8-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="6e5e8-139">Envoyer un SMS</span><span class="sxs-lookup"><span data-stu-id="6e5e8-139">Send a SMS</span></span>
  * <span data-ttu-id="6e5e8-140">sms:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="6e5e8-141">Exemple :sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="6e5e8-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="6e5e8-142">Composer un numéro de téléphone</span><span class="sxs-lookup"><span data-stu-id="6e5e8-142">Dial a phone number</span></span>
  * <span data-ttu-id="6e5e8-143">tel:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="6e5e8-144">Exemple :tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="6e5e8-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="6e5e8-145">**Actions Android uniquement**</span><span class="sxs-lookup"><span data-stu-id="6e5e8-145">**Android only actions**</span></span>
  * <span data-ttu-id="6e5e8-146">Télécharger une application sur hello Play Store</span><span class="sxs-lookup"><span data-stu-id="6e5e8-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="6e5e8-147">market://details?id=\[package d’application\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="6e5e8-148">Exemple :market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="6e5e8-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="6e5e8-149">Démarrer une recherche géolocalisée</span><span class="sxs-lookup"><span data-stu-id="6e5e8-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="6e5e8-150">geo:0,0?q=\[requête de recherche\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="6e5e8-151">Exemple :geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="6e5e8-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="6e5e8-152">**Actions iOS uniquement**</span><span class="sxs-lookup"><span data-stu-id="6e5e8-152">**iOS only actions**</span></span>
  * <span data-ttu-id="6e5e8-153">Télécharger une application sur hello App Store</span><span class="sxs-lookup"><span data-stu-id="6e5e8-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="6e5e8-154">http://itunes.apple.com/[pays]/app/[nom de l’application]/id[ID de l’application]?mt=8</span><span class="sxs-lookup"><span data-stu-id="6e5e8-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="6e5e8-155">Exemple: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="6e5e8-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="6e5e8-156">Actions Windows</span><span class="sxs-lookup"><span data-stu-id="6e5e8-156">Windows Actions</span></span>
  * <span data-ttu-id="6e5e8-157">Ouvrir une page Web</span><span class="sxs-lookup"><span data-stu-id="6e5e8-157">Open a web page</span></span>
  * <span data-ttu-id="6e5e8-158">http://\[domaine-site-web\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="6e5e8-159">Exemple : http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="6e5e8-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="6e5e8-160">Envoyer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="6e5e8-160">Send an e-mail</span></span>
  * <span data-ttu-id="6e5e8-161">mailto:\[destinataire-e-mail\]?subject=\[objet\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="6e5e8-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="6e5e8-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="6e5e8-163">Envoyer un SMS (application Skype du Store requise)</span><span class="sxs-lookup"><span data-stu-id="6e5e8-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="6e5e8-164">sms:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="6e5e8-165">Exemple :sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="6e5e8-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="6e5e8-166">Composer un numéro de téléphone (application Skype du Store requise)</span><span class="sxs-lookup"><span data-stu-id="6e5e8-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="6e5e8-167">tel:\[numéro-téléphone\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="6e5e8-168">Exemple :tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="6e5e8-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="6e5e8-169">Télécharger une application sur hello Play Store</span><span class="sxs-lookup"><span data-stu-id="6e5e8-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="6e5e8-170">ms-windows-store:PDP?PFN=\[ID de package d’application\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="6e5e8-171">Exemple :ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="6e5e8-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="6e5e8-172">Démarrer une recherche Bing Cartes</span><span class="sxs-lookup"><span data-stu-id="6e5e8-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="6e5e8-173">bingmaps:?q=\[requête de recherche\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="6e5e8-174">Exemple :bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="6e5e8-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="6e5e8-175">Utiliser un modèle personnalisé</span><span class="sxs-lookup"><span data-stu-id="6e5e8-175">Use a custom scheme</span></span>
  * <span data-ttu-id="6e5e8-176">\[schéma personnalisé\]://\[paramètres du schéma personnalisé\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="6e5e8-177">Exemple :myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="6e5e8-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="6e5e8-178">Utiliser un package de données (application du Store pour la lecture d'extension requise)</span><span class="sxs-lookup"><span data-stu-id="6e5e8-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="6e5e8-179">\[dossier\]\[données\].\[extension\]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="6e5e8-180">Exemple :myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="6e5e8-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="6e5e8-181">Génération d'une URL de suivi :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="6e5e8-182">Consultez hello la section « Paramètres » de hello <UI Documentation> pour obtenir des instructions sur la création d’une URL de suivi qui permettront de toodownload des utilisateurs de vos autres applications.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="6e5e8-183">Définir les textes hello de l’annonce</span><span class="sxs-lookup"><span data-stu-id="6e5e8-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="6e5e8-184">Renseignez le titre de hello, le contenu et les textes de bouton de l’annonce.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="6e5e8-185">Vous pouvez cibler un public d’une campagne de futures en fonction des commentaires de la portée de la façon dont les utilisateurs ont répondu toothis campagne hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="6e5e8-186">Ciblage de l’audience peut être basé sur les commentaires hello d’indique si cette campagne a été simplement envoyée, réponse, actionnés ou quittés.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="6e5e8-187">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6e5e8-187">See also</span></span>
* <span data-ttu-id="6e5e8-188">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="6e5e8-189">Contenu des sondages</span><span class="sxs-lookup"><span data-stu-id="6e5e8-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="6e5e8-191">Renseignez hello titre, description et les textes de bouton de l’annonce.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="6e5e8-192">Ajoutez ensuite des questions et choix pour les questions de tooyour réponses hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="6e5e8-193">Vous pouvez cibler un public d’une campagne de futures en fonction des commentaires de la portée de la façon dont les utilisateurs ont répondu toothis campagne hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="6e5e8-194">Le ciblage de l'audience est déterminé selon que la campagne est issue d'une transmission de type push, qu'elle a obtenu une réponse, qu'elle a été activée ou quittée.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="6e5e8-195">Ciblage de l’audience peut également être basé sur les commentaires de réponse au sondage, où les choix de questions et réponses hello sont utilisés comme critères.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="6e5e8-196">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6e5e8-196">See also</span></span>
* <span data-ttu-id="6e5e8-197">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="6e5e8-198">Contenu des Push de données</span><span class="sxs-lookup"><span data-stu-id="6e5e8-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="6e5e8-200">Choisissez le type hello de vos données :</span><span class="sxs-lookup"><span data-stu-id="6e5e8-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="6e5e8-201">Texte</span><span class="sxs-lookup"><span data-stu-id="6e5e8-201">Text</span></span>
* <span data-ttu-id="6e5e8-202">Données binaires</span><span class="sxs-lookup"><span data-stu-id="6e5e8-202">Binary data</span></span>
* <span data-ttu-id="6e5e8-203">Données Base64</span><span class="sxs-lookup"><span data-stu-id="6e5e8-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="6e5e8-204">Définir le contenu de hello de vos données</span><span class="sxs-lookup"><span data-stu-id="6e5e8-204">Define hello content of your data</span></span>
* <span data-ttu-id="6e5e8-205">Si vous avez sélectionné des données de texte toopush, copiez et collez le texte hello dans la zone « contenu » de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="6e5e8-206">Si vous avez sélectionné toopush données binaire ou en base 64, utilisez tooupload de bouton « Télécharger votre fichier » hello votre fichier.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="6e5e8-207">Vous pouvez cibler un public d’une campagne de futures en fonction des commentaires de la portée de la façon dont les utilisateurs ont répondu toothis campagne hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="6e5e8-208">Le ciblage de l'audience est déterminé selon que la campagne est issue d'une transmission de type push, qu'elle a obtenu une réponse, qu'elle a été activée ou quittée.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="6e5e8-209">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6e5e8-209">See also</span></span>
* <span data-ttu-id="6e5e8-210">[Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="6e5e8-211">Contenu des vignettes (Windows Phone uniquement)</span><span class="sxs-lookup"><span data-stu-id="6e5e8-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="6e5e8-213">Définir le contenu de votre vignette hello</span><span class="sxs-lookup"><span data-stu-id="6e5e8-213">Define hello content of your tile</span></span>
<span data-ttu-id="6e5e8-214">charge utile de vignette Hello est hello toobe de texte affichée dans la mosaïque hello de votre application sur les appareils Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="6e5e8-215">Un push de la vignette est version du Service de Notification Push Microsoft (MPNS) hello d’un push natif pour Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="6e5e8-216">Hello vignette push type est hello uniquement par émission de données qui n’a pas de réponse et donc audience hello de futures campagnes ne peut pas être généré sur les résultats d’une campagne de push de vignette hello.</span><span class="sxs-lookup"><span data-stu-id="6e5e8-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="6e5e8-217">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6e5e8-217">See also</span></span>
* <span data-ttu-id="6e5e8-218">[Documentation sur les API - API Reach - Push natif][Link 4]</span><span class="sxs-lookup"><span data-stu-id="6e5e8-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

