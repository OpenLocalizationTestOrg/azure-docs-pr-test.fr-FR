---
title: "Didacticiel : Intégration d’Azure Active Directory à Asset Bank | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Asset Bank."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="d6238-103">Didacticiel : Intégration d’Azure Active Directory à Asset Bank</span><span class="sxs-lookup"><span data-stu-id="d6238-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="d6238-104">Dans ce didacticiel, vous allez apprendre à intégrer Asset Bank à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6238-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6238-105">L’intégration de Asset Bank à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d6238-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6238-106">Dans Azure AD, vous pouvez contrôler qui a accès à Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="d6238-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="d6238-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Asset Bank (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6238-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6238-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6238-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6238-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6238-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6238-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6238-110">Prerequisites</span></span>

<span data-ttu-id="d6238-111">Pour configurer l’intégration d’Azure AD à Asset Bank, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d6238-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="d6238-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6238-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6238-113">Un abonnement Asset Bank pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d6238-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6238-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d6238-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6238-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d6238-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6238-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d6238-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6238-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6238-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6238-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d6238-118">Scenario description</span></span>
<span data-ttu-id="d6238-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d6238-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6238-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6238-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6238-121">Ajout d’Asset Bank à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d6238-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="d6238-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6238-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="d6238-123">Ajout d’Asset Bank à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d6238-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="d6238-124">Pour configurer l’intégration d’Asset Bank à Azure AD, vous devez ajouter Asset Bank, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d6238-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6238-125">**Pour ajouter Asset Bank à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6238-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6238-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6238-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6238-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d6238-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6238-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d6238-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d6238-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d6238-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d6238-133">Dans la zone de recherche, tapez **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="d6238-133">In the search box, type **Asset Bank**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="d6238-135">Dans le panneau de résultats, sélectionnez **Asset Bank**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d6238-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6238-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6238-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6238-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Asset Bank avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d6238-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6238-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur Asset Bank correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6238-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="d6238-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Asset Bank associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d6238-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="d6238-141">Dans Asset Bank, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d6238-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6238-142">Pour configurer et tester l’authentification unique Azure AD avec Asset Bank, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6238-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6238-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d6238-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6238-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6238-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6238-145">**[Création d’un utilisateur de test Asset Bank](#creating-an-asset-bank-test-user)** pour avoir un équivalent de Britta Simon dans Asset Bank lié à sa représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d6238-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6238-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6238-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6238-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d6238-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6238-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6238-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6238-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="d6238-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="d6238-150">**Pour configurer l’authentification unique Azure AD avec Asset Bank, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6238-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="d6238-151">Dans le portail Azure, dans la page d’intégration de l’application **Asset Bank**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d6238-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d6238-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d6238-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="d6238-155">Dans la section **Domaine et URL Asset Bank**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6238-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="d6238-157">a.</span><span class="sxs-lookup"><span data-stu-id="d6238-157">a.</span></span> <span data-ttu-id="d6238-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="d6238-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="d6238-159">b.</span><span class="sxs-lookup"><span data-stu-id="d6238-159">b.</span></span> <span data-ttu-id="d6238-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="d6238-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6238-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d6238-161">These values are not real.</span></span> <span data-ttu-id="d6238-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="d6238-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d6238-163">Pour obtenir ces valeurs, contactez [l’équipe du support Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="d6238-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="d6238-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d6238-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="d6238-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d6238-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6238-168">Pour configurer l’authentification unique côté **Asset Bank**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à [l’équipe du support Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="d6238-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="d6238-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d6238-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6238-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d6238-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6238-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6238-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6238-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6238-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6238-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d6238-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d6238-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6238-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6238-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6238-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6238-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d6238-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6238-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d6238-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6238-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6238-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6238-184">a.</span><span class="sxs-lookup"><span data-stu-id="d6238-184">a.</span></span> <span data-ttu-id="d6238-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6238-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6238-186">b.</span><span class="sxs-lookup"><span data-stu-id="d6238-186">b.</span></span> <span data-ttu-id="d6238-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6238-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6238-188">c.</span><span class="sxs-lookup"><span data-stu-id="d6238-188">c.</span></span> <span data-ttu-id="d6238-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d6238-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6238-190">d.</span><span class="sxs-lookup"><span data-stu-id="d6238-190">d.</span></span> <span data-ttu-id="d6238-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6238-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="d6238-192">Création d’un utilisateur de test Asset Bank</span><span class="sxs-lookup"><span data-stu-id="d6238-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="d6238-193">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="d6238-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="d6238-194">Asset Bank prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="d6238-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d6238-195">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d6238-195">There is no action item for you in this section.</span></span> <span data-ttu-id="d6238-196">Un utilisateur est créé lors d’une tentative d’accès à Asset Bank s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="d6238-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="d6238-197">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="d6238-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6238-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6238-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6238-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="d6238-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d6238-201">**Pour affecter Britta Simon à Asset Bank, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6238-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="d6238-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d6238-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d6238-204">Dans la liste des applications, sélectionnez **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="d6238-204">In the applications list, select **Asset Bank**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="d6238-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6238-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d6238-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d6238-208">Click **Add** button.</span></span> <span data-ttu-id="d6238-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d6238-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d6238-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d6238-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6238-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6238-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6238-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d6238-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6238-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d6238-214">Testing single sign-on</span></span>

<span data-ttu-id="d6238-215">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d6238-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6238-216">Lorsque vous cliquez sur la vignette Asset Bank dans le volet d’accès, vous devez être connecté automatiquement à votre application Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="d6238-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d6238-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d6238-217">Additional resources</span></span>

* [<span data-ttu-id="d6238-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6238-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6238-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d6238-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

