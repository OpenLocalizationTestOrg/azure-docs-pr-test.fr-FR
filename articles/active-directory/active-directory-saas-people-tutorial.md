---
title: "Didacticiel : Intégration d’Azure Active Directory à People | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et People."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="14202-103">Didacticiel : Intégration d’Azure Active Directory à People</span><span class="sxs-lookup"><span data-stu-id="14202-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="14202-104">Dans ce didacticiel, vous allez apprendre à intégrer People à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14202-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14202-105">L’intégration de People à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="14202-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14202-106">Dans Azure AD, vous pouvez contrôler qui a accès à People</span><span class="sxs-lookup"><span data-stu-id="14202-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="14202-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à People (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14202-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14202-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="14202-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="14202-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14202-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14202-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="14202-110">Prerequisites</span></span>

<span data-ttu-id="14202-111">Pour configurer l’intégration d’Azure AD à People, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="14202-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="14202-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="14202-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14202-113">Un abonnement People pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="14202-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14202-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="14202-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14202-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="14202-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14202-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="14202-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14202-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14202-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14202-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="14202-118">Scenario description</span></span>
<span data-ttu-id="14202-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="14202-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14202-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="14202-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14202-121">Ajout de People à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="14202-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="14202-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="14202-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="14202-123">Ajout de People à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="14202-123">Adding People from the gallery</span></span>
<span data-ttu-id="14202-124">Pour configurer l’intégration de People à Azure AD, vous devez ajouter People, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="14202-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14202-125">**Pour ajouter People à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="14202-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14202-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14202-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14202-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="14202-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14202-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="14202-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="14202-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="14202-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="14202-133">Dans la zone de recherche, tapez **People**.</span><span class="sxs-lookup"><span data-stu-id="14202-133">In the search box, type **People**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="14202-135">Dans le panneau des résultats, sélectionnez **People**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="14202-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14202-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="14202-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14202-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec People avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="14202-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14202-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur People équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14202-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="14202-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur People associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="14202-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="14202-141">Dans People, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="14202-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="14202-142">Pour configurer et tester l’authentification unique Azure AD avec People, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="14202-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14202-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="14202-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="14202-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14202-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14202-145">**[Création d’un utilisateur de test People](#creating-a-people-test-user)** pour obtenir un équivalent de Britta Simon dans People lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="14202-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="14202-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14202-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14202-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="14202-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14202-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="14202-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14202-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application People.</span><span class="sxs-lookup"><span data-stu-id="14202-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="14202-150">**Pour configurer l’authentification unique Azure AD avec People, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="14202-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="14202-151">Dans le Portail Azure, sur la page d’intégration de l’application **People**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="14202-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="14202-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="14202-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="14202-155">Dans la section **Domaine et URL People**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="14202-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="14202-157">a.</span><span class="sxs-lookup"><span data-stu-id="14202-157">a.</span></span> <span data-ttu-id="14202-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="14202-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="14202-159">b.</span><span class="sxs-lookup"><span data-stu-id="14202-159">b.</span></span> <span data-ttu-id="14202-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="14202-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="14202-161">c.</span><span class="sxs-lookup"><span data-stu-id="14202-161">c.</span></span> <span data-ttu-id="14202-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="14202-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14202-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="14202-163">These values are not real.</span></span> <span data-ttu-id="14202-164">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="14202-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="14202-165">Pour obtenir ces valeurs, contactez l’[équipe du support technique People](mailto:customerservices@peoplehr.com).</span><span class="sxs-lookup"><span data-stu-id="14202-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="14202-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14202-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="14202-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="14202-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="14202-170">Pour que l’authentification unique soit configurée pour votre application, vous devez vous connecter à votre locataire People en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="14202-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="14202-171">Dans le menu sur le côté gauche, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="14202-171">In the menu on the left side, click **Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="14202-173">Cliquez sur **Company**.</span><span class="sxs-lookup"><span data-stu-id="14202-173">Click **Company**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="14202-175">Dans **Importer le fichier de métadonnées SAML « Authentification unique »**, cliquez sur **Parcourir** pour importer le fichier de métadonnées téléchargé.</span><span class="sxs-lookup"><span data-stu-id="14202-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="14202-177">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="14202-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14202-178">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="14202-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14202-179">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14202-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14202-180">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="14202-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="14202-181">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="14202-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="14202-183">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="14202-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14202-184">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14202-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14202-186">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="14202-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14202-188">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="14202-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14202-190">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="14202-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14202-192">a.</span><span class="sxs-lookup"><span data-stu-id="14202-192">a.</span></span> <span data-ttu-id="14202-193">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14202-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14202-194">b.</span><span class="sxs-lookup"><span data-stu-id="14202-194">b.</span></span> <span data-ttu-id="14202-195">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14202-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14202-196">c.</span><span class="sxs-lookup"><span data-stu-id="14202-196">c.</span></span> <span data-ttu-id="14202-197">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="14202-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="14202-198">d.</span><span class="sxs-lookup"><span data-stu-id="14202-198">d.</span></span> <span data-ttu-id="14202-199">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="14202-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="14202-200">Création d’un utilisateur de test People</span><span class="sxs-lookup"><span data-stu-id="14202-200">Creating a People test user</span></span>

<span data-ttu-id="14202-201">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans People.</span><span class="sxs-lookup"><span data-stu-id="14202-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="14202-202">Collaborez avec l’[équipe du support technique People](mailto:customerservices@peoplehr.com) pour ajouter des utilisateurs dans la plateforme People.</span><span class="sxs-lookup"><span data-stu-id="14202-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="14202-203">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="14202-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="14202-204">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="14202-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="14202-205">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à People.</span><span class="sxs-lookup"><span data-stu-id="14202-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="14202-207">**Pour affecter Britta Simon à People, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="14202-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="14202-208">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="14202-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="14202-210">Dans la liste des applications, sélectionnez **People**.</span><span class="sxs-lookup"><span data-stu-id="14202-210">In the applications list, select **People**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="14202-212">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="14202-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="14202-214">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="14202-214">Click **Add** button.</span></span> <span data-ttu-id="14202-215">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="14202-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="14202-217">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="14202-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="14202-218">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="14202-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14202-219">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="14202-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14202-220">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="14202-220">Testing single sign-on</span></span>

<span data-ttu-id="14202-221">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="14202-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="14202-222">Quand vous cliquez sur la vignette People dans le volet d’accès, vous devez être connecté automatiquement à votre application People.</span><span class="sxs-lookup"><span data-stu-id="14202-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14202-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="14202-223">Additional resources</span></span>

* [<span data-ttu-id="14202-224">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14202-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14202-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="14202-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

