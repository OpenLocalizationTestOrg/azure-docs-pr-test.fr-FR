---
title: "Didacticiel : Intégration d’Azure Active Directory à Nomadesk | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Nomadesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 1d652d562f4c5caffded18d928e2395e537f59f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="5564e-103">Didacticiel : Intégration d’Azure Active Directory à Nomadesk</span><span class="sxs-lookup"><span data-stu-id="5564e-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="5564e-104">Dans ce didacticiel, vous allez apprendre à intégrer Nomadesk à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5564e-104">In this tutorial, you learn how to integrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5564e-105">L’intégration de Nomadesk dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5564e-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5564e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="5564e-106">You can control in Azure AD who has access to Nomadesk</span></span>
- <span data-ttu-id="5564e-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Nomadesk (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5564e-107">You can enable your users to automatically get signed-on to Nomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5564e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5564e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5564e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5564e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5564e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5564e-110">Prerequisites</span></span>

<span data-ttu-id="5564e-111">Pour configurer l’intégration d’Azure AD à Nomadesk, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5564e-111">To configure Azure AD integration with Nomadesk, you need the following items:</span></span>

- <span data-ttu-id="5564e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5564e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5564e-113">Un abonnement Nomadesk pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5564e-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5564e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5564e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5564e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5564e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5564e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5564e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5564e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5564e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5564e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5564e-118">Scenario description</span></span>
<span data-ttu-id="5564e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5564e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5564e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5564e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5564e-121">Ajout de Nomadesk depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="5564e-121">Adding Nomadesk from the gallery</span></span>
2. <span data-ttu-id="5564e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5564e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-the-gallery"></a><span data-ttu-id="5564e-123">Ajout de Nomadesk depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="5564e-123">Adding Nomadesk from the gallery</span></span>
<span data-ttu-id="5564e-124">Pour configurer l’intégration de Nomadesk à Azure AD, vous devez ajouter Nomadesk, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5564e-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5564e-125">**Pour ajouter Nomadesk à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5564e-125">**To add Nomadesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5564e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5564e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5564e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5564e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5564e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5564e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5564e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5564e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5564e-133">Dans la zone de recherche, tapez **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="5564e-133">In the search box, type **Nomadesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_search.png)

5. <span data-ttu-id="5564e-135">Dans le panneau des résultats, sélectionnez **Nomadesk**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5564e-135">In the results panel, select **Nomadesk**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5564e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5564e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5564e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Nomadesk, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5564e-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5564e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Nomadesk équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5564e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadesk is to a user in Azure AD.</span></span> <span data-ttu-id="5564e-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Nomadesk associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5564e-140">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span></span>

<span data-ttu-id="5564e-141">Dans Nomadesk, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5564e-141">In Nomadesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5564e-142">Pour configurer et tester l’authentification unique Azure AD avec Nomadesk, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5564e-142">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5564e-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5564e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5564e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5564e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5564e-145">**[Création d’un utilisateur de test Nomadesk](#creating-a-nomadesk-test-user)** pour obtenir un équivalent de Britta Simon dans Nomadesk, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5564e-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5564e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5564e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5564e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5564e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5564e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5564e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5564e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="5564e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="5564e-150">**Pour configurer l’authentification unique Azure AD avec Nomadesk, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5564e-150">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="5564e-151">Dans le portail Azure, sur la page d’intégration de l’application **Nomadesk**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5564e-151">In the Azure portal, on the **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5564e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5564e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

3. <span data-ttu-id="5564e-155">Dans la section **Domaine et URL Nomadesk**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5564e-155">On the **Nomadesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="5564e-157">a.</span><span class="sxs-lookup"><span data-stu-id="5564e-157">a.</span></span> <span data-ttu-id="5564e-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="5564e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="5564e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5564e-159">b.</span></span> <span data-ttu-id="5564e-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="5564e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5564e-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5564e-161">These values are not real.</span></span> <span data-ttu-id="5564e-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5564e-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="5564e-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="5564e-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) to get these values.</span></span> 
 
4. <span data-ttu-id="5564e-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5564e-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

5. <span data-ttu-id="5564e-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5564e-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5564e-168">Dans la section **Configuration de Nomadesk**, cliquez sur **Configurer Nomadesk** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="5564e-168">On the **Nomadesk Configuration** section, click **Configure Nomadesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5564e-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5564e-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_configure.png) 

7. <span data-ttu-id="5564e-171">Pour configurer l’authentification unique côté **Nomadesk**, vous devez envoyer le **Certificat** téléchargé, l’**URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à l’[équipe de support technique Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="5564e-171">To configure single sign-on on **Nomadesk** side, you need to send the downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="5564e-172">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="5564e-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5564e-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5564e-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5564e-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5564e-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5564e-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5564e-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5564e-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5564e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="5564e-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5564e-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5564e-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5564e-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5564e-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5564e-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5564e-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5564e-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5564e-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5564e-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5564e-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5564e-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5564e-188">a.</span><span class="sxs-lookup"><span data-stu-id="5564e-188">a.</span></span> <span data-ttu-id="5564e-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5564e-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5564e-190">b.</span><span class="sxs-lookup"><span data-stu-id="5564e-190">b.</span></span> <span data-ttu-id="5564e-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5564e-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5564e-192">c.</span><span class="sxs-lookup"><span data-stu-id="5564e-192">c.</span></span> <span data-ttu-id="5564e-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5564e-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5564e-194">d.</span><span class="sxs-lookup"><span data-stu-id="5564e-194">d.</span></span> <span data-ttu-id="5564e-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5564e-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="5564e-196">Création d’un utilisateur de test Nomadesk</span><span class="sxs-lookup"><span data-stu-id="5564e-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="5564e-197">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="5564e-197">The objective of this section is to create a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="5564e-198">Nomadesk prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="5564e-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5564e-199">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="5564e-199">There is no action item for you in this section.</span></span> <span data-ttu-id="5564e-200">Un nouvel utilisateur est créé lors d’une tentative d’accès à Nomadesk, s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="5564e-200">A new user is created during an attempt to access Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="5564e-201">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="5564e-201">If you need to create a user manually, you need to contact the [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5564e-202">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5564e-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5564e-203">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="5564e-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5564e-205">**Pour affecter Britta Simon à Nomadesk, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5564e-205">**To assign Britta Simon to Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="5564e-206">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5564e-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5564e-208">Dans la liste des applications, sélectionnez **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="5564e-208">In the applications list, select **Nomadesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_app.png) 

3. <span data-ttu-id="5564e-210">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5564e-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5564e-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5564e-212">Click **Add** button.</span></span> <span data-ttu-id="5564e-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5564e-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5564e-215">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5564e-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5564e-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5564e-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5564e-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5564e-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5564e-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5564e-218">Testing single sign-on</span></span>

<span data-ttu-id="5564e-219">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5564e-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5564e-220">Lorsque vous cliquez sur la vignette Nomadesk dans le panneau d’accès, vous devez êtes automatiquement connecté à votre application Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="5564e-220">When you click the Nomadesk tile in the Access Panel,  you should get automatically signed-on to your Nomadesk application.</span></span>
<span data-ttu-id="5564e-221">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5564e-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5564e-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5564e-222">Additional resources</span></span>

* [<span data-ttu-id="5564e-223">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5564e-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5564e-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5564e-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png

