---
title: "Didacticiel : Intégration d’Azure Active Directory à BC in the Cloud | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BC in the Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: ebc95d600eca1027331cd92cfe481d0c3ee833a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-the-cloud"></a><span data-ttu-id="fe838-103">Didacticiel : Intégration d’Azure Active Directory à BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="fe838-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span></span>

<span data-ttu-id="fe838-104">Dans ce didacticiel, vous allez apprendre à intégrer BC in the Cloud à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe838-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe838-105">L’intégration de BC in the Cloud à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fe838-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fe838-106">Dans Azure AD, vous pouvez contrôler qui a accès à BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe838-106">You can control in Azure AD who has access to BC in the Cloud</span></span>
- <span data-ttu-id="fe838-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à BC in the Cloud (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe838-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fe838-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="fe838-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fe838-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe838-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe838-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fe838-110">Prerequisites</span></span>

<span data-ttu-id="fe838-111">Pour configurer l’intégration d’Azure AD à BC in the Cloud, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fe838-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span></span>

- <span data-ttu-id="fe838-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe838-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe838-113">Un abonnement BC in the Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fe838-113">A BC in the Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe838-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fe838-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe838-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fe838-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe838-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fe838-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe838-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe838-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe838-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fe838-118">Scenario description</span></span>
<span data-ttu-id="fe838-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fe838-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe838-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe838-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe838-121">Ajout de BC in the Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fe838-121">Adding BC in the Cloud from the gallery</span></span>
2. <span data-ttu-id="fe838-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe838-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-the-cloud-from-the-gallery"></a><span data-ttu-id="fe838-123">Ajout de BC in the Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fe838-123">Adding BC in the Cloud from the gallery</span></span>
<span data-ttu-id="fe838-124">Pour configurer l’intégration de BC in the Cloud à Azure AD, vous devez ajouter BC in the Cloud de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fe838-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fe838-125">**Pour ajouter BC in the Cloud à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="fe838-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fe838-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe838-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fe838-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fe838-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fe838-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fe838-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fe838-131">Pour ajouter l’application, cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fe838-131">To add new application, click **Add** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fe838-133">Dans la zone de recherche, tapez **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="fe838-133">In the search box, type **BC in the Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="fe838-135">Dans le volet de résultats, sélectionnez **BC in the Cloud**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="fe838-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fe838-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe838-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fe838-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BC in the Cloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fe838-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fe838-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur BC in the Cloud correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe838-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="fe838-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur BC in the Cloud associé.</span><span class="sxs-lookup"><span data-stu-id="fe838-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span></span>

<span data-ttu-id="fe838-141">Dans BC in the Cloud, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="fe838-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fe838-142">Pour configurer et tester l’authentification unique avec Azure AD avec BC in the Cloud, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe838-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fe838-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fe838-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fe838-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe838-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe838-145">**[Création d’un utilisateur de test BC in the Cloud](#creating-a-bc-in-the-cloud-test-user)** pour avoir un équivalent de Britta Simon dans BC in the Cloud lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="fe838-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe838-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe838-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe838-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="fe838-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fe838-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe838-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fe838-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe838-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span></span>

<span data-ttu-id="fe838-150">**Pour configurer l’authentification unique Azure AD avec BC in the Cloud, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="fe838-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="fe838-151">Dans le portail Azure, dans la page d’intégration de l’application **BC in the Cloud**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fe838-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fe838-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fe838-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="fe838-155">Dans la section **Domaine et URL BC in the Cloud**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe838-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="fe838-157">a.</span><span class="sxs-lookup"><span data-stu-id="fe838-157">a.</span></span> <span data-ttu-id="fe838-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="fe838-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="fe838-159">b.</span><span class="sxs-lookup"><span data-stu-id="fe838-159">b.</span></span> <span data-ttu-id="fe838-160">Dans la zone de texte **Identificateur**, entrez une URL telle que celle-ci : `https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="fe838-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fe838-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="fe838-161">This value is not real.</span></span> <span data-ttu-id="fe838-162">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="fe838-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fe838-163">Pour obtenir cette valeur, contactez [l’équipe du support BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="fe838-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span></span> 
 
4. <span data-ttu-id="fe838-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fe838-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="fe838-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fe838-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fe838-168">Pour configurer l’authentification unique côté **BC in the Cloud**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe du support BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="fe838-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="fe838-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="fe838-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fe838-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="fe838-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fe838-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe838-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fe838-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe838-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="fe838-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fe838-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fe838-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fe838-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fe838-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe838-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fe838-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fe838-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fe838-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fe838-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fe838-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe838-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fe838-184">a.</span><span class="sxs-lookup"><span data-stu-id="fe838-184">a.</span></span> <span data-ttu-id="fe838-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe838-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe838-186">b.</span><span class="sxs-lookup"><span data-stu-id="fe838-186">b.</span></span> <span data-ttu-id="fe838-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe838-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fe838-188">c.</span><span class="sxs-lookup"><span data-stu-id="fe838-188">c.</span></span> <span data-ttu-id="fe838-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fe838-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fe838-190">d.</span><span class="sxs-lookup"><span data-stu-id="fe838-190">d.</span></span> <span data-ttu-id="fe838-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fe838-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-the-cloud-test-user"></a><span data-ttu-id="fe838-192">Création d’un utilisateur de test BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="fe838-192">Creating a BC in the Cloud test user</span></span>

<span data-ttu-id="fe838-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe838-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span></span> <span data-ttu-id="fe838-194">Pour ajouter les utilisateurs dans l’application BC in the Cloud, contactez [l’équipe du support BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="fe838-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span></span> <span data-ttu-id="fe838-195">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fe838-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fe838-196">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe838-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fe838-197">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe838-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fe838-199">**Pour attribuer Britta Simon à BC in the Cloud, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="fe838-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="fe838-200">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fe838-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fe838-202">Dans la liste des applications, sélectionnez **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="fe838-202">In the applications list, select **BC in the Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="fe838-204">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fe838-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fe838-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fe838-206">Click **Add** button.</span></span> <span data-ttu-id="fe838-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fe838-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fe838-209">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fe838-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fe838-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fe838-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe838-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fe838-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fe838-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fe838-212">Testing single sign-on</span></span>

<span data-ttu-id="fe838-213">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="fe838-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

 <span data-ttu-id="fe838-214">Lorsque vous cliquez sur la vignette BC in the Cloud dans le volet d’accès, vous devez être connecté automatiquement à votre application BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe838-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span></span> <span data-ttu-id="fe838-215">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe838-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe838-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fe838-216">Additional resources</span></span>

* [<span data-ttu-id="fe838-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe838-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe838-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fe838-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

