---
title: "Didacticiel : Intégration d’Azure Active Directory avec Atomic Learning | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Atomic Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 6cce8fc839e60eb6498ab48bf68e9906c98889a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="3b6c4-103">Didacticiel : Intégration d’Azure Active Directory à Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="3b6c4-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="3b6c4-104">Dans ce didacticiel, vous allez apprendre à intégrer Atomic Learning à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b6c4-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b6c4-105">L’intégration de Atomic Learning dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3b6c4-106">Dans Azure AD, vous pouvez contrôler qui a accès à Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-106">You can control in Azure AD who has access to Atomic Learning</span></span>
- <span data-ttu-id="3b6c4-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Atomic Learning (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b6c4-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3b6c4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3b6c4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b6c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b6c4-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3b6c4-110">Prerequisites</span></span>

<span data-ttu-id="3b6c4-111">Pour configurer l’intégration d’Azure AD à Atomic Learning, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span></span>

- <span data-ttu-id="3b6c4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b6c4-113">Un abonnement Atomic Learning pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3b6c4-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b6c4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b6c4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b6c4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b6c4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b6c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b6c4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3b6c4-118">Scenario description</span></span>
<span data-ttu-id="3b6c4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b6c4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b6c4-121">Ajout d’Atomic Learning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3b6c4-121">Adding Atomic Learning from the gallery</span></span>
2. <span data-ttu-id="3b6c4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-the-gallery"></a><span data-ttu-id="3b6c4-123">Ajout d’Atomic Learning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3b6c4-123">Adding Atomic Learning from the gallery</span></span>
<span data-ttu-id="3b6c4-124">Pour configurer l’intégration de Atomic Learning à Azure AD, vous devez ajouter Atomic Learning à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3b6c4-125">**Pour ajouter Atomic Learning à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3b6c4-125">**To add Atomic Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6c4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b6c4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3b6c4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3b6c4-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3b6c4-133">Dans la zone de recherche, entrez **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-133">In the search box, type **Atomic Learning**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="3b6c4-135">Dans le volet de résultats, sélectionnez **Atomic Learning**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-135">In the results panel, select **Atomic Learning**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b6c4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b6c4-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Atomic Learning au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3b6c4-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3b6c4-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Atomic Learning équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span></span> <span data-ttu-id="3b6c4-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Atomic Learning associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-140">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span></span>

<span data-ttu-id="3b6c4-141">Dans Atomic Learning, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-141">In Atomic Learning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3b6c4-142">Pour configurer et tester l’authentification unique Azure AD avec Atomic Learning, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-142">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3b6c4-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3b6c4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b6c4-145">**[Création d’un utilisateur de test Atomic Learning](#creating-an-atomic-learning-test-user)** pour avoir dans Atomic Learning un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b6c4-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b6c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b6c4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b6c4-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="3b6c4-150">**Pour configurer l’authentification unique Azure AD avec Atomic Learning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3b6c4-150">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6c4-151">Dans le portail Azure, sur la page d’intégration de l’application **Atomic Learning**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-151">In the Azure portal, on the **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3b6c4-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="3b6c4-155">Dans la section **Domaine et URL Atomic Learning**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-155">On the **Atomic Learning Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="3b6c4-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3b6c4-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3b6c4-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-158">This value is not real.</span></span> <span data-ttu-id="3b6c4-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3b6c4-160">Contactez l’[équipe du support technique d’Atomic Learning](mailto:cs@atomiclearning.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) to get this value.</span></span> 
 
4. <span data-ttu-id="3b6c4-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="3b6c4-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3b6c4-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3b6c4-165">Pour configurer l’authentification unique du côté d’**Atomic Learning**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe du support technique d’Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="3b6c4-165">To configure single sign-on on **Atomic Learning** side, you need to send the downloaded **Metadata XML** to [Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="3b6c4-166">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3b6c4-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3b6c4-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3b6c4-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b6c4-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b6c4-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c4-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="3b6c4-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3b6c4-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3b6c4-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6c4-174">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b6c4-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b6c4-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b6c4-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3b6c4-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b6c4-182">a.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-182">a.</span></span> <span data-ttu-id="3b6c4-183">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b6c4-184">b.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-184">b.</span></span> <span data-ttu-id="3b6c4-185">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b6c4-186">c.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-186">c.</span></span> <span data-ttu-id="3b6c4-187">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3b6c4-188">d.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-188">d.</span></span> <span data-ttu-id="3b6c4-189">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="3b6c4-190">Création d’un utilisateur de test Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="3b6c4-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="3b6c4-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="3b6c4-192">Atomic Learning prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="3b6c4-193">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-193">There is no action item for you in this section.</span></span> <span data-ttu-id="3b6c4-194">S’il n’existe pas déjà, un utilisateur est créé au moment d’une tentative d’accès à Atomic Learning à l’aide de l’adresse e-mail de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-194">A new user is created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3b6c4-195">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c4-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3b6c4-196">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atomic Learning.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3b6c4-198">**Pour affecter Britta Simon à Atomic Learning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3b6c4-198">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6c4-199">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3b6c4-201">Dans la liste des applications, sélectionnez **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-201">In the applications list, select **Atomic Learning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="3b6c4-203">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3b6c4-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-205">Click **Add** button.</span></span> <span data-ttu-id="3b6c4-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3b6c4-208">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3b6c4-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b6c4-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b6c4-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3b6c4-211">Testing single sign-on</span></span>

<span data-ttu-id="3b6c4-212">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3b6c4-213">Quand vous cliquez sur la vignette Atomic Learning dans le volet d’accès, vous devez être connecté automatiquement à votre application Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="3b6c4-213">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span></span>
<span data-ttu-id="3b6c4-214">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3b6c4-214">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3b6c4-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3b6c4-215">Additional resources</span></span>

* [<span data-ttu-id="3b6c4-216">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b6c4-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b6c4-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3b6c4-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

