---
title: "Didacticiel : Intégration d’Azure Active Directory avec JobScore | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et JobScore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed2d362f7b027bfdc38ba2fdaa03948ff5632c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="a060c-103">Didacticiel : Intégration d’Azure Active Directory à JobScore</span><span class="sxs-lookup"><span data-stu-id="a060c-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="a060c-104">Dans ce didacticiel, vous allez apprendre à intégrer JobScore à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a060c-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a060c-105">L’intégration de JobScore avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a060c-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a060c-106">Dans Azure AD, vous pouvez contrôler qui a accès à JobScore</span><span class="sxs-lookup"><span data-stu-id="a060c-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="a060c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à JobScore (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a060c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a060c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a060c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a060c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a060c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a060c-110">Prerequisites</span></span>

<span data-ttu-id="a060c-111">Pour configurer l’intégration d’Azure AD à JobScore, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a060c-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="a060c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a060c-113">Un abonnement JobScore pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a060c-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a060c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a060c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a060c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a060c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a060c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a060c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a060c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a060c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a060c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a060c-118">Scenario description</span></span>
<span data-ttu-id="a060c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a060c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a060c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a060c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a060c-121">Ajout de JobScore à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a060c-121">Adding JobScore from the gallery</span></span>
2. <span data-ttu-id="a060c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="a060c-123">Ajout de JobScore à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a060c-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="a060c-124">Pour configurer l’intégration de JobScore à Azure AD, vous devez ajouter JobScore à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a060c-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a060c-125">**Pour ajouter JobScore à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a060c-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a060c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a060c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a060c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a060c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a060c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a060c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a060c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a060c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a060c-133">Dans la zone de recherche, entrez **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="a060c-133">In the search box, type **JobScore**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="a060c-135">Dans le volet de résultats, sélectionnez **JobScore**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a060c-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a060c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a060c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec JobScore avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a060c-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a060c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur JobScore équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a060c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="a060c-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur JobScore associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a060c-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="a060c-141">Dans JobScore, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a060c-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a060c-142">Pour configurer et tester l’authentification unique Azure AD avec JobScore, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a060c-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a060c-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a060c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a060c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a060c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a060c-145">**[Création d’un utilisateur de test JobScore](#creating-a-jobscore-test-user)** pour avoir un équivalent de Britta Simon dans JobScore lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a060c-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a060c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a060c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a060c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a060c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a060c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a060c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application JobScore.</span><span class="sxs-lookup"><span data-stu-id="a060c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="a060c-150">**Pour configurer l’authentification unique Azure AD avec JobScore, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a060c-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="a060c-151">Dans le portail Azure, sur la page d’intégration de l’application **JobScore**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a060c-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a060c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a060c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="a060c-155">Dans la section **Domaine et URL JobScore**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a060c-155">On the **JobScore Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="a060c-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="a060c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a060c-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="a060c-158">This value is not real.</span></span> <span data-ttu-id="a060c-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="a060c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a060c-160">Contactez [l’équipe de support client de JobScore](mailto:support@jobscore.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="a060c-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span></span> 
 
4. <span data-ttu-id="a060c-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a060c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="a060c-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a060c-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a060c-165">Pour configurer l’authentification unique côté **JobScore**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique de JobScore](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="a060c-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="a060c-166">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a060c-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a060c-167">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a060c-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a060c-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a060c-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a060c-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="a060c-170">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a060c-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a060c-172">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a060c-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a060c-173">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a060c-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a060c-175">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a060c-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a060c-177">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a060c-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a060c-179">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a060c-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a060c-181">a.</span><span class="sxs-lookup"><span data-stu-id="a060c-181">a.</span></span> <span data-ttu-id="a060c-182">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a060c-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a060c-183">b.</span><span class="sxs-lookup"><span data-stu-id="a060c-183">b.</span></span> <span data-ttu-id="a060c-184">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a060c-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a060c-185">c.</span><span class="sxs-lookup"><span data-stu-id="a060c-185">c.</span></span> <span data-ttu-id="a060c-186">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a060c-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a060c-187">d.</span><span class="sxs-lookup"><span data-stu-id="a060c-187">d.</span></span> <span data-ttu-id="a060c-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a060c-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="a060c-189">Création d’un utilisateur de test JobScore</span><span class="sxs-lookup"><span data-stu-id="a060c-189">Creating a JobScore test user</span></span>

<span data-ttu-id="a060c-190">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans JobScore.</span><span class="sxs-lookup"><span data-stu-id="a060c-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="a060c-191">Collaborez avec [l’équipe du support technique de JobScore](mailto:support@jobscore.com) pour ajouter des utilisateurs dans la plateforme JobScore.</span><span class="sxs-lookup"><span data-stu-id="a060c-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a060c-192">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a060c-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a060c-193">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à JobScore.</span><span class="sxs-lookup"><span data-stu-id="a060c-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a060c-195">**Pour affecter Britta Simon à JobScore, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a060c-195">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="a060c-196">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a060c-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a060c-198">Dans la liste des applications, sélectionnez **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="a060c-198">In the applications list, select **JobScore**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="a060c-200">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a060c-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a060c-202">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a060c-202">Click **Add** button.</span></span> <span data-ttu-id="a060c-203">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a060c-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a060c-205">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a060c-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a060c-206">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a060c-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a060c-207">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a060c-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a060c-208">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a060c-208">Testing single sign-on</span></span>

<span data-ttu-id="a060c-209">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a060c-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a060c-210">Si vous cliquez sur la mosaïque JobScore dans le volet d’accès, vous devez vous connecter automatiquement à votre application JobScore.</span><span class="sxs-lookup"><span data-stu-id="a060c-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a060c-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a060c-211">Additional resources</span></span>

* [<span data-ttu-id="a060c-212">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a060c-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a060c-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a060c-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

