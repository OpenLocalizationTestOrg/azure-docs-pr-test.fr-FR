---
title: "Didacticiel : Intégration d’Azure Active Directory à Direct | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Direct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 84582492592613320bd3ec2bdffe08519852d7c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="37f3f-103">Didacticiel : Intégration d’Azure Active Directory à Direct</span><span class="sxs-lookup"><span data-stu-id="37f3f-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="37f3f-104">Dans ce didacticiel, vous allez apprendre à intégrer Direct à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37f3f-104">In this tutorial, you learn how to integrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37f3f-105">L’intégration de Direct à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="37f3f-105">Integrating Direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37f3f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Direct.</span><span class="sxs-lookup"><span data-stu-id="37f3f-106">You can control in Azure AD who has access to Direct</span></span>
- <span data-ttu-id="37f3f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Direct (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f3f-107">You can enable your users to automatically get signed-on to Direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37f3f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="37f3f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37f3f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37f3f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37f3f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37f3f-110">Prerequisites</span></span>

<span data-ttu-id="37f3f-111">Pour configurer l’intégration d’Azure AD avec Direct, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="37f3f-111">To configure Azure AD integration with Direct, you need the following items:</span></span>

- <span data-ttu-id="37f3f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37f3f-113">Un abonnement Direct pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="37f3f-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37f3f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="37f3f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37f3f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="37f3f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37f3f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="37f3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37f3f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37f3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37f3f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="37f3f-118">Scenario description</span></span>
<span data-ttu-id="37f3f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="37f3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37f3f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="37f3f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37f3f-121">Ajout de Direct à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="37f3f-121">Adding Direct from the gallery</span></span>
2. <span data-ttu-id="37f3f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="37f3f-123">Ajout de Direct à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="37f3f-123">Adding Direct from the gallery</span></span>
<span data-ttu-id="37f3f-124">Pour configurer l’intégration de Direct avec Azure AD, vous devez ajouter Direct à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="37f3f-124">To configure the integration of Direct into Azure AD, you need to add Direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37f3f-125">**Pour ajouter Direct à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37f3f-125">**To add Direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37f3f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37f3f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37f3f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="37f3f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="37f3f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="37f3f-133">Dans la zone de recherche, tapez **Direct**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-133">In the search box, type **Direct**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="37f3f-135">Dans le volet de résultats, sélectionnez **Direct**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="37f3f-135">In the results panel, select **Direct**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37f3f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37f3f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Direct, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="37f3f-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37f3f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Direct correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f3f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Direct is to a user in Azure AD.</span></span> <span data-ttu-id="37f3f-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Direct associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="37f3f-140">In other words, a link relationship between an Azure AD user and the related user in Direct needs to be established.</span></span>

