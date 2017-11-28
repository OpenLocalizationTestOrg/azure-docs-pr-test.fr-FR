---
title: "aaaProblem configuration de mot de passe l’authentification unique pour une application non-galerie | Documents Microsoft"
description: "Comprendre le cadran de personnes hello courantes des problèmes lors de la configuration de mot de passe Single Sign-on pour les applications non-galerie personnalisées qui ne sont pas répertoriées dans hello Galerie d’applications Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="07b89-103">Problème de configuration de l’authentification unique avec mot de passe pour une application non issue de la galerie</span><span class="sxs-lookup"><span data-stu-id="07b89-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="07b89-104">Cet article vous a-t-il face de personnes toounderstand hello courantes des problèmes lors de la configuration **mot de passe l’authentification unique sur** avec une application non-galerie.</span><span class="sxs-lookup"><span data-stu-id="07b89-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="07b89-105">Comment se connecter toocapture dans des champs pour une application</span><span class="sxs-lookup"><span data-stu-id="07b89-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="07b89-106">La capture des champs de connexion est uniquement prise en charge pour les pages de connexion HTML et **n’est pas prise en charge pour les pages de connexion non standard** comme celles qui utilisent Flash ou d’autres technologies non HTML.</span><span class="sxs-lookup"><span data-stu-id="07b89-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="07b89-107">Deux options s’offrent à vous pour capturer des champs de connexion dans vos applications personnalisées :</span><span class="sxs-lookup"><span data-stu-id="07b89-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="07b89-108">La capture de champs de connexion automatique</span><span class="sxs-lookup"><span data-stu-id="07b89-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="07b89-109">La capture de champs de connexion manuelle</span><span class="sxs-lookup"><span data-stu-id="07b89-109">Manual sign-in field capture</span></span>

