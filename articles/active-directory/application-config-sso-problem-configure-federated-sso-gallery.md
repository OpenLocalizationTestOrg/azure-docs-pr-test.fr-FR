---
title: "aaaProblem configuration fédérée l’authentification unique pour une application Azure AD galerie | Documents Microsoft"
description: "Résoudre certains des problèmes courants de hello vous pouvez rencontrer lors de la configuration fédérée seule l’authentification à l’aide de SAML pour les applications qui sont répertoriées dans la galerie d’applications Azure AD de hello"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="28c7d-103">Problème de configuration de l’authentification unique fédérée pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="28c7d-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="28c7d-104">Si vous rencontrez un problème lors de la configuration d’une application,</span><span class="sxs-lookup"><span data-stu-id="28c7d-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="28c7d-105">Vérifiez que vous avez suivi toutes les étapes de hello dans didacticiel hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="28c7d-106">Dans la configuration de l’application hello, vous disposez de la documentation inline sur la façon dont tooconfigure hello application.</span><span class="sxs-lookup"><span data-stu-id="28c7d-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="28c7d-107">Vous pouvez également accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir une aide pas à pas détaillé.</span><span class="sxs-lookup"><span data-stu-id="28c7d-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="28c7d-108">Impossible d’ajouter une autre instance de l’application hello</span><span class="sxs-lookup"><span data-stu-id="28c7d-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="28c7d-109">tooadd une deuxième instance d’une application, vous devez toobe en mesure de :</span><span class="sxs-lookup"><span data-stu-id="28c7d-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="28c7d-110">Configurer un identificateur unique pour la deuxième instance de hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="28c7d-111">Vous ne serez pas hello tooconfigure en mesure de même identificateur utilisé pour première instance de hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="28c7d-112">Configurer un certificat différent que hello celui utilisé pour la première instance de hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="28c7d-113">Si hello application ne prend en charge des hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="28c7d-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="28c7d-114">Ensuite, vous ne serez pas en mesure de tooconfigure une deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="28c7d-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="28c7d-115">Impossible d’ajouter hello identificateur ou de hello URL de réponse</span><span class="sxs-lookup"><span data-stu-id="28c7d-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="28c7d-116">Si vous n’êtes pas en mesure de tooconfigure hello identificateur ou hello URL de réponse, confirmez hello identificateur et valeurs de l’URL de réponse correspondent hello préconfiguré pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="28c7d-117">modèles de hello tooknow préconfigurés pour l’application hello :</span><span class="sxs-lookup"><span data-stu-id="28c7d-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="28c7d-118">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.** Accédez à toostep 7.</span><span class="sxs-lookup"><span data-stu-id="28c7d-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="28c7d-119">Si vous êtes déjà dans le panneau de configuration d’application hello sur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28c7d-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="28c7d-120">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="28c7d-121">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="28c7d-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="28c7d-122">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28c7d-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="28c7d-123">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="28c7d-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="28c7d-124">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="28c7d-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="28c7d-125">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28c7d-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="28c7d-126">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="28c7d-127">Sélectionnez **SAML-authentification** de hello **Mode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="28c7d-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="28c7d-128">Accédez toohello **identificateur** ou **URL de réponse** zone de texte, sous hello **section URL et de domaine.**</span><span class="sxs-lookup"><span data-stu-id="28c7d-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="28c7d-129">Il existe trois façons de tooknow des modèles de hello pris en charge pour l’application hello :</span><span class="sxs-lookup"><span data-stu-id="28c7d-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="28c7d-130">Dans la zone de texte hello, vous consultez ou hello pris en charge les modèles comme un espace réservé *exemple :* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="28c7d-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="28c7d-131">Si le modèle de hello n’est pas pris en charge, vous consultez un point d’exclamation rouge lorsque vous essayez de valeur de hello tooenter dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="28c7d-132">Si vous pointez votre souris sur le point d’exclamation rouge de hello, vous voir les modèles de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="28c7d-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="28c7d-133">Dans le didacticiel hello pour une application hello, vous pouvez également obtenir des informations sur les modèles de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="28c7d-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="28c7d-134">Sous hello **Azure AD de configurer l’authentification unique sur** section.</span><span class="sxs-lookup"><span data-stu-id="28c7d-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="28c7d-135">Étape accédez toohello pour les valeurs hello configuré sous hello **domaine et les URL** section.</span><span class="sxs-lookup"><span data-stu-id="28c7d-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="28c7d-136">Si les valeurs hello ne correspondent pas avec les modèles hello préconfigurés sur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28c7d-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="28c7d-137">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="28c7d-137">You can:</span></span>

-   <span data-ttu-id="28c7d-138">Travailler avec des valeurs de tooget du fournisseur d’application hello qui correspondent au modèle hello préconfiguré sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="28c7d-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="28c7d-139">Ou bien, vous pouvez contacter l’équipe d’Azure AD à < aadapprequest@microsoft.com > ou laisser un commentaire dans hello toorequest didacticiel hello mise à jour des modèles de hello pris en charge pour l’application hello</span><span class="sxs-lookup"><span data-stu-id="28c7d-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="28c7d-140">Où définir le format de hello EntityID (identifiant d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="28c7d-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="28c7d-141">Vous ne sont pas être en mesure de tooselect hello au format EntityID (identifiant d’utilisateur) que Azure AD envoie toohello application dans la réponse de hello après l’authentification des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="28c7d-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="28c7d-142">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="28c7d-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="28c7d-143">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) section hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="28c7d-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="28c7d-144">Impossible de trouver hello Azure AD métadonnées toocomplete hello configuration avec l’application hello</span><span class="sxs-lookup"><span data-stu-id="28c7d-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="28c7d-145">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="28c7d-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="28c7d-146">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="28c7d-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="28c7d-147">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="28c7d-148">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="28c7d-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="28c7d-149">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28c7d-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="28c7d-150">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="28c7d-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="28c7d-151">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="28c7d-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="28c7d-152">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28c7d-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="28c7d-153">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="28c7d-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="28c7d-154">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="28c7d-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="28c7d-155">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="28c7d-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="28c7d-156">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="28c7d-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="28c7d-157">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="28c7d-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="28c7d-158">Ne connaissez pas comment toocustomize SAML revendications envoyé tooan application</span><span class="sxs-lookup"><span data-stu-id="28c7d-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="28c7d-159">toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="28c7d-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28c7d-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28c7d-160">Next steps</span></span>
[<span data-ttu-id="28c7d-161">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28c7d-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
