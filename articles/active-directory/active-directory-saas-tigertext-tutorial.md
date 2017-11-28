---
title: "Didacticiel : Intégration d’Azure Active Directory à TigerText Secure Messenger | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TigerText Secure Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="064c0-103">Didacticiel : Intégration d’Azure Active Directory à TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="064c0-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="064c0-104">Dans ce didacticiel, vous allez apprendre à intégrer TigerText Secure Messenger à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="064c0-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="064c0-105">L’intégration de TigerText Secure Messenger dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="064c0-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="064c0-106">Dans Azure AD, vous pouvez contrôler qui a accès à TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="064c0-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="064c0-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à TigerText Secure Messenger (authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="064c0-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="064c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="064c0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="064c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="064c0-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="064c0-110">Prerequisites</span></span>

<span data-ttu-id="064c0-111">Pour configurer l’intégration d’Azure AD à TigerText Secure Messenger, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="064c0-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="064c0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="064c0-113">Un abonnement TigerText Secure Messenger pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="064c0-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="064c0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="064c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="064c0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="064c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="064c0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="064c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="064c0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="064c0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="064c0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="064c0-118">Scenario description</span></span>
<span data-ttu-id="064c0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="064c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="064c0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="064c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="064c0-121">Ajouter TigerText Secure Messenger à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="064c0-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="064c0-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="064c0-123">Ajouter TigerText Secure Messenger à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="064c0-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="064c0-124">Pour configurer l’intégration de TigerText Secure Messenger à Azure AD, vous devez ajouter TigerText Secure Messenger, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="064c0-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="064c0-125">**Pour ajouter TigerText Secure Messenger à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="064c0-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="064c0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="064c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="064c0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="064c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="064c0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="064c0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="064c0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="064c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="064c0-133">Dans la zone de recherche, tapez **TigerText Secure Messenger**, sélectionnez **TigerText Secure Messenger** à partir du volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="064c0-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Ajouter à partir de la galerie](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="064c0-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="064c0-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TigerText Secure Messenger pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="064c0-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="064c0-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TigerText Secure Messenger équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="064c0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="064c0-138">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur TigerText Secure Messenger associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="064c0-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="064c0-139">Dans TigerText Secure Messenger, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="064c0-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="064c0-140">Pour configurer et tester l’authentification unique Azure AD avec TigerText Secure Messenger, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="064c0-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="064c0-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="064c0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="064c0-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="064c0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="064c0-143">**[Créer un utilisateur de test TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)** pour avoir un équivalent de Britta Simon dans TigerText Secure Messenger, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="064c0-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="064c0-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="064c0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="064c0-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="064c0-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="064c0-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="064c0-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="064c0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="064c0-148">**Pour configurer l’authentification unique Azure AD avec TigerText Secure Messenger, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="064c0-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="064c0-149">Dans le portail Azure, dans la page d’intégration de l’application **TigerText Secure Messenger**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="064c0-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="064c0-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="064c0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="064c0-153">Dans la section **Domaine et URL TigerText Secure Messenger**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="064c0-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Section Domaine et URL TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="064c0-155">a.</span><span class="sxs-lookup"><span data-stu-id="064c0-155">a.</span></span> <span data-ttu-id="064c0-156">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="064c0-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="064c0-157">b.</span><span class="sxs-lookup"><span data-stu-id="064c0-157">b.</span></span> <span data-ttu-id="064c0-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="064c0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="064c0-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="064c0-159">This value is not real.</span></span> <span data-ttu-id="064c0-160">Mettez à jour cette valeur avec l’identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="064c0-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="064c0-161">Contactez l’[équipe de support de TigerText Secure Messenger](mailTo:prosupport@tigertext.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="064c0-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="064c0-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="064c0-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="064c0-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="064c0-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="064c0-166">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support technique TigerText Secure Messenger](mailTo:prosupport@tigertext.com), en lui fournissant les **métadonnées téléchargées**.</span><span class="sxs-lookup"><span data-stu-id="064c0-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="064c0-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="064c0-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="064c0-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="064c0-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="064c0-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="064c0-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="064c0-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-170">Create an Azure AD test user</span></span>
<span data-ttu-id="064c0-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="064c0-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="064c0-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="064c0-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="064c0-174">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="064c0-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="064c0-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="064c0-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes->Tous les utilisateurs](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="064c0-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="064c0-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="064c0-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="064c0-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="064c0-182">a.</span><span class="sxs-lookup"><span data-stu-id="064c0-182">a.</span></span> <span data-ttu-id="064c0-183">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="064c0-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="064c0-184">b.</span><span class="sxs-lookup"><span data-stu-id="064c0-184">b.</span></span> <span data-ttu-id="064c0-185">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="064c0-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="064c0-186">c.</span><span class="sxs-lookup"><span data-stu-id="064c0-186">c.</span></span> <span data-ttu-id="064c0-187">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="064c0-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="064c0-188">d.</span><span class="sxs-lookup"><span data-stu-id="064c0-188">d.</span></span> <span data-ttu-id="064c0-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="064c0-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="064c0-190">Créer un utilisateur de test TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="064c0-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="064c0-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans TigerText.</span><span class="sxs-lookup"><span data-stu-id="064c0-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="064c0-192">Veuillez contacter l’[équipe de support TigerText Secure Messenger](mailTo:prosupport@tigertext.com) pour ajouter des utilisateurs à la plateforme TigerText.</span><span class="sxs-lookup"><span data-stu-id="064c0-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="064c0-193">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="064c0-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="064c0-194">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="064c0-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="064c0-196">**Pour affecter Britta Simon à TigerText Secure Messenger, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="064c0-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="064c0-197">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="064c0-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="064c0-199">Dans la liste des applications, sélectionnez **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="064c0-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger dans la liste des applications](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="064c0-201">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="064c0-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="064c0-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="064c0-203">Click **Add** button.</span></span> <span data-ttu-id="064c0-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="064c0-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="064c0-206">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="064c0-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="064c0-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="064c0-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="064c0-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="064c0-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="064c0-209">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="064c0-209">Test single sign-on</span></span>

<span data-ttu-id="064c0-210">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="064c0-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="064c0-211">Lorsque vous cliquez sur la vignette TigerText dans le volet d’accès, vous êtes normalement connecté automatiquement à votre application TigerText.</span><span class="sxs-lookup"><span data-stu-id="064c0-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="064c0-212">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="064c0-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="064c0-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="064c0-213">Additional resources</span></span>

* [<span data-ttu-id="064c0-214">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="064c0-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="064c0-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="064c0-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

