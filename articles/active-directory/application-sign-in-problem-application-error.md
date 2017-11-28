---
title: "aaaError sur une page de l’application après l’ouverture de session | Documents Microsoft"
description: "Comment les problèmes de tooresolve avec Azure AD se connectent lors de l’application hello lui-même émet une erreur"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="ea13f-103">Erreur dans la page d’une application après la connexion</span><span class="sxs-lookup"><span data-stu-id="ea13f-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="ea13f-104">Dans ce scénario, Azure AD a signé utilisateur hello dans mais hello application affiche une erreur interdisant hello utilisateur toosuccessfully terminer hello signe dans le flux.</span><span class="sxs-lookup"><span data-stu-id="ea13f-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="ea13f-105">Dans ce scénario, application hello n’accepte pas de problème de réponse hello par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea13f-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="ea13f-106">Voici quelques raisons possibles pour lesquelles application hello n’a pas accepté la réponse hello d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea13f-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="ea13f-107">Si l’erreur hello dans l’application hello n’est pas assez clair tooknow ce qui est manquant dans la réponse de hello, puis :</span><span class="sxs-lookup"><span data-stu-id="ea13f-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="ea13f-108">Si l’application hello est hello Azure AD galerie, vérifiez vous avez suivi toutes les étapes de hello dans l’article de hello [comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="ea13f-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="ea13f-109">Utiliser un outil tel que [Fiddler](http://www.telerik.com/fiddler) toocapture SAML demande, la réponse SAML et jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="ea13f-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="ea13f-110">Partager la réponse SAML de hello avec tooknow de fournisseur d’application hello ce qui est manquant.</span><span class="sxs-lookup"><span data-stu-id="ea13f-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="ea13f-111">Attributs manquants hello réponse SAML</span><span class="sxs-lookup"><span data-stu-id="ea13f-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="ea13f-112">tooadd un attribut dans toobe de configuration d’Azure AD hello envoyé en réponse de hello Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea13f-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="ea13f-113">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ea13f-114">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ea13f-115">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ea13f-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ea13f-116">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea13f-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ea13f-117">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ea13f-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ea13f-118">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ea13f-119">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ea13f-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ea13f-120">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ea13f-121">Cliquez sur **affichage et modification des attributs de tous les autres utilisateurs sous** hello **attributs utilisateur** hello tooedit de section attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ea13f-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="ea13f-122">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="ea13f-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="ea13f-123">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="ea13f-123">click **Add attribute**.</span></span> <span data-ttu-id="ea13f-124">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="ea13f-125">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-125">Click **Save.**</span></span> <span data-ttu-id="ea13f-126">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="ea13f-127">Enregistrer la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-127">Save hello configuration.</span></span>

<span data-ttu-id="ea13f-128">Prochaine connexion d’utilisateur de hello dans toohello application, Azure AD envoyer nouvel attribut de hello Bonjour réponse SAML.</span><span class="sxs-lookup"><span data-stu-id="ea13f-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="ea13f-129">application Hello attend une autre valeur de l’identificateur de l’utilisateur ou d’un format</span><span class="sxs-lookup"><span data-stu-id="ea13f-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="ea13f-130">Hello connectez-vous toohello application échoue car hello réponse SAML manque des attributs tels que les rôles ou application hello attend un autre format d’attribut de EntityID hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="ea13f-131">Ajoutez un attribut dans la configuration de l’application hello Azure AD :</span><span class="sxs-lookup"><span data-stu-id="ea13f-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="ea13f-132">toochange hello valeur d’identificateur de l’utilisateur, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea13f-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="ea13f-133">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ea13f-134">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ea13f-135">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ea13f-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ea13f-136">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea13f-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ea13f-137">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ea13f-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ea13f-138">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ea13f-139">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ea13f-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ea13f-140">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ea13f-141">Sous hello **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ea13f-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="ea13f-142">Changer le format d’EntityID (identificateur d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="ea13f-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="ea13f-143">Si l’application hello attend un autre format pour l’attribut EntityID de hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="ea13f-144">Ensuite, vous n’être tooselect en mesure de hello au format EntityID (identifiant d’utilisateur) que Azure AD envoie toohello application dans la réponse de hello après l’authentification des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ea13f-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="ea13f-145">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="ea13f-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="ea13f-146">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="ea13f-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="ea13f-147">application Hello attend une méthode de signature différente pour hello réponse SAML</span><span class="sxs-lookup"><span data-stu-id="ea13f-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="ea13f-148">toochange quelles parties du jeton SAML de hello sont signés numériquement par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea13f-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="ea13f-149">Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea13f-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="ea13f-150">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ea13f-151">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ea13f-152">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ea13f-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ea13f-153">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea13f-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ea13f-154">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ea13f-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ea13f-155">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ea13f-156">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ea13f-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ea13f-157">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ea13f-158">Cliquez sur **afficher les paramètres de signature de certificat avancés** sous hello **le certificat de signature SAML** section.</span><span class="sxs-lookup"><span data-stu-id="ea13f-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="ea13f-159">Sélectionnez hello approprié **Option de signature** attendu par l’application hello :</span><span class="sxs-lookup"><span data-stu-id="ea13f-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="ea13f-160">Signer la réponse SAML</span><span class="sxs-lookup"><span data-stu-id="ea13f-160">Sign SAML response</span></span>

  * <span data-ttu-id="ea13f-161">Signer la réponse et l’assertion SAML</span><span class="sxs-lookup"><span data-stu-id="ea13f-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="ea13f-162">Signer l’assertion SAML</span><span class="sxs-lookup"><span data-stu-id="ea13f-162">Sign SAML assertion</span></span>

<span data-ttu-id="ea13f-163">Prochaine connexion d’utilisateur de hello dans toohello application, d’authentification Azure AD hello partie de réponse SAML de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ea13f-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="ea13f-164">application Hello attend hello signature toobe de l’algorithme SHA-1</span><span class="sxs-lookup"><span data-stu-id="ea13f-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="ea13f-165">Par défaut, Azure AD connecte le jeton SAML de hello à l’aide de hello la plupart des algorithme de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ea13f-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="ea13f-166">Modifier l’algorithme de connexion hello tooSHA-1 n’est pas recommandée, sauf si requis par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="ea13f-167">toochange hello algorithme de signature, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea13f-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="ea13f-168">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ea13f-169">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ea13f-170">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ea13f-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ea13f-171">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea13f-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ea13f-172">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ea13f-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ea13f-173">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ea13f-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ea13f-174">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ea13f-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ea13f-175">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ea13f-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ea13f-176">Cliquez sur **afficher les paramètres de signature de certificat avancés** sous hello **le certificat de signature SAML** section.</span><span class="sxs-lookup"><span data-stu-id="ea13f-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="ea13f-177">Sélectionnez l’algorithme SHA-1, Bonjour **algorithme de signature**.</span><span class="sxs-lookup"><span data-stu-id="ea13f-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="ea13f-178">Prochaine hello utilisateur s’inscrit dans l’application de toohello, d’authentification Azure AD hello jeton SAML utilisant l’algorithme SHA-1.</span><span class="sxs-lookup"><span data-stu-id="ea13f-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea13f-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea13f-179">Next steps</span></span>
[<span data-ttu-id="ea13f-180">Comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea13f-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
