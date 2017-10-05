---
title: "Problème de configuration de l’authentification unique avec mot de passe pour une application non issue de la galerie | Microsoft Docs"
description: "Comprendre les problèmes courants auxquels les utilisateurs sont confrontés lors de la configuration d’une authentification unique avec mot de passe pour les applications qui ne figurent pas dans la galerie d’applications Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="662b7-103">Problème de configuration de l’authentification unique avec mot de passe pour une application non issue de la galerie</span><span class="sxs-lookup"><span data-stu-id="662b7-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="662b7-104">Cet article vous aide à comprendre les problèmes courants auxquels les utilisateurs sont confrontés lors de la configuration d’une **authentification unique avec mot de passe** pour une application non issue de la galerie.</span><span class="sxs-lookup"><span data-stu-id="662b7-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="662b7-105">Comment capturer les champs de connexion d’une application</span><span class="sxs-lookup"><span data-stu-id="662b7-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="662b7-106">La capture des champs de connexion est uniquement prise en charge pour les pages de connexion HTML et **n’est pas prise en charge pour les pages de connexion non standard** comme celles qui utilisent Flash ou d’autres technologies non HTML.</span><span class="sxs-lookup"><span data-stu-id="662b7-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="662b7-107">Deux options s’offrent à vous pour capturer des champs de connexion dans vos applications personnalisées :</span><span class="sxs-lookup"><span data-stu-id="662b7-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="662b7-108">La capture de champs de connexion automatique</span><span class="sxs-lookup"><span data-stu-id="662b7-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="662b7-109">La capture de champs de connexion manuelle</span><span class="sxs-lookup"><span data-stu-id="662b7-109">Manual sign-in field capture</span></span>