<span data-ttu-id="07b89-110">**Capture de champ de connexion automatique** fonctionne bien avec la plupart des compatible HTML pages de connexion, s’ils utilisent **ID DIV connus pour le nom d’utilisateur hello et un mot de passe d’entrée** champ.</span><span class="sxs-lookup"><span data-stu-id="07b89-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="07b89-111">Hello que cela fonctionne consiste par frottement hello HTML sur la page de hello toofind ID DIV qui correspondent à certains critères et en enregistrant ensuite que les métadonnées pour cette application afin de nous pouvons relire ultérieurement les mots de passe tooit.</span><span class="sxs-lookup"><span data-stu-id="07b89-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="07b89-112">**Capture de champ de connexion manuelle** peut être utilisé dans le cas de hello hello application **n’affecte pas un fournisseur** hello d’entrée des champs utilisés pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="07b89-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="07b89-113">Capture de champ de connexion manuelle peut également servir dans les cas de hello lorsque hello **fournisseur restitue plusieurs champs** qui ne peut pas être détecté automatiquement.</span><span class="sxs-lookup"><span data-stu-id="07b89-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="07b89-114">Azure AD peut stocker les données pour que la page, de nombreux champs de hello connexion tant que vous nous dire où ces champs se trouvent sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="07b89-115">En règle générale, **si la capture de champ de connexion automatique ne fonctionne pas, nous suggérons toujours lors de l’option manuelle de hello.**</span><span class="sxs-lookup"><span data-stu-id="07b89-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="07b89-116">Comment tooautomatically capturer les champs de connexion pour une application</span><span class="sxs-lookup"><span data-stu-id="07b89-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="07b89-117">tooconfigure **mot de passe Single Sign-on** pour une application en utilisant **capture du champ de connexion automatique**, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07b89-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="07b89-118">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="07b89-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="07b89-119">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="07b89-120">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="07b89-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="07b89-121">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07b89-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="07b89-122">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="07b89-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="07b89-123">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="07b89-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="07b89-124">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="07b89-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="07b89-125">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="07b89-126">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="07b89-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="07b89-127">Entrez hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="07b89-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="07b89-128">Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour.</span><span class="sxs-lookup"><span data-stu-id="07b89-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="07b89-129">**Assurez-vous que connexion hello dans les champs est visibles à l’URL de hello vous fournissez**.</span><span class="sxs-lookup"><span data-stu-id="07b89-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="07b89-130">Cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="07b89-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="07b89-131">Une fois que vous le faire, nous allons capturer automatiquement cette URL pour un nom d’utilisateur et mot de passe zone d’entrée vous permettre de transmettre des toouse Azure AD toosecurely application toothat de mots de passe à l’aide d’extension du navigateur hello accès Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="07b89-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="07b89-132">Comment toomanually capturer les champs de connexion pour une application</span><span class="sxs-lookup"><span data-stu-id="07b89-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="07b89-133">toomanually capture champs de connexion, vous devez disposer d’extension de navigateur de panneau d’accès hello installée et **ne pas être en cours d’exécution en mode privé, inPrivate ou incognito.**</span><span class="sxs-lookup"><span data-stu-id="07b89-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="07b89-134">extension du navigateur tooinstall hello, suivez les étapes hello Bonjour [comment tooinstall hello extension du navigateur de panneau d’accès](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span><span class="sxs-lookup"><span data-stu-id="07b89-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="07b89-135">tooconfigure **mot de passe Single Sign-on** pour une application en utilisant **capture du champ de connexion manuelle**, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07b89-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="07b89-136">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="07b89-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="07b89-137">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="07b89-138">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="07b89-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="07b89-139">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07b89-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="07b89-140">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="07b89-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="07b89-141">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="07b89-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="07b89-142">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="07b89-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="07b89-143">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="07b89-144">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="07b89-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="07b89-145">Entrez hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="07b89-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="07b89-146">Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour.</span><span class="sxs-lookup"><span data-stu-id="07b89-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="07b89-147">**Assurez-vous que connexion hello dans les champs est visibles à l’URL de hello vous fournissez**.</span><span class="sxs-lookup"><span data-stu-id="07b89-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="07b89-148">Cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="07b89-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="07b89-149">Une fois que vous le faire, nous allons capturer automatiquement cette URL pour un nom d’utilisateur et mot de passe zone d’entrée vous permettre de transmettre des toouse Azure AD toosecurely application toothat de mots de passe à l’aide d’extension du navigateur hello accès Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="07b89-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="07b89-150">En cas de hello que cette opération échoue, vous pouvez **hello mode connexion toouse champ de connexion manuelle capture des modifications** en continuant toostep 12.</span><span class="sxs-lookup"><span data-stu-id="07b89-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="07b89-151">Cliquez sur **Configurer les paramètres d’authentification unique par mot de passe de** &lt;nom de l’application&gt;.</span><span class="sxs-lookup"><span data-stu-id="07b89-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="07b89-152">Sélectionnez hello **détecter manuellement les champs de connexion** option de configuration.</span><span class="sxs-lookup"><span data-stu-id="07b89-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="07b89-153">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="07b89-153">Click **Ok**.</span></span>

15. <span data-ttu-id="07b89-154">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="07b89-154">Click **Save**.</span></span>

