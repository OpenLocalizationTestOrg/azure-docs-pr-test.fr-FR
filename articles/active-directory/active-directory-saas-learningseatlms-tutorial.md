---
title: "Didacticiel : intégration d’Azure Active Directory avec Learning Seat LMS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Learning Seat LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 877e0288fdd1f590acf064c204aff0741539b112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="9fbda-103">Didacticiel : intégration d’Azure Active Directory à Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="9fbda-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="9fbda-104">Dans ce didacticiel, vous allez apprendre à intégrer Learning Seat LMS à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fbda-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fbda-105">L’intégration de Learning Seat LMS dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9fbda-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9fbda-106">Dans Azure AD, vous pouvez contrôler qui a accès à Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="9fbda-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="9fbda-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Learning Seat LMS (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fbda-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9fbda-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9fbda-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="9fbda-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9fbda-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9fbda-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fbda-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9fbda-111">Prerequisites</span></span>

<span data-ttu-id="9fbda-112">Pour configurer l’intégration d’Azure AD à Learning Seat LMS, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9fbda-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="9fbda-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9fbda-114">Un abonnement à Learning Seat LMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9fbda-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fbda-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9fbda-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fbda-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9fbda-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fbda-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9fbda-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fbda-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9fbda-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fbda-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9fbda-119">Scenario description</span></span>
<span data-ttu-id="9fbda-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9fbda-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fbda-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9fbda-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fbda-122">Ajout de Learning Seat LMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9fbda-122">Adding Learning Seat LMS from the gallery</span></span>
2. <span data-ttu-id="9fbda-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="9fbda-124">Ajout de Learning Seat LMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9fbda-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="9fbda-125">Pour configurer l’intégration de Learning Seat LMS à Azure AD, vous devez ajouter Learning Seat LMS à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9fbda-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9fbda-126">**Pour ajouter Learning Seat LMS à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9fbda-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9fbda-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9fbda-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9fbda-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9fbda-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9fbda-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9fbda-134">Dans la zone de recherche, entrez **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="9fbda-136">Dans le volet de résultats, sélectionnez **Learning Seat LMS**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9fbda-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fbda-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fbda-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Learning Seat LMS avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9fbda-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9fbda-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Learning Seat LMS équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fbda-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="9fbda-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Learning Seat LMS associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9fbda-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="9fbda-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** dans Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="9fbda-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="9fbda-142">Pour configurer et tester l'authentification unique Azure AD avec Learning Seat LMS, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="9fbda-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9fbda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9fbda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9fbda-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9fbda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fbda-145">**[Création d’un utilisateur de test Learning Seat LMS](#creating-a-learnconnect-test-user)** : pour avoir un équivalent de Britta Simon dans Learning Seat LMS lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fbda-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fbda-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fbda-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fbda-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9fbda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fbda-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fbda-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le nouveau portail Azure et configurer l’authentification unique dans votre application Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="9fbda-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="9fbda-150">**Pour configurer l’authentification unique Azure AD avec Learning Seat LMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9fbda-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="9fbda-151">Dans le portail Azure, sur la page d’intégration de l’application **Learning Seat LMS**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9fbda-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9fbda-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="9fbda-155">Dans la section **Domaines et URL Learning Seat LMS**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP** :</span><span class="sxs-lookup"><span data-stu-id="9fbda-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="9fbda-157">a.</span><span class="sxs-lookup"><span data-stu-id="9fbda-157">a.</span></span> <span data-ttu-id="9fbda-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="9fbda-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="9fbda-159">b.</span><span class="sxs-lookup"><span data-stu-id="9fbda-159">b.</span></span> <span data-ttu-id="9fbda-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="9fbda-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="9fbda-161">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="9fbda-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="9fbda-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="9fbda-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9fbda-164">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9fbda-164">These values are not the real values.</span></span> <span data-ttu-id="9fbda-165">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="9fbda-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="9fbda-166">Pour obtenir ces valeurs, contactez [l’équipe de support technique Learning Seat](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="9fbda-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

5. <span data-ttu-id="9fbda-167">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9fbda-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="9fbda-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9fbda-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9fbda-171">Pour configurer l’authentification unique du côté de **Learning Seat LMS**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique de Learning Seat](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="9fbda-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="9fbda-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9fbda-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9fbda-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9fbda-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9fbda-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9fbda-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fbda-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="9fbda-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9fbda-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9fbda-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9fbda-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9fbda-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fbda-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fbda-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9fbda-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fbda-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fbda-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fbda-187">a.</span><span class="sxs-lookup"><span data-stu-id="9fbda-187">a.</span></span> <span data-ttu-id="9fbda-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fbda-189">b.</span><span class="sxs-lookup"><span data-stu-id="9fbda-189">b.</span></span> <span data-ttu-id="9fbda-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9fbda-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fbda-191">c.</span><span class="sxs-lookup"><span data-stu-id="9fbda-191">c.</span></span> <span data-ttu-id="9fbda-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9fbda-193">d.</span><span class="sxs-lookup"><span data-stu-id="9fbda-193">d.</span></span> <span data-ttu-id="9fbda-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="9fbda-195">Création d’un utilisateur de test Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="9fbda-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="9fbda-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="9fbda-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="9fbda-197">Contactez [l’équipe de support technique Learning Seat LMS](http://help.learningseatlms.com/help) avec toutes les informations utilisateur pour ajouter des utilisateurs dans l’application Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="9fbda-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9fbda-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fbda-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9fbda-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="9fbda-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9fbda-201">**Pour affecter Britta Simon à Learning Seat LMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9fbda-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="9fbda-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9fbda-204">Dans la liste des applications, sélectionnez **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="9fbda-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9fbda-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-208">Click **Add** button.</span></span> <span data-ttu-id="9fbda-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9fbda-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9fbda-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9fbda-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fbda-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9fbda-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fbda-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9fbda-214">Testing single sign-on</span></span>

<span data-ttu-id="9fbda-215">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9fbda-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="9fbda-216">Lorsque vous cliquez sur la vignette Learning Seat LMS dans le volet d’accès, vous êtes automatiquement connecté à votre application Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="9fbda-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="9fbda-217">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9fbda-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fbda-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9fbda-218">Additional resources</span></span>

* [<span data-ttu-id="9fbda-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fbda-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fbda-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9fbda-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