<span data-ttu-id="662b7-110">La **capture de champs de connexion automatique** fonctionne avec la plupart des pages de connexion HTML, si celles-ci utilisent des **ID DIV connus pour les champs de saisie du nom d’utilisateur et du mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="662b7-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="662b7-111">Voici comment se déroule ce processus : le code HTML de la page est récupéré pour rechercher des ID DIV qui répondent à certains critères, puis ces métadonnées sont enregistrées pour cette application de façon que nous puissions y réutiliser les mots de passe plus tard.</span><span class="sxs-lookup"><span data-stu-id="662b7-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="662b7-112">La **capture de champs de connexion manuelle** peut être utilisée quand le fournisseur **de l’application n’a pas ajouté de libellé** aux champs de saisie utilisés pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="662b7-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="662b7-113">La capture de champs de connexion manuelle peut également être utile lorsque le **fournisseur affiche plusieurs champs** qui ne peuvent pas être détectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="662b7-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="662b7-114">Azure AD peut stocker les données de tous les champs de la page de connexion, sous réserve que vous nous donniez l’emplacement de chacun sur la page.</span><span class="sxs-lookup"><span data-stu-id="662b7-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="662b7-115">En règle générale, **si la capture de champs de connexion automatique ne fonctionne pas, nous vous suggérons toujours d’essayer l’option manuelle.**</span><span class="sxs-lookup"><span data-stu-id="662b7-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="662b7-116">Comment capturer automatiquement les champs de connexion d’une application</span><span class="sxs-lookup"><span data-stu-id="662b7-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="662b7-117">Pour configurer **l’authentification unique avec mot de passe** d’une application à l’aide de la **capture de champs de connexion automatique**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="662b7-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="662b7-118">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’administrateur général** ou en tant que **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="662b7-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="662b7-119">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="662b7-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="662b7-120">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="662b7-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="662b7-121">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="662b7-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="662b7-122">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="662b7-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="662b7-123">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="662b7-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="662b7-124">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="662b7-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="662b7-125">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="662b7-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="662b7-126">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="662b7-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="662b7-127">Entrez **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="662b7-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="662b7-128">Il s’agit de l’URL où les utilisateurs entrent leur nom d’utilisateur et mot de passe pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="662b7-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="662b7-129">**Vérifiez que les champs de connexion sont visibles dans l’URL que vous fournissez**.</span><span class="sxs-lookup"><span data-stu-id="662b7-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="662b7-130">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="662b7-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="662b7-131">Une fois cela effectué, nous décomposons automatiquement cette URL pour afficher les zones de saisie du mot de passe et du nom d’utilisateur. Vous pouvez ensuite utiliser Azure AD pour transmettre en toute sécurité les mots de passe à cette application à l’aide de l’extension de navigateur du volet accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="662b7-132">Comment capturer manuellement les champs de connexion d’une application</span><span class="sxs-lookup"><span data-stu-id="662b7-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="662b7-133">Pour capturer manuellement les champs de connexion, l’extension de navigateur du volet d’accès doit être installée et **ne doit pas s’exécuter en mode inPrivate, incognito ou privé.**</span><span class="sxs-lookup"><span data-stu-id="662b7-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="662b7-134">Pour installer l’extension de navigateur, suivez les étapes de la section [Comment installer l’extension de navigateur du volet d’accès](#i-cannot-manually-detect-sign-in-fields-for-my-application).</span><span class="sxs-lookup"><span data-stu-id="662b7-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="662b7-135">Pour configurer **l’authentification unique avec mot de passe** d’une application à l’aide de la **capture de champs de connexion manuelle**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="662b7-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="662b7-136">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’administrateur général** ou en tant que **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="662b7-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="662b7-137">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="662b7-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="662b7-138">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="662b7-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="662b7-139">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="662b7-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="662b7-140">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="662b7-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="662b7-141">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="662b7-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="662b7-142">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="662b7-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="662b7-143">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="662b7-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="662b7-144">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="662b7-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="662b7-145">Entrez **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="662b7-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="662b7-146">Il s’agit de l’URL où les utilisateurs entrent leur nom d’utilisateur et mot de passe pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="662b7-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="662b7-147">**Vérifiez que les champs de connexion sont visibles dans l’URL que vous fournissez**.</span><span class="sxs-lookup"><span data-stu-id="662b7-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="662b7-148">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="662b7-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="662b7-149">Une fois cela effectué, nous décomposons automatiquement cette URL pour afficher les zones de saisie du mot de passe et du nom d’utilisateur. Vous pouvez ensuite utiliser Azure AD pour transmettre en toute sécurité les mots de passe à cette application à l’aide de l’extension de navigateur du volet accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="662b7-150">Si l’opération échoue, vous pouvez **modifier le mode de connexion pour qu’il utilise la capture de champs de connexion manuelle** en continuant à l’étape 12.</span><span class="sxs-lookup"><span data-stu-id="662b7-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="662b7-151">Cliquez sur **Configurer les paramètres d’authentification unique par mot de passe de** &lt;nom de l’application&gt;.</span><span class="sxs-lookup"><span data-stu-id="662b7-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="662b7-152">Sélectionnez l’option de configuration **Détecter manuellement les champs de connexion**.</span><span class="sxs-lookup"><span data-stu-id="662b7-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="662b7-153">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="662b7-153">Click **Ok**.</span></span>

15. <span data-ttu-id="662b7-154">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="662b7-154">Click **Save**.</span></span>

