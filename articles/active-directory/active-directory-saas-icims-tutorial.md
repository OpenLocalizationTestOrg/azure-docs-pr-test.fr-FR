---
title: "Didacticiel : intégration d’Azure Active Directory à ICIMS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="8fedd-103">Didacticiel : intégration d’Azure Active Directory à ICIMS</span><span class="sxs-lookup"><span data-stu-id="8fedd-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="8fedd-104">Dans ce didacticiel, vous allez apprendre à intégrer ICIMS dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fedd-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fedd-105">L’intégration d’ICIMS dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8fedd-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8fedd-106">Dans Azure AD, vous pouvez contrôler qui a accès à ICIMS.</span><span class="sxs-lookup"><span data-stu-id="8fedd-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="8fedd-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à ICIMS (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fedd-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8fedd-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8fedd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8fedd-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fedd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fedd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8fedd-110">Prerequisites</span></span>

<span data-ttu-id="8fedd-111">Pour configurer l’intégration d’Azure AD avec ICIMS, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8fedd-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="8fedd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fedd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fedd-113">Un abonnement ICIMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8fedd-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8fedd-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8fedd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8fedd-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8fedd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fedd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8fedd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fedd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fedd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fedd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8fedd-118">Scenario description</span></span>
<span data-ttu-id="8fedd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8fedd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fedd-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fedd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fedd-121">Ajout d’ICIMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8fedd-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="8fedd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fedd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="8fedd-123">Ajout d’ICIMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8fedd-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="8fedd-124">Pour configurer l’intégration d’ICIMS avec Azure AD, vous devez ajouter ICIMS à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8fedd-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8fedd-125">**Pour ajouter ICIMS à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8fedd-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8fedd-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="8fedd-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8fedd-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="8fedd-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8fedd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="8fedd-133">Dans la zone de recherche, tapez **ICIMS**, sélectionnez **ICIMS** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8fedd-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![ICIMS dans la liste des résultats](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8fedd-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fedd-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8fedd-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ICIMS, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8fedd-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8fedd-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ICIMS équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fedd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="8fedd-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur ICIMS associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8fedd-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="8fedd-139">Dans ICIMS, assignez la valeur du **nom d’utilisateur** d’Azure AD comme valeur de **Username** (Nom d’utilisateur) pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8fedd-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8fedd-140">Pour configurer et tester l’authentification unique Azure AD avec ICIMS, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fedd-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8fedd-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8fedd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8fedd-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fedd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fedd-143">**[Créer un utilisateur de test ICIMS](#create-an-icims-test-user)** pour avoir dans ICIMS un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="8fedd-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fedd-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fedd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fedd-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8fedd-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8fedd-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fedd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8fedd-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ICIMS.</span><span class="sxs-lookup"><span data-stu-id="8fedd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="8fedd-148">**Pour configurer l’authentification unique Azure AD avec ICIMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8fedd-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="8fedd-149">Dans le portail Azure, dans la page d’intégration de l’application **ICIMS**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8fedd-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8fedd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="8fedd-153">Dans la section **ICIMS Domain and URLs** (Domaine et URL ICIMS), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8fedd-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans ICIMS Domain and URLs (Domaine et URL ICIMS)](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="8fedd-155">a.</span><span class="sxs-lookup"><span data-stu-id="8fedd-155">a.</span></span> <span data-ttu-id="8fedd-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="8fedd-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="8fedd-157">b.</span><span class="sxs-lookup"><span data-stu-id="8fedd-157">b.</span></span> <span data-ttu-id="8fedd-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="8fedd-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fedd-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8fedd-159">These values are not real.</span></span> <span data-ttu-id="8fedd-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="8fedd-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8fedd-161">Pour obtenir ces valeurs, contactez l’[équipe de support client ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8fedd-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="8fedd-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8fedd-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="8fedd-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8fedd-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8fedd-166">Dans la section **ICIMS Configuration** (Configuration d’ICIMS), cliquez sur **Configure ICIMS** (Configurer ICIMS) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8fedd-167">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8fedd-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration d’ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="8fedd-169">Pour configurer l’authentification unique côté **ICIMS**, vous devez envoyer le **XML des métadonnées** téléchargé, **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à l’[équipe de support ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8fedd-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="8fedd-170">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="8fedd-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8fedd-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8fedd-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8fedd-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8fedd-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8fedd-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8fedd-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8fedd-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fedd-174">Create an Azure AD test user</span></span>
<span data-ttu-id="8fedd-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8fedd-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="8fedd-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8fedd-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8fedd-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8fedd-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8fedd-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8fedd-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8fedd-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8fedd-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8fedd-186">a.</span><span class="sxs-lookup"><span data-stu-id="8fedd-186">a.</span></span> <span data-ttu-id="8fedd-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fedd-188">b.</span><span class="sxs-lookup"><span data-stu-id="8fedd-188">b.</span></span> <span data-ttu-id="8fedd-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fedd-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8fedd-190">c.</span><span class="sxs-lookup"><span data-stu-id="8fedd-190">c.</span></span> <span data-ttu-id="8fedd-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8fedd-192">d.</span><span class="sxs-lookup"><span data-stu-id="8fedd-192">d.</span></span> <span data-ttu-id="8fedd-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="8fedd-194">Créer un utilisateur de test ICIMS</span><span class="sxs-lookup"><span data-stu-id="8fedd-194">Create an ICIMS test user</span></span>

<span data-ttu-id="8fedd-195">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans ICIMS.</span><span class="sxs-lookup"><span data-stu-id="8fedd-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="8fedd-196">Pour ajouter des utilisateurs dans le compte ICIMS, contactez l’[équipe de support ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8fedd-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8fedd-197">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fedd-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="8fedd-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ICIMS.</span><span class="sxs-lookup"><span data-stu-id="8fedd-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![Attribuer le rôle d’utilisateur][200]

<span data-ttu-id="8fedd-200">**Pour affecter Britta Simon à ICIMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8fedd-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="8fedd-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8fedd-203">Dans la liste des applications, sélectionnez **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-203">In the applications list, select **ICIMS**.</span></span>

    ![Lien ICIMS dans la liste des applications](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="8fedd-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="8fedd-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-207">Click **Add** button.</span></span> <span data-ttu-id="8fedd-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="8fedd-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8fedd-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8fedd-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fedd-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8fedd-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8fedd-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8fedd-213">Test single sign-on</span></span>

<span data-ttu-id="8fedd-214">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8fedd-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="8fedd-215">Lorsque vous cliquez sur la vignette ICIMS dans le volet d’accès, vous devez être connecté automatiquement à votre application ICIMS.</span><span class="sxs-lookup"><span data-stu-id="8fedd-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fedd-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8fedd-216">Additional resources</span></span>

* [<span data-ttu-id="8fedd-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fedd-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fedd-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8fedd-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

