---
title: "Didacticiel : Intégration d’Azure Active Directory à MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et MOVEit Transfer - Azure AD integration."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="c429b-103">Didacticiel : Intégration d’Azure Active Directory à MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="c429b-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="c429b-104">Dans ce didacticiel, vous allez apprendre à intégrer MOVEit Transfer - Azure AD integration à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c429b-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c429b-105">L’intégration de MOVEit Transfer - Azure AD integration à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c429b-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c429b-106">Dans Azure AD, vous pouvez contrôler qui a accès à MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c429b-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="c429b-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à MOVEit Transfer - Azure AD integration (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c429b-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c429b-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c429b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c429b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c429b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c429b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c429b-110">Prerequisites</span></span>

<span data-ttu-id="c429b-111">Pour configurer l’intégration de MOVEit Transfer - Azure AD integration à Azure AD, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c429b-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="c429b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c429b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c429b-113">Un abonnement MOVEit Transfer - Azure AD integration pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c429b-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c429b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c429b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c429b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c429b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c429b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c429b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c429b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c429b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c429b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c429b-118">Scenario description</span></span>
<span data-ttu-id="c429b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c429b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c429b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c429b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c429b-121">Ajout de MOVEit Transfer - Azure AD integration à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c429b-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="c429b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c429b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="c429b-123">Ajout de MOVEit Transfer - Azure AD integration à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c429b-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="c429b-124">Pour configurer l’intégration de MOVEit Transfer - Azure AD integration avec Azure AD, vous devez ajouter MOVEit Transfer - Azure AD integration, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c429b-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c429b-125">**Pour ajouter MOVEit Transfer - Azure AD integration à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c429b-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c429b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c429b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="c429b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c429b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c429b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c429b-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="c429b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c429b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="c429b-133">Dans la zone de recherche, tapez **MOVEit Transfer - Azure AD integration**, sélectionnez **MOVEit Transfer - Azure AD integration** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c429b-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![MOVEit Transfer - Azure AD integration dans la liste des résultats](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c429b-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c429b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c429b-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MOVEit Transfer - Azure AD integration avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c429b-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c429b-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur MOVEit Transfer - Azure AD integration équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c429b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="c429b-138">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur MOVEit Transfer - Azure AD integration associé.</span><span class="sxs-lookup"><span data-stu-id="c429b-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="c429b-139">Dans MOVEit Transfer - Azure AD integration, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c429b-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c429b-140">Pour configurer et tester l’authentification unique Azure AD avec MOVEit Transfer - Azure AD integration, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c429b-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c429b-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c429b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c429b-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c429b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c429b-143">**[Créer un utilisateur de test MOVEit Transfer - Azure AD integration](#create-a-moveit-transfer---azure-ad-integration-test-user)** pour avoir un équivalent de Britta Simon dans MOVEit Transfer - Azure AD integration lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c429b-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c429b-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c429b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c429b-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c429b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c429b-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c429b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c429b-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c429b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="c429b-148">**Pour configurer l’authentification unique Azure AD avec MOVEit Transfer - Azure AD integration, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c429b-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="c429b-149">Dans le portail Azure, sur la page d’intégration de l’application **MOVEit Transfer - Azure AD integration**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c429b-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c429b-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c429b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="c429b-153">Dans la section **Domaine et URL MOVEit Transfer - Azure AD integration**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c429b-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="c429b-155">a.</span><span class="sxs-lookup"><span data-stu-id="c429b-155">a.</span></span> <span data-ttu-id="c429b-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="c429b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="c429b-157">b.</span><span class="sxs-lookup"><span data-stu-id="c429b-157">b.</span></span> <span data-ttu-id="c429b-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="c429b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="c429b-159">c.</span><span class="sxs-lookup"><span data-stu-id="c429b-159">c.</span></span> <span data-ttu-id="c429b-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="c429b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="c429b-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c429b-161">These values are not real.</span></span> <span data-ttu-id="c429b-162">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="c429b-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c429b-163">Vous pouvez vous reporter à ces valeurs ultérieurement dans la section **URL de métadonnées du fournisseur de service**, ou contacter l’[équipe de support technique MOVEit Transfer - Azure AD integration](https://community.ipswitch.com/s/support) pour les obtenir.</span><span class="sxs-lookup"><span data-stu-id="c429b-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="c429b-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c429b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="c429b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c429b-166">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="c429b-168">Connectez-vous à votre client MOVEit Transfer - Azure AD integration en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c429b-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="c429b-169">Dans le volet de navigation gauche, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c429b-169">On the left navigation pane, click **Settings**.</span></span>

    ![Section Paramètres côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="c429b-171">Cliquez sur le lien **Authentification unique** qui se trouve sous **Stratégies de sécurité -> Authentification des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c429b-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Stratégies de sécurité côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="c429b-173">Cliquez sur le lien URL de métadonnées pour télécharger le document de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="c429b-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![URL de métadonnées du fournisseur de service](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="c429b-175">Vérifiez que la valeur **entityID** correspond à celle de l’**identificateur** dans la section **Domaine et URL MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="c429b-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="c429b-176">Vérifiez que l’URL d’emplacement **AssertionConsumerService** correspond à l’**URL de réponse** dans la section **Domaine et URL MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="c429b-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="c429b-178">Cliquez sur **Add Identity Provider** (Ajouter un fournisseur d’identité) pour ajouter un nouveau fournisseur d’identité fédéré.</span><span class="sxs-lookup"><span data-stu-id="c429b-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![Ajouter un fournisseur d’identité](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="c429b-180">Cliquez sur **Parcourir...** pour sélectionner le fichier de métadonnées que vous avez téléchargé à partir du portail Azure, puis cliquez sur **Ajouter un fournisseur d’identité** pour charger le fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="c429b-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![Fournisseur d’identité SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="c429b-182">Sélectionnez **Oui** sous **Activé** dans la page **Edit Federated Identity Provider Settings** (Modifier les paramètres du fournisseur d’identité fédéré...), puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c429b-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Paramètres de fournisseur d’identité fédérée](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="c429b-184">Dans la page **Edit Federated Identity Provider User Settings** (Modifier les paramètres utilisateur du fournisseur d’identité fédérée), effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c429b-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Modifier les paramètres de fournisseur d’identité fédérée](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="c429b-186">a.</span><span class="sxs-lookup"><span data-stu-id="c429b-186">a.</span></span> <span data-ttu-id="c429b-187">Sélectionnez **SAML NameID** comme **Nom de connexion**.</span><span class="sxs-lookup"><span data-stu-id="c429b-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="c429b-188">b.</span><span class="sxs-lookup"><span data-stu-id="c429b-188">b.</span></span> <span data-ttu-id="c429b-189">Sélectionnez **Autre** comme **Nom complet** et dans la zone de texte **Nom de l’attribut**, insérez la valeur : `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="c429b-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="c429b-190">c.</span><span class="sxs-lookup"><span data-stu-id="c429b-190">c.</span></span> <span data-ttu-id="c429b-191">Sélectionnez **Autre** comme **E-mail** et dans la zone de texte **Nom de l’attribut**, insérez la valeur : `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="c429b-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="c429b-192">d.</span><span class="sxs-lookup"><span data-stu-id="c429b-192">d.</span></span> <span data-ttu-id="c429b-193">Sélectionnez **Oui** sous **Auto-create account on signon** (Créer automatiquement un compte lors de l’authentification).</span><span class="sxs-lookup"><span data-stu-id="c429b-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="c429b-194">e.</span><span class="sxs-lookup"><span data-stu-id="c429b-194">e.</span></span> <span data-ttu-id="c429b-195">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c429b-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="c429b-196">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c429b-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c429b-197">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c429b-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c429b-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c429b-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c429b-199">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c429b-199">Create an Azure AD test user</span></span>

<span data-ttu-id="c429b-200">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c429b-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c429b-202">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c429b-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c429b-203">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c429b-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c429b-205">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c429b-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c429b-207">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c429b-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c429b-209">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c429b-209">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c429b-211">a.</span><span class="sxs-lookup"><span data-stu-id="c429b-211">a.</span></span> <span data-ttu-id="c429b-212">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c429b-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c429b-213">b.</span><span class="sxs-lookup"><span data-stu-id="c429b-213">b.</span></span> <span data-ttu-id="c429b-214">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c429b-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c429b-215">c.</span><span class="sxs-lookup"><span data-stu-id="c429b-215">c.</span></span> <span data-ttu-id="c429b-216">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c429b-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c429b-217">d.</span><span class="sxs-lookup"><span data-stu-id="c429b-217">d.</span></span> <span data-ttu-id="c429b-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c429b-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="c429b-219">Créer un utilisateur de test MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="c429b-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="c429b-220">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c429b-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="c429b-221">MOVEit Transfer - Azure AD integration prend en charge l’approvisionnement juste-à-temps que vous avez activé.</span><span class="sxs-lookup"><span data-stu-id="c429b-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="c429b-222">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="c429b-222">There is no action item for you in this section.</span></span> <span data-ttu-id="c429b-223">Un utilisateur est créé lors d’une tentative d’accès à MOVEit Transfer - Azure AD integration s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="c429b-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="c429b-224">Si vous devez créer un utilisateur manuellement, contactez l’[équipe du support technique MOVEit Transfer - Azure AD integration](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="c429b-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c429b-225">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c429b-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="c429b-226">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c429b-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="c429b-228">**Pour affecter Britta Simon à MOVEit Transfer - Azure AD integration, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c429b-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="c429b-229">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c429b-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c429b-231">Dans la liste des applications, sélectionnez **MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="c429b-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Lien MOVEit Transfer - Azure AD integration dans la liste des applications](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="c429b-233">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c429b-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="c429b-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c429b-235">Click **Add** button.</span></span> <span data-ttu-id="c429b-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c429b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="c429b-238">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c429b-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c429b-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c429b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c429b-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c429b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c429b-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c429b-241">Test single sign-on</span></span>

<span data-ttu-id="c429b-242">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c429b-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c429b-243">Lorsque vous cliquez sur la vignette MOVEit Transfer - Azure AD integration dans le volet d’accès, vous êtes connecté automatiquement à votre application MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c429b-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c429b-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c429b-244">Additional resources</span></span>

* [<span data-ttu-id="c429b-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c429b-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c429b-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c429b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

