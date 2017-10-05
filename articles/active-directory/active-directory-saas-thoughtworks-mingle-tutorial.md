---
title: "Didacticiel : intégration d’Azure Active Directory à Thoughtworks Mingle | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="ea8df-103">Didacticiel : Intégration d’Azure AD à Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="ea8df-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="ea8df-104">Dans ce didacticiel, vous allez apprendre à intégrer Thoughtworks Mingle à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea8df-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea8df-105">L’intégration de Thoughtworks Mingle à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ea8df-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea8df-106">Dans Azure AD, vous pouvez contrôler qui a accès à Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="ea8df-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Thoughtworks Mingle (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea8df-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea8df-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea8df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea8df-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea8df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea8df-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ea8df-110">Prerequisites</span></span>

<span data-ttu-id="ea8df-111">Pour configurer l’intégration d’Azure AD à Thoughtworks Mingle, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ea8df-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="ea8df-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea8df-113">Un abonnement Thoughtworks Mingle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ea8df-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea8df-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ea8df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea8df-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea8df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea8df-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea8df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea8df-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea8df-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea8df-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ea8df-118">Scenario description</span></span>
<span data-ttu-id="ea8df-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ea8df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea8df-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea8df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea8df-121">Ajout de Thoughtworks Mingle à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ea8df-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="ea8df-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="ea8df-123">Ajout de Thoughtworks Mingle à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ea8df-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="ea8df-124">Pour configurer l’intégration de Thoughtworks Mingle à Azure AD, vous devez ajouter Thoughtworks Mingle depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ea8df-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea8df-125">**Pour ajouter Thoughtworks Mingle à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea8df-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea8df-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="ea8df-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea8df-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="ea8df-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ea8df-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="ea8df-133">Dans la zone de recherche, tapez **Thoughtworks Mingle**, sélectionnez **Thoughtworks Mingle** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ea8df-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![Thoughtworks Mingle dans la liste des résultats](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ea8df-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8df-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ea8df-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Thoughtworks Mingle avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ea8df-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea8df-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur de Thoughtworks Mingle équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea8df-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="ea8df-138">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur de Thoughtworks Mingle associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ea8df-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="ea8df-139">Dans Thoughtworks Mingle, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ea8df-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ea8df-140">Pour configurer et tester l’authentification unique Azure AD avec Thoughtworks Mingle, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea8df-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea8df-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ea8df-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea8df-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea8df-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea8df-143">**[Créer un utilisateur de test Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)** pour avoir un équivalent de Britta Simon dans Thoughtworks Mingle lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="ea8df-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea8df-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea8df-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea8df-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ea8df-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ea8df-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8df-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ea8df-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="ea8df-148">**Pour configurer l’authentification unique Azure AD avec Thoughtworks Mingle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea8df-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="ea8df-149">Dans le portail Azure, dans la page d’intégration de l’application **Thoughtworks Mingle**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ea8df-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ea8df-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="ea8df-153">Dans la section **Domaine et URL Thoughtworks Mingle**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea8df-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="ea8df-155">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="ea8df-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea8df-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-156">The value is not real.</span></span> <span data-ttu-id="ea8df-157">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="ea8df-158">Pour obtenir cette valeur, contactez [l’équipe de support technique Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support).</span><span class="sxs-lookup"><span data-stu-id="ea8df-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="ea8df-159">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ea8df-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="ea8df-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ea8df-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea8df-163">Connectez-vous à votre site d’entreprise **Thoughtworks Mingle** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ea8df-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="ea8df-164">Cliquez sur l’onglet **Admin**, puis sur **SSO Config (Configuration SSO)**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="ea8df-165">![Onglet Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuration SSO")</span><span class="sxs-lookup"><span data-stu-id="ea8df-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="ea8df-166">Dans la section **SSO Config** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea8df-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ea8df-167">![Configuration de l’authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ea8df-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="ea8df-168">a.</span><span class="sxs-lookup"><span data-stu-id="ea8df-168">a.</span></span> <span data-ttu-id="ea8df-169">Pour charger le fichier de métadonnées, cliquez sur **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="ea8df-170">b.</span><span class="sxs-lookup"><span data-stu-id="ea8df-170">b.</span></span> <span data-ttu-id="ea8df-171">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ea8df-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ea8df-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea8df-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ea8df-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea8df-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea8df-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ea8df-175">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8df-175">Create an Azure AD test user</span></span>
<span data-ttu-id="ea8df-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ea8df-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="ea8df-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea8df-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea8df-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea8df-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea8df-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ea8df-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea8df-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea8df-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea8df-187">a.</span><span class="sxs-lookup"><span data-stu-id="ea8df-187">a.</span></span> <span data-ttu-id="ea8df-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea8df-189">b.</span><span class="sxs-lookup"><span data-stu-id="ea8df-189">b.</span></span> <span data-ttu-id="ea8df-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea8df-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea8df-191">c.</span><span class="sxs-lookup"><span data-stu-id="ea8df-191">c.</span></span> <span data-ttu-id="ea8df-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea8df-193">d.</span><span class="sxs-lookup"><span data-stu-id="ea8df-193">d.</span></span> <span data-ttu-id="ea8df-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="ea8df-195">Créer un utilisateur de test Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="ea8df-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="ea8df-196">Pour que les utilisateurs Azure AD puissent se connecter, ils doivent être approvisionnés dans l’application Thoughtworks Mingle à l’aide de leurs noms d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea8df-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="ea8df-197">Dans le cas de Thoughtworks Mingle, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="ea8df-198">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea8df-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ea8df-199">Connectez-vous à votre site d’entreprise Thoughtworks Mingle en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ea8df-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="ea8df-200">Cliquez sur **Profile**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="ea8df-201">![Votre premier projet](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Votre premier projet")</span><span class="sxs-lookup"><span data-stu-id="ea8df-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="ea8df-202">Cliquez sur l’onglet **Admin**, puis sur **Users (Utilisateurs)**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="ea8df-203">![Utilisateurs](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="ea8df-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="ea8df-204">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-204">Click **New User**.</span></span>
   
    <span data-ttu-id="ea8df-205">![Nouvel utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="ea8df-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="ea8df-206">Dans la boîte de dialogue **New User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea8df-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="ea8df-207">![Boîte de dialogue Nouvel utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="ea8df-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="ea8df-208">a.</span><span class="sxs-lookup"><span data-stu-id="ea8df-208">a.</span></span> <span data-ttu-id="ea8df-209">Renseignez les zones de texte **Sign-in name** (Nom de connexion), **Display name** (Nom d’affichage), **Choose password** (Choisir le mot de passe) et **Confirm password** (Confirmer le mot de passe) du compte Azure AD valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="ea8df-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="ea8df-210">b.</span><span class="sxs-lookup"><span data-stu-id="ea8df-210">b.</span></span> <span data-ttu-id="ea8df-211">Dans **User type (Type d’utilisateur)**, sélectionnez **Full user (Utilisateur complet)**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="ea8df-212">c.</span><span class="sxs-lookup"><span data-stu-id="ea8df-212">c.</span></span> <span data-ttu-id="ea8df-213">Cliquez sur **Create This Profile**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="ea8df-214">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur, fourni par Thoughtworks Mingle, pour approvisionner des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="ea8df-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ea8df-215">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8df-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="ea8df-216">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="ea8df-218">**Pour affecter Britta Simon à Thoughtworks Mingle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea8df-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="ea8df-219">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ea8df-221">Dans la liste des applications, sélectionnez **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![Lien Thoughtworks Mingle dans la liste des applications](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="ea8df-223">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="ea8df-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-225">Click **Add** button.</span></span> <span data-ttu-id="ea8df-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="ea8df-228">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ea8df-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea8df-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea8df-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ea8df-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ea8df-231">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ea8df-231">Test single sign-on</span></span>

<span data-ttu-id="ea8df-232">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ea8df-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ea8df-233">Si vous cliquez sur la vignette Thoughtworks Mingledans le volet d’accès, vous devez vous connecter automatiquement à votre application Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ea8df-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea8df-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ea8df-234">Additional resources</span></span>

* [<span data-ttu-id="ea8df-235">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea8df-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea8df-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ea8df-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