<span data-ttu-id="37f3f-141">Dans Direct, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="37f3f-141">In Direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37f3f-142">Pour configurer et tester l’authentification unique Azure AD avec Direct, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="37f3f-142">To configure and test Azure AD single sign-on with Direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37f3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="37f3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37f3f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37f3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37f3f-145">**[Création d’un utilisateur test Direct](#creating-a-direct-test-user)** pour avoir un équivalent de Britta Simon dans Direct lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="37f3f-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in Direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37f3f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f3f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37f3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="37f3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37f3f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37f3f-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Direct.</span><span class="sxs-lookup"><span data-stu-id="37f3f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="37f3f-150">**Pour configurer l’authentification unique Azure AD avec Direct, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37f3f-150">**To configure Azure AD single sign-on with Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="37f3f-151">Dans le portail Azure, sur la page d’intégration de l’application **Direct**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-151">In the Azure portal, on the **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="37f3f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37f3f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="37f3f-155">Dans la section **Domaine et URL Direct**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="37f3f-155">On the **Direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="37f3f-157">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="37f3f-157">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="37f3f-158">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="37f3f-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="37f3f-160">Dans la zone de texte **URL de connexion**, entrez l’URL : `https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="37f3f-160">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="37f3f-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="37f3f-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="37f3f-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="37f3f-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="37f3f-165">Pour configurer l’authentification unique côté **Direct**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique de Direct](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="37f3f-165">To configure single sign-on on **Direct** side, you need to send the downloaded **Metadata XML** to [Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="37f3f-166">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="37f3f-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37f3f-167">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="37f3f-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37f3f-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37f3f-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37f3f-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f3f-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="37f3f-170">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37f3f-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="37f3f-172">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37f3f-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37f3f-173">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37f3f-175">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37f3f-177">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="37f3f-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37f3f-179">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37f3f-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37f3f-181">a.</span><span class="sxs-lookup"><span data-stu-id="37f3f-181">a.</span></span> <span data-ttu-id="37f3f-182">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37f3f-183">b.</span><span class="sxs-lookup"><span data-stu-id="37f3f-183">b.</span></span> <span data-ttu-id="37f3f-184">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37f3f-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37f3f-185">c.</span><span class="sxs-lookup"><span data-stu-id="37f3f-185">c.</span></span> <span data-ttu-id="37f3f-186">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37f3f-187">d.</span><span class="sxs-lookup"><span data-stu-id="37f3f-187">d.</span></span> <span data-ttu-id="37f3f-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="37f3f-189">Création d’un utilisateur de test Direct</span><span class="sxs-lookup"><span data-stu-id="37f3f-189">Creating a Direct test user</span></span>

<span data-ttu-id="37f3f-190">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Direct.</span><span class="sxs-lookup"><span data-stu-id="37f3f-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="37f3f-191">Collaborez avec l’[équipe du support technique de Direct](https://direct4b.com/ja/support.html#inquiry) pour ajouter des utilisateurs dans la plate-forme Direct.</span><span class="sxs-lookup"><span data-stu-id="37f3f-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the Direct platform.</span></span> <span data-ttu-id="37f3f-192">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37f3f-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="37f3f-193">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f3f-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="37f3f-194">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Direct.</span><span class="sxs-lookup"><span data-stu-id="37f3f-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Direct.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="37f3f-196">**Pour affecter Britta Simon à Direct, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37f3f-196">**To assign Britta Simon to Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="37f3f-197">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="37f3f-199">Dans la liste des applications, sélectionnez **Direct**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-199">In the applications list, select **Direct**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="37f3f-201">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="37f3f-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-203">Click **Add** button.</span></span> <span data-ttu-id="37f3f-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="37f3f-206">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="37f3f-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37f3f-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37f3f-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37f3f-209">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="37f3f-209">Testing single sign-on</span></span>

<span data-ttu-id="37f3f-210">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="37f3f-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="37f3f-211">Si vous souhaitez tester en **mode initié par IDP** :</span><span class="sxs-lookup"><span data-stu-id="37f3f-211">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="37f3f-212">Lorsque vous cliquez sur la vignette **Direct** dans le volet d’accès, vous devez être connecté automatiquement à votre application **Direct**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-212">When you click the **Direct** tile in the Access Panel, you should get automatically signed-on to your **Direct** application.</span></span>

2. <span data-ttu-id="37f3f-213">Si vous souhaitez tester en **mode initié par SP** :</span><span class="sxs-lookup"><span data-stu-id="37f3f-213">If you wish to test in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="37f3f-214">a.</span><span class="sxs-lookup"><span data-stu-id="37f3f-214">a.</span></span> <span data-ttu-id="37f3f-215">Cliquez sur la vignette **Direct** dans le volet d’accès, et vous serez redirigé vers la page d’authentification de l’application.</span><span class="sxs-lookup"><span data-stu-id="37f3f-215">Click on the **Direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="37f3f-216">b.</span><span class="sxs-lookup"><span data-stu-id="37f3f-216">b.</span></span> <span data-ttu-id="37f3f-217">Entrez votre `subdomain` dans la zone de texte affichée et appuyez sur « 次へ (Suivant) ». Vous serez alors automatiquement authentifié sur votre application **Direct**.</span><span class="sxs-lookup"><span data-stu-id="37f3f-217">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **Direct** application .</span></span>
    
<span data-ttu-id="37f3f-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37f3f-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37f3f-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="37f3f-219">Additional resources</span></span>

* [<span data-ttu-id="37f3f-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37f3f-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37f3f-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="37f3f-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