16. <span data-ttu-id="07b89-155">Suivez hello sur l’écran des instructions toouse hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="07b89-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="07b89-156">Une erreur « Nous n’avons trouvé aucun champ de connexion à cette URL. » s’affiche</span><span class="sxs-lookup"><span data-stu-id="07b89-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="07b89-157">Vous obtenez cette erreur en cas d’échec de la détection automatique des champs de connexion.</span><span class="sxs-lookup"><span data-stu-id="07b89-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="07b89-158">tooresolve les étapes de ce problème, essayez la détection champ de connexion manuelle en suivant les hello Bonjour [comment toomanually capturer les champs de connexion pour une application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span><span class="sxs-lookup"><span data-stu-id="07b89-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="07b89-159">Je vois une erreur « Impossible de toosave Single Sign-on configuration »</span><span class="sxs-lookup"><span data-stu-id="07b89-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="07b89-160">Dans certains cas rares, la mise à jour de la configuration de l’authentification unique de l’hello peut échouer.</span><span class="sxs-lookup"><span data-stu-id="07b89-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="07b89-161">tooresolve cela réessayez hello seule configuration de l’authentification à nouveau.</span><span class="sxs-lookup"><span data-stu-id="07b89-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="07b89-162">Si le problème persiste toofail de manière cohérente, ouvrez une demande de support et fournissent des informations hello collectées Bonjour [comment toosee les détails de hello d’une notification de portail](#i-cannot-manually-detect-sign-in-fields-for-my-application) et [comment tooget aider en envoyant la notification détails tooa ingénieur de support](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span><span class="sxs-lookup"><span data-stu-id="07b89-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="07b89-163">Impossible de détecter manuellement les champs de connexion de mon application</span><span class="sxs-lookup"><span data-stu-id="07b89-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="07b89-164">Vous pouvez voir lorsque détection manuelle ne fonctionne pas de comportements de hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="07b89-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="07b89-165">processus de capture manuelle de Hello est apparue toowork, mais les champs hello capturées n’étaient pas correctes</span><span class="sxs-lookup"><span data-stu-id="07b89-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="07b89-166">champs de droite Hello ne sont soulignés lors de l’exécution du processus de capture hello</span><span class="sxs-lookup"><span data-stu-id="07b89-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="07b89-167">processus de capture Hello me prend page de connexion de l’application toohello comme prévu, mais rien ne se produit</span><span class="sxs-lookup"><span data-stu-id="07b89-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="07b89-168">Capture manuelle apparaît toowork, mais l’authentification unique ne se produit lorsque mes utilisateurs accèdent toohello application hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="07b89-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="07b89-169">Vérifiez les éléments suivants de hello si vous rencontrez l’une de ces problèmes :</span><span class="sxs-lookup"><span data-stu-id="07b89-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="07b89-170">Assurez-vous d’avoir hello dernière version d’extension du navigateur hello accès panneau **installé** et **activé** en suivant les étapes de hello Bonjour [comment tooinstall hello navigateur de panneau d’accès extension](#how-to-install-the-access-panel-browser-extension) section.</span><span class="sxs-lookup"><span data-stu-id="07b89-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="07b89-171">Assurez-vous que vous n’essayez pas de processus de capture hello lors de votre navigateur **mode privé, inPrivate ou incognito**.</span><span class="sxs-lookup"><span data-stu-id="07b89-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="07b89-172">extension de panneau d’accès Hello n’est pas pris en charge dans ces modes.</span><span class="sxs-lookup"><span data-stu-id="07b89-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="07b89-173">Assurez-vous que vos utilisateurs n’essaient pas de toosign dans l’application toohello à partir du panneau d’accès hello lors de **mode privé, inPrivate ou incognito**.</span><span class="sxs-lookup"><span data-stu-id="07b89-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="07b89-174">extension de panneau d’accès Hello n’est pas pris en charge dans ces modes.</span><span class="sxs-lookup"><span data-stu-id="07b89-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="07b89-175">Réessayez le processus de capture manuelle de hello, la vérification des marqueurs de hello rouge sont sur des champs de hello correct.</span><span class="sxs-lookup"><span data-stu-id="07b89-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="07b89-176">Si le processus de capture manuelle de hello semble toohang ou page de connexion hello ne rien (cas 3 ci-dessus), essayez à nouveau les processus de capture manuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="07b89-177">Mais, cette fois après avoir effectué le processus hello, appuyez sur hello **F12** bouton tooopen console de développement de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="07b89-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="07b89-178">Une fois, il, ouvrez hello **console** et type **window.location= »&lt;entrez hello signe dans l’url que vous avez spécifié lors de la configuration d’application hello&gt;»** , puis appuyez sur  **Entrez**.</span><span class="sxs-lookup"><span data-stu-id="07b89-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="07b89-179">Cette force une page de redirection qui terminer le processus de capture hello et stocker hello les champs qui ont été capturées.</span><span class="sxs-lookup"><span data-stu-id="07b89-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="07b89-180">Si aucune de ces approches ne fonctionne pour vous, nous pouvons vous aider.</span><span class="sxs-lookup"><span data-stu-id="07b89-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="07b89-181">Ouvrez un cas de prise en charge avec les détails de ce que vous avez essayé de, ainsi que les informations de hello collectées Bonjour hello [comment toosee les détails de hello d’une notification de portail](#i-cannot-manually-detect-sign-in-fields-for-my-application) et [comment tooget aider en envoyant des détails de la notification prise en charge tooa ingénieur](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="07b89-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="07b89-182">Comment tooinstall hello extension du navigateur de panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="07b89-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="07b89-183">tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07b89-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="07b89-184">Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07b89-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="07b89-185">Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="07b89-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="07b89-186">Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="07b89-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="07b89-187">En fonction de votre navigateur vous être lien de téléchargement toohello dirigée.</span><span class="sxs-lookup"><span data-stu-id="07b89-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="07b89-188">**Ajouter** navigateur de tooyour extension hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="07b89-189">Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.</span><span class="sxs-lookup"><span data-stu-id="07b89-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="07b89-190">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="07b89-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="07b89-191">Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="07b89-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="07b89-192">Vous pouvez également télécharger l’extension de hello pour Chrome et Firefox à partir de liens directs de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07b89-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="07b89-193">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="07b89-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="07b89-194">Extension du volet d’accès pour Firefox</span><span class="sxs-lookup"><span data-stu-id="07b89-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="07b89-195">Comment toosee les détails de hello d’une notification de portail</span><span class="sxs-lookup"><span data-stu-id="07b89-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="07b89-196">Vous pouvez voir les détails de hello toute notification portail en suivant les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07b89-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="07b89-197">Cliquez sur hello **Notifications** icône (clochette hello) dans hello coin supérieur droit de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="07b89-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="07b89-198">Sélectionnez une notification dans un **erreur** état (celles avec un toothem suivant rouge ( !)).</span><span class="sxs-lookup"><span data-stu-id="07b89-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="07b89-199">!NOTE] Vous ne pouvez pas cliquer sur les notifications affichant l’état **Réussi** ou **En cours**.</span><span class="sxs-lookup"><span data-stu-id="07b89-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="07b89-200">Cette hello ouvrir **détails de la Notification** panneau.</span><span class="sxs-lookup"><span data-stu-id="07b89-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="07b89-201">Utilisez ces informations vous-même toounderstand plus des détails sur le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="07b89-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="07b89-202">Si vous avez toujours besoin d’aide, vous pouvez également partager ces informations avec une prise en charge ingénieur ou hello groupe tooget aide produit avec votre problème.</span><span class="sxs-lookup"><span data-stu-id="07b89-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="07b89-203">Cliquez sur hello **copie** **icône** toohello à droite de hello **copiez erreur** toocopy de zone de texte tous les hello tooshare détails de notification avec un ingénieur du groupe de produit ou de la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="07b89-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="07b89-204">Comment tooget aider en envoyant l’ingénieur du support de notification détails tooa</span><span class="sxs-lookup"><span data-stu-id="07b89-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="07b89-205">Il est très important que vous partagez **tous hello détails ci-dessous** avec un ingénieur du support, si vous avez besoin d’aide, afin qu’ils peuvent vous aider à rapidement.</span><span class="sxs-lookup"><span data-stu-id="07b89-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="07b89-206">Vous pouvez facilement en cela **prendre une capture d’écran,** ou en cliquant sur hello **icône d’erreur de copie**, trouvé toohello Hello **erreur de copie** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="07b89-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="07b89-207">Explication des détails de la notification</span><span class="sxs-lookup"><span data-stu-id="07b89-207">Notification Details Explained</span></span>