16. <span data-ttu-id="662b7-155">Suivez les instructions à l’écran pour utiliser le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="662b7-156">Une erreur « Nous n’avons trouvé aucun champ de connexion à cette URL. » s’affiche</span><span class="sxs-lookup"><span data-stu-id="662b7-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="662b7-157">Vous obtenez cette erreur en cas d’échec de la détection automatique des champs de connexion.</span><span class="sxs-lookup"><span data-stu-id="662b7-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="662b7-158">Pour résoudre ce problème, essayez d’utiliser la détection manuelle des champs de connexion en suivant les étapes de la section [Comment capturer manuellement les champs de connexion d’une application](#how-to-manually-capture-sign-in-fields-for-an-application).</span><span class="sxs-lookup"><span data-stu-id="662b7-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="662b7-159">Une erreur « Impossible d’enregistrer la configuration de l’authentification unique » s’affiche</span><span class="sxs-lookup"><span data-stu-id="662b7-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="662b7-160">Bien que cela soit rare, il peut arriver que la mise à jour de la configuration de l’authentification unique échoue.</span><span class="sxs-lookup"><span data-stu-id="662b7-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="662b7-161">Pour résoudre ce problème, essayez d’enregistrer à nouveau la configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="662b7-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="662b7-162">Si le problème persiste, ouvrez une demande de support et fournissez les informations collectées dans les sections [Comment afficher les détails d’une notification du portail](#i-cannot-manually-detect-sign-in-fields-for-my-application) et [Comment obtenir de l’aide en envoyant les détails de la notification à un ingénieur du support technique](#how-to-get-help-by-sending-notification-details-to-a-support-engineer).</span><span class="sxs-lookup"><span data-stu-id="662b7-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="662b7-163">Impossible de détecter manuellement les champs de connexion de mon application</span><span class="sxs-lookup"><span data-stu-id="662b7-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="662b7-164">Voici quelques-uns des comportements que vous pouvez observer lorsque la détection manuelle ne fonctionne pas :</span><span class="sxs-lookup"><span data-stu-id="662b7-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="662b7-165">Le processus de capture manuelle semble fonctionner, mais les champs capturés ne sont pas corrects.</span><span class="sxs-lookup"><span data-stu-id="662b7-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="662b7-166">Les champs corrects ne sont pas mis en surbrillance lors de l’exécution du processus de capture.</span><span class="sxs-lookup"><span data-stu-id="662b7-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="662b7-167">Le processus de capture me redirige comme prévu vers la page de connexion de l’application, mais rien ne se produit.</span><span class="sxs-lookup"><span data-stu-id="662b7-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="662b7-168">La capture manuelle semble fonctionner, mais l’authentification unique ne se produit pas lorsque mes utilisateurs accèdent à l’application à partir du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="662b7-169">Si vous rencontrez l’un de ces problèmes, vérifiez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="662b7-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="662b7-170">Assurez-vous que la dernière version de l’extension de navigateur du volet d’accès est **installée** et **activée** en suivant les étapes de la section [Comment installer l’extension de navigateur du volet d’accès](#how-to-install-the-access-panel-browser-extension).</span><span class="sxs-lookup"><span data-stu-id="662b7-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="662b7-171">Assurez-vous que vous ne tentez pas d’exécuter le processus de capture alors que votre navigateur est en **mode incognito, inPrivate ou privé**.</span><span class="sxs-lookup"><span data-stu-id="662b7-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="662b7-172">Ces modes ne prennent pas en charge l’extension du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="662b7-173">Assurez-vous que vos utilisateurs ne tentent pas de se connecter à l’application à partir du volet d’accès alors qu’ils sont en **mode incognito, inPrivate ou privé**.</span><span class="sxs-lookup"><span data-stu-id="662b7-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="662b7-174">Ces modes ne prennent pas en charge l’extension du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="662b7-175">Tentez une nouvelle fois d’exécuter le processus de capture manuelle en veillant à ce que les marqueurs rouges soient sur les champs appropriés.</span><span class="sxs-lookup"><span data-stu-id="662b7-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="662b7-176">Si le processus de capture manuelle semble bloqué ou si la page de connexion ne réagit pas (cas 3 ci-dessus), tentez une nouvelle fois d’exécuter le processus de capture manuelle.</span><span class="sxs-lookup"><span data-stu-id="662b7-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="662b7-177">Mais cette fois, à la fin du processus, appuyez sur le bouton **F12** pour ouvrir la console de développement de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="662b7-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="662b7-178">Ouvrez la **console** et saisissez **window.location=”&lt;entrez l’url de connexion que vous avez spécifiée lors de la configuration de l’application&gt;”**, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="662b7-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="662b7-179">Cette manipulation permet de forcer une redirection de page qui termine le processus de capture et stocke les fichiers qui ont été capturés.</span><span class="sxs-lookup"><span data-stu-id="662b7-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="662b7-180">Si aucune de ces approches ne fonctionne pour vous, nous pouvons vous aider.</span><span class="sxs-lookup"><span data-stu-id="662b7-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="662b7-181">Ouvrez une demande de support et fournissez des informations sur les méthodes utilisées pour résoudre le problème, ainsi que les informations collectées dans les sections [Comment afficher les détails d’une notification du portail](#i-cannot-manually-detect-sign-in-fields-for-my-application) et [Comment obtenir de l’aide en envoyant les détails de la notification à un ingénieur du support technique](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="662b7-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="662b7-182">Comment installer l’extension de navigateur du volet d’accès</span><span class="sxs-lookup"><span data-stu-id="662b7-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="662b7-183">Pour installer l’extension de navigateur du volet d’accès, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="662b7-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="662b7-184">Ouvrez le [volet d’accès](https://myapps.microsoft.com) dans l’un des navigateurs pris en charge et connectez-vous en tant **qu’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="662b7-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="662b7-185">Cliquez sur une **application avec authentification unique par mot de passe** dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="662b7-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="662b7-186">Dans l’invite vous demandant d’installer le logiciel, sélectionnez **Installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="662b7-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="662b7-187">Vous êtes redirigé vers le lien de téléchargement selon votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="662b7-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="662b7-188">**Ajoutez** l’extension à votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="662b7-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="662b7-189">Si votre navigateur vous le demande, sélectionnez l’option **Activer** ou **Autoriser** pour l’extension.</span><span class="sxs-lookup"><span data-stu-id="662b7-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="662b7-190">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="662b7-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="662b7-191">Connectez-vous au volet d’accès et essayez de **démarrer** vos applications à authentification unique avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="662b7-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="662b7-192">Vous pouvez également télécharger l’extension pour Chrome et Firefox à partir des liens directs ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="662b7-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="662b7-193">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="662b7-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="662b7-194">Extension du volet d’accès pour Firefox</span><span class="sxs-lookup"><span data-stu-id="662b7-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="662b7-195">Comment afficher les détails d’une notification du portail</span><span class="sxs-lookup"><span data-stu-id="662b7-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="662b7-196">Vous pouvez afficher les détails d’une notification provenant du portail en suivant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="662b7-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="662b7-197">Cliquez sur l’icône **Notifications** (cloche) dans le coin supérieur droit du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="662b7-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="662b7-198">Sélectionnez n’importe quelle notification avec l’état **Erreur**, signalée par un (!) rouge.</span><span class="sxs-lookup"><span data-stu-id="662b7-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="662b7-199">!NOTE] Vous ne pouvez pas cliquer sur les notifications affichant l’état **Réussi** ou **En cours**.</span><span class="sxs-lookup"><span data-stu-id="662b7-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="662b7-200">Le volet **Détails de la notification** apparaît.</span><span class="sxs-lookup"><span data-stu-id="662b7-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="662b7-201">Utilisez ces informations pour en savoir plus sur le problème.</span><span class="sxs-lookup"><span data-stu-id="662b7-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="662b7-202">Si vous avez encore besoin d’aide, vous pouvez également partager ces informations avec un ingénieur du support technique ou du groupe de produits qui vous assistera pour résoudre votre problème.</span><span class="sxs-lookup"><span data-stu-id="662b7-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="662b7-203">Cliquez sur **l’icône** de **copie** à droite de la zone de texte **Erreur de copie** pour copier tous les détails de la notification afin de les partager avec un ingénieur du support technique ou du groupe de produits.</span><span class="sxs-lookup"><span data-stu-id="662b7-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="662b7-204">Comment obtenir de l’aide en envoyant les détails de la notification à un ingénieur du support technique</span><span class="sxs-lookup"><span data-stu-id="662b7-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="662b7-205">Il est très important que vous partagiez **tous les détails ci-dessous** avec un ingénieur du support technique si vous avez besoin d’aide, car celui-ci peut vous permettre de résoudre rapidement le problème.</span><span class="sxs-lookup"><span data-stu-id="662b7-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="662b7-206">Vous pouvez facilement le faire en **prenant une capture d’écran** ou en cliquant sur **l’icône d’erreur de copie** située à droite de la zone de texte **Erreur de copie**.</span><span class="sxs-lookup"><span data-stu-id="662b7-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="662b7-207">Explication des détails de la notification</span><span class="sxs-lookup"><span data-stu-id="662b7-207">Notification Details Explained</span></span>

<span data-ttu-id="662b7-208">Vous trouverez ci-dessous plus d’informations sur la signification de chaque notification ainsi que des exemples de chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="662b7-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="662b7-209">Éléments essentiels de la notification</span><span class="sxs-lookup"><span data-stu-id="662b7-209">Essential Notification Items</span></span>

-   <span data-ttu-id="662b7-210">**Titre** : titre descriptif de la notification</span><span class="sxs-lookup"><span data-stu-id="662b7-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="662b7-211">Exemple : **Paramètres de proxy d’application**</span><span class="sxs-lookup"><span data-stu-id="662b7-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="662b7-212">**Description** : description de ce qui s’est produit suite à l’opération</span><span class="sxs-lookup"><span data-stu-id="662b7-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="662b7-213">Exemple : **L’URL interne entrée est déjà utilisée par une autre application**</span><span class="sxs-lookup"><span data-stu-id="662b7-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="662b7-214">**ID de notification** : ID unique de la notification</span><span class="sxs-lookup"><span data-stu-id="662b7-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="662b7-215">Exemple : **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="662b7-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="662b7-216">**ID de demande client** : ID de la demande spécifique faite par votre navigateur</span><span class="sxs-lookup"><span data-stu-id="662b7-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="662b7-217">Exemple : **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="662b7-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="662b7-218">**Horodatage UTC** : horodatage de l’affichage de la notification, au format UTC</span><span class="sxs-lookup"><span data-stu-id="662b7-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="662b7-219">Exemple : **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="662b7-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="662b7-220">**ID de transaction interne** : ID interne nous permettant de rechercher l’erreur dans nos systèmes</span><span class="sxs-lookup"><span data-stu-id="662b7-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="662b7-221">Exemple : **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="662b7-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="662b7-222">**UPN** : utilisateur qui a effectué l’opération</span><span class="sxs-lookup"><span data-stu-id="662b7-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="662b7-223">Exemple : **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="662b7-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="662b7-224">**ID de locataire** : ID unique du locataire dont l’utilisateur qui a effectué l’opération était membre</span><span class="sxs-lookup"><span data-stu-id="662b7-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="662b7-225">Exemple : **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="662b7-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="662b7-226">**ID de l’objet utilisateur** : ID unique de l’utilisateur qui a effectué l’opération</span><span class="sxs-lookup"><span data-stu-id="662b7-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="662b7-227">Exemple : **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="662b7-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="662b7-228">Éléments détaillés de la notification</span><span class="sxs-lookup"><span data-stu-id="662b7-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="662b7-229">**Nom d’affichage** : **(peut être vide)** nom d’affichage plus détaillé de l’erreur</span><span class="sxs-lookup"><span data-stu-id="662b7-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="662b7-230">Exemple *: **Paramètres de proxy d’application**</span><span class="sxs-lookup"><span data-stu-id="662b7-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="662b7-231">**État** : état spécifique de la notification</span><span class="sxs-lookup"><span data-stu-id="662b7-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="662b7-232">Exemple *: **Échec**</span><span class="sxs-lookup"><span data-stu-id="662b7-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="662b7-233">**ID de l’objet** : **(peut être vide)** ID de l’objet sur lequel l’opération a été effectuée</span><span class="sxs-lookup"><span data-stu-id="662b7-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="662b7-234">Exemple : **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="662b7-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="662b7-235">**Détails** : description détaillée de ce qui s’est produit suite à l’opération</span><span class="sxs-lookup"><span data-stu-id="662b7-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="662b7-236">Exemple : **l’URL interne 'http://bing.com/' n’est pas valide car elle est déjà en cours d’utilisation**</span><span class="sxs-lookup"><span data-stu-id="662b7-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="662b7-237">**Erreur de copie** : cliquez sur **l’icône de copie** à droite de la zone de texte **Erreur de copie** pour copier tous les détails de la notification afin de les partager avec un ingénieur du support technique ou du groupe de produits</span><span class="sxs-lookup"><span data-stu-id="662b7-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="662b7-238">Exemple : ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="662b7-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="662b7-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="662b7-239">Next steps</span></span>
[<span data-ttu-id="662b7-240">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="662b7-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

