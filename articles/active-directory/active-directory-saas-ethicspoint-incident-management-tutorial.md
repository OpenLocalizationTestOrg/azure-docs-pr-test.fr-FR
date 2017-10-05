---
title: "Didacticiel : Intégration d’Azure Active Directory avec EthicsPoint Incident Management (EPIM) | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et EthicsPoint Incident Management (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: b5ac3afd973b5765ba151e766754934b49ac0e0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="42819-103">Didacticiel : Intégration d’Azure Active Directory avec EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="42819-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="42819-104">Dans ce didacticiel, vous allez apprendre à intégrer EthicsPoint Incident Management (EPIM) à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42819-104">In this tutorial, you learn how to integrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42819-105">L’intégration dEthicsPoint Incident Management (EPIM) avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="42819-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42819-106">Vous pouvez contrôler dans Azure AD qui a accès à EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="42819-106">You can control in Azure AD who has access to EthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="42819-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à EthicsPoint Incident Management (EPIM) (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-107">You can enable your users to automatically get signed-on to EthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42819-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="42819-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42819-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42819-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42819-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="42819-110">Prerequisites</span></span>

<span data-ttu-id="42819-111">Pour configurer l’intégration d’Azure AD à EthicsPoint Incident Management (EPIM), vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="42819-111">To configure Azure AD integration with EthicsPoint Incident Management (EPIM), you need the following items:</span></span>

- <span data-ttu-id="42819-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42819-113">Un abonnement EthicsPoint Incident Management (EPIM) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="42819-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42819-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="42819-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42819-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="42819-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42819-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42819-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42819-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42819-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42819-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="42819-118">Scenario description</span></span>
<span data-ttu-id="42819-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="42819-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42819-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="42819-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42819-121">Ajout d’EthicsPoint Incident Management (EPIM) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="42819-121">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
2. <span data-ttu-id="42819-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-the-gallery"></a><span data-ttu-id="42819-123">Ajout d’EthicsPoint Incident Management (EPIM) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="42819-123">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
<span data-ttu-id="42819-124">Pour configurer l’intégration d’EthicsPoint Incident Management (EPIM) avec Azure AD, vous devez ajouter EthicsPoint Incident Management (EPIM), à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="42819-124">To configure the integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need to add EthicsPoint Incident Management (EPIM) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42819-125">**Pour ajouter EthicsPoint Incident Management (EPIM) à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42819-125">**To add EthicsPoint Incident Management (EPIM) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42819-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42819-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42819-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="42819-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42819-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42819-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="42819-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42819-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="42819-133">Dans la zone de recherche, tapez **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="42819-133">In the search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="42819-135">Dans le volet des résultats, sélectionnez **EthicsPoint Incident Management (EPIM)**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="42819-135">In the results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42819-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42819-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec EthicsPoint Incident Management (EPIM) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="42819-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42819-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur EthicsPoint Incident Management (EPIM) équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42819-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EthicsPoint Incident Management (EPIM) is to a user in Azure AD.</span></span> <span data-ttu-id="42819-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur EthicsPoint Incident Management (EPIM) associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="42819-140">In other words, a link relationship between an Azure AD user and the related user in EthicsPoint Incident Management (EPIM) needs to be established.</span></span>

<span data-ttu-id="42819-141">Dans EthicsPoint Incident Management (EPIM), assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="42819-141">In EthicsPoint Incident Management (EPIM), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42819-142">Pour configurer et tester l’authentification unique Azure AD avec EthicsPoint Incident Management (EPIM), vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="42819-142">To configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42819-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="42819-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42819-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42819-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42819-145">**[Création d’un utilisateur de test EthicsPoint Incident Management (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)** pour avoir un équivalent de Britta Simon dans EthicsPoint Incident Management (EPIM) lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="42819-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - to have a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42819-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42819-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42819-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="42819-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42819-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42819-149">Dans cette section, vous allez activer l’authentification unique Azure AD sur le portail Azure et configurer l’authentification unique dans votre application EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="42819-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="42819-150">**Pour configurer l’authentification unique Azure AD avec EthicsPoint Incident Management (EPIM), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42819-150">**To configure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="42819-151">Sur le portail Azure, à la page d’intégration de l’application **EthicsPoint Incident Management (EPIM)**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="42819-151">In the Azure portal, on the **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="42819-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42819-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="42819-155">Dans la section **Domaine et URL EthicsPoint Incident Management (EPIM)**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="42819-155">On the **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="42819-157">a.</span><span class="sxs-lookup"><span data-stu-id="42819-157">a.</span></span> <span data-ttu-id="42819-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="42819-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="42819-159">b.</span><span class="sxs-lookup"><span data-stu-id="42819-159">b.</span></span> <span data-ttu-id="42819-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="42819-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="42819-161">c.</span><span class="sxs-lookup"><span data-stu-id="42819-161">c.</span></span> <span data-ttu-id="42819-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="42819-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42819-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="42819-163">These values are not real.</span></span> <span data-ttu-id="42819-164">Mettez à jour ces valeurs avec l’URL de réponse, l’identificateur et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="42819-164">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="42819-165">Pour obtenir ces valeurs, contactez [l’équipe de prise en charge des clients EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="42819-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="42819-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="42819-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="42819-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="42819-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="42819-170">Pour configurer l’authentification unique du côté d’**EthicsPoint Incident Management (EPIM)**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à l’[équipe de support technique d’EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="42819-170">To configure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need to send the downloaded **Metadata XML** to [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="42819-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="42819-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42819-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="42819-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42819-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42819-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42819-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="42819-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42819-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="42819-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42819-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42819-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42819-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42819-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42819-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42819-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42819-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42819-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="42819-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42819-186">a.</span><span class="sxs-lookup"><span data-stu-id="42819-186">a.</span></span> <span data-ttu-id="42819-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42819-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42819-188">b.</span><span class="sxs-lookup"><span data-stu-id="42819-188">b.</span></span> <span data-ttu-id="42819-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42819-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42819-190">c.</span><span class="sxs-lookup"><span data-stu-id="42819-190">c.</span></span> <span data-ttu-id="42819-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="42819-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42819-192">d.</span><span class="sxs-lookup"><span data-stu-id="42819-192">d.</span></span> <span data-ttu-id="42819-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="42819-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="42819-194">Création d’un utilisateur de test d’EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="42819-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="42819-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="42819-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="42819-196">Travaillez avec l’[équipe de support technique d’EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us) pour ajouter les utilisateurs dans la plateforme EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="42819-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) to add the users in the EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42819-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42819-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42819-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="42819-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EthicsPoint Incident Management (EPIM).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="42819-200">**Pour affecter Britta Simon à EthicsPoint Incident Management (EPIM), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42819-200">**To assign Britta Simon to EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="42819-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42819-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="42819-203">Dans la liste des applications, sélectionnez **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="42819-203">In the applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="42819-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42819-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="42819-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="42819-207">Click **Add** button.</span></span> <span data-ttu-id="42819-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42819-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="42819-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="42819-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42819-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42819-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42819-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42819-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42819-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="42819-213">Testing single sign-on</span></span>

<span data-ttu-id="42819-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="42819-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="42819-215">Lorsque vous cliquez sur la mosaïque EthicsPoint Incident Management (EPIM) dans le volet d’accès, vous devez être connecté automatiquement à votre application EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="42819-215">When you click the EthicsPoint Incident Management (EPIM) tile in the Access Panel, you should get automatically signed-on to your EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42819-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="42819-216">Additional resources</span></span>

* [<span data-ttu-id="42819-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42819-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42819-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="42819-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