<span data-ttu-id="07b89-208">Hello ci-dessous explique plus la fonction de chacun des éléments de notification hello et donne des exemples de chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="07b89-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="07b89-209">Éléments essentiels de la notification</span><span class="sxs-lookup"><span data-stu-id="07b89-209">Essential Notification Items</span></span>

-   <span data-ttu-id="07b89-210">**Titre** : hello titre descriptif de la notification de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="07b89-211">Exemple : **Paramètres de proxy d’application**</span><span class="sxs-lookup"><span data-stu-id="07b89-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="07b89-212">**Description** – hello description de ce qui s’est produite en raison de l’opération de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="07b89-213">Exemple : **L’URL interne entrée est déjà utilisée par une autre application**</span><span class="sxs-lookup"><span data-stu-id="07b89-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="07b89-214">**Id de notification** – id unique de hello de notification de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="07b89-215">Exemple : **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="07b89-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="07b89-216">**Id de demande client** – id de demande spécifique hello effectuée par votre navigateur</span><span class="sxs-lookup"><span data-stu-id="07b89-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="07b89-217">Exemple : **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="07b89-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="07b89-218">**Heure UTC de marqueur** – hello horodatage au cours de laquelle hello notification s’est produite, en heure UTC</span><span class="sxs-lookup"><span data-stu-id="07b89-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="07b89-219">Exemple : **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="07b89-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="07b89-220">**Id de Transaction interne** – hello ID interne, nous pouvons utiliser des erreurs de hello toolook dans nos systèmes</span><span class="sxs-lookup"><span data-stu-id="07b89-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="07b89-221">Exemple : **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="07b89-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="07b89-222">**UPN** – utilisateur hello qui a effectué l’opération de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="07b89-223">Exemple : **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="07b89-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="07b89-224">**Id de locataire** – ID unique de hello du client, hello dont hello utilisateur qui a effectué l’opération de hello était membre</span><span class="sxs-lookup"><span data-stu-id="07b89-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="07b89-225">Exemple : **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="07b89-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="07b89-226">**L’Id d’objet utilisateur** – hello ID unique de l’utilisateur hello qui a effectué l’opération de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="07b89-227">Exemple : **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="07b89-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="07b89-228">Éléments détaillés de la notification</span><span class="sxs-lookup"><span data-stu-id="07b89-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="07b89-229">**Nom d’affichage** – **(peut être vide)** un nom d’affichage plus détaillé pour l’erreur de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="07b89-230">Exemple *: **Paramètres de proxy d’application**</span><span class="sxs-lookup"><span data-stu-id="07b89-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="07b89-231">**État** – hello état spécifique de la notification de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="07b89-232">Exemple *: **Échec**</span><span class="sxs-lookup"><span data-stu-id="07b89-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="07b89-233">**Id d’objet** – **(peut être vide)** hello ID d’objet sur le hello opération a été effectuée</span><span class="sxs-lookup"><span data-stu-id="07b89-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="07b89-234">Exemple : **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="07b89-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="07b89-235">**Détails** – hello description détaillée de ce qui s’est produite en raison de l’opération de hello</span><span class="sxs-lookup"><span data-stu-id="07b89-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="07b89-236">Exemple : **l’URL interne 'http://bing.com/' n’est pas valide car elle est déjà en cours d’utilisation**</span><span class="sxs-lookup"><span data-stu-id="07b89-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="07b89-237">**Erreur de copie** – cliquez sur hello **icône de copie** toohello à droite de hello **copiez erreur** toocopy de zone de texte tous les hello tooshare détails de notification avec un ingénieur du groupe de support ou de produit</span><span class="sxs-lookup"><span data-stu-id="07b89-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="07b89-238">Exemple : ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="07b89-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="07b89-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07b89-239">Next steps</span></span>
[<span data-ttu-id="07b89-240">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="07b89-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

