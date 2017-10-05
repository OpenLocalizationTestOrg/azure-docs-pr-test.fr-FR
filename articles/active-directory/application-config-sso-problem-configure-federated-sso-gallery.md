---
title: "Problème de configuration de l’authentification unique fédérée pour une application de la galerie Azure AD | Microsoft Docs"
description: "Découvrez comment résoudre certains problèmes courants que vous pouvez rencontrer lors de la configuration de l’authentification unique fédérée avec SAML pour les applications répertoriées dans la galerie d’applications Azure AD"
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="01482-103">Problème de configuration de l’authentification unique fédérée pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="01482-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="01482-104">Si vous rencontrez un problème lors de la configuration d’une application,</span><span class="sxs-lookup"><span data-stu-id="01482-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="01482-105">vérifiez que vous avez suivi toutes les étapes du didacticiel dédié à l’application.</span><span class="sxs-lookup"><span data-stu-id="01482-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="01482-106">Dans la configuration de l’application, une documentation en ligne sur la configuration de l’application vous est proposée.</span><span class="sxs-lookup"><span data-stu-id="01482-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="01482-107">Pour une aide pas à pas détaillée, vous pouvez accéder à la [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="01482-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="01482-108">Impossible d’ajouter une autre instance de l’application</span><span class="sxs-lookup"><span data-stu-id="01482-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="01482-109">Pour ajouter une deuxième instance d’une application, vous devez être en mesure de :</span><span class="sxs-lookup"><span data-stu-id="01482-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="01482-110">Configurer un identificateur unique pour la deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="01482-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="01482-111">Vous ne pourrez pas configurer le même identificateur que celui utilisé pour la première instance.</span><span class="sxs-lookup"><span data-stu-id="01482-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="01482-112">Configurer un certificat différent de celui utilisé pour la première instance.</span><span class="sxs-lookup"><span data-stu-id="01482-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="01482-113">Si l’application ne prend en charge aucune de ces configurations,</span><span class="sxs-lookup"><span data-stu-id="01482-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="01482-114">vous ne pourrez pas configurer une deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="01482-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="01482-115">Impossible d’ajouter l’identificateur ou l’URL de réponse</span><span class="sxs-lookup"><span data-stu-id="01482-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="01482-116">Si vous n’êtes pas en mesure de configurer l’identificateur ou l’URL de réponse, vérifiez que les valeurs de l’identificateur et de l’URL de réponse correspondent aux modèles préconfigurés pour l’application.</span><span class="sxs-lookup"><span data-stu-id="01482-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="01482-117">Pour connaître les modèles préconfigurés pour l’application :</span><span class="sxs-lookup"><span data-stu-id="01482-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="01482-118">Ouvrez le [**Portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’Administrateur général** ou **Coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="01482-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="01482-119">Passez à l’étape 7.</span><span class="sxs-lookup"><span data-stu-id="01482-119">Go to step 7.</span></span> <span data-ttu-id="01482-120">Si vous êtes déjà dans le panneau de configuration de l’application sur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01482-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="01482-121">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="01482-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="01482-122">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01482-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="01482-123">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01482-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="01482-124">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="01482-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="01482-125">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="01482-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="01482-126">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="01482-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="01482-127">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="01482-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="01482-128">Sélectionnez **Authentification basée sur SAML** dans la liste déroulante **Mode**.</span><span class="sxs-lookup"><span data-stu-id="01482-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="01482-129">Accédez à la zone de texte **Identificateur** ou **URL de réponse** sous la section **Domaine et URL**.</span><span class="sxs-lookup"><span data-stu-id="01482-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="01482-130">Il existe trois façons de connaître les modèles pris en charge pour l’application :</span><span class="sxs-lookup"><span data-stu-id="01482-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="01482-131">Dans la zone de texte, les modèles pris en charge apparaissent sous forme d’espace réservé. *Exemple :* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="01482-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="01482-132">Si le modèle n’est pas pris en charge, un point d’exclamation rouge s’affiche lorsque vous essayez d’entrer la valeur dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="01482-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="01482-133">Si vous placez le pointeur de la souris sur le point d’exclamation rouge, les modèles pris en charge s’affichent.</span><span class="sxs-lookup"><span data-stu-id="01482-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="01482-134">Vous pouvez également obtenir des informations sur les modèles pris en charge dans le didacticiel dédié à l’application.</span><span class="sxs-lookup"><span data-stu-id="01482-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="01482-135">Sous la section **Configurer Azure AD pour l’authentification unique**,</span><span class="sxs-lookup"><span data-stu-id="01482-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="01482-136">accédez à l’étape de configuration des valeurs sous la section **Domaine et URL**.</span><span class="sxs-lookup"><span data-stu-id="01482-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="01482-137">Si les valeurs ne correspondent aux modèles préconfigurés sur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01482-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="01482-138">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="01482-138">You can:</span></span>

-   <span data-ttu-id="01482-139">Travailler avec le fournisseur de l’application pour obtenir des valeurs qui correspondent au modèle préconfiguré sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="01482-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="01482-140">Contacter l’équipe Azure AD à l’adresse <aadapprequest@microsoft.com> ou laisser un commentaire dans le didacticiel pour demander la mise à jour des modèles pris en charge pour l’application</span><span class="sxs-lookup"><span data-stu-id="01482-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="01482-141">Où définir le format d’EntityID (identificateur d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="01482-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="01482-142">Vous ne pouvez pas sélectionner le format d’EntityID (identificateur d’utilisateur) qu’Azure AD envoie à l’application dans la réponse après l’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01482-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="01482-143">Azure AD sélectionne le format de l’attribut NameID (identificateur d’utilisateur) en fonction de la valeur sélectionnée ou du format demandé par l’application dans la demande d’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="01482-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="01482-144">Pour plus d’informations, consultez l’article [Protocole SAML d’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) dans la section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="01482-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="01482-145">Impossible de trouver les métadonnées Azure AD pour terminer la configuration avec l’application</span><span class="sxs-lookup"><span data-stu-id="01482-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="01482-146">Pour télécharger le certificat ou les métadonnées de l’application à partir d’Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="01482-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="01482-147">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="01482-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="01482-148">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="01482-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="01482-149">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01482-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="01482-150">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01482-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="01482-151">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="01482-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="01482-152">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="01482-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="01482-153">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="01482-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="01482-154">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="01482-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="01482-155">Accédez à la section **Certificat de signature SAML**, puis cliquez sur la valeur de colonne **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="01482-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="01482-156">En fonction de ce que l’application nécessite pour configurer l’authentification unique, vous voyez soit l’option de téléchargement des métadonnées XML, soit le certificat.</span><span class="sxs-lookup"><span data-stu-id="01482-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="01482-157">Azure AD ne fournit pas d’URL permettant d’obtenir les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="01482-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="01482-158">Les métadonnées peuvent uniquement être récupérées sous forme de fichier XML.</span><span class="sxs-lookup"><span data-stu-id="01482-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="01482-159">Vous ne savez pas comment personnaliser les revendications SAML envoyées à une application</span><span class="sxs-lookup"><span data-stu-id="01482-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="01482-160">Pour savoir comment personnaliser les revendications d’attribut SAML envoyées à votre application, consultez [Claims mapping in Azure Active Directory (public preview)](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mappage de revendications dans Azure Active Directory [préversion]) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="01482-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01482-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01482-161">Next steps</span></span>
[<span data-ttu-id="01482-162">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01482-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
