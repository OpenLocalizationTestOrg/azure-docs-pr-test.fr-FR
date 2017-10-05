---
title: "Didacticiel : Intégration d’Azure Active Directory à Yardi eLearning | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Yardi eLearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: e7b36b692ad2a8bc3a3f5203d93882af96fd2109
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="5cdc6-103">Didacticiel : Intégration d’Azure Active Directory à Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5cdc6-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="5cdc6-104">Dans ce didacticiel, vous allez apprendre à intégrer Yardi eLearning à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5cdc6-104">In this tutorial, you learn how to integrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5cdc6-105">L’intégration de Yardi eLearning dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-105">Integrating Yardi eLearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5cdc6-106">Dans Azure AD, vous pouvez contrôler qui a accès à Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5cdc6-106">You can control in Azure AD who has access to Yardi eLearning</span></span>
- <span data-ttu-id="5cdc6-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Yardi eLearning (via l'authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-107">You can enable your users to automatically get signed-on to Yardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5cdc6-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5cdc6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5cdc6-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5cdc6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cdc6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5cdc6-110">Prerequisites</span></span>

<span data-ttu-id="5cdc6-111">Pour configurer l’intégration d’Azure AD à Yardi eLearning, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-111">To configure Azure AD integration with Yardi eLearning, you need the following items:</span></span>

- <span data-ttu-id="5cdc6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5cdc6-113">Un abonnement Yardi eLearning pour lequel l'authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5cdc6-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5cdc6-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5cdc6-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5cdc6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5cdc6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5cdc6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5cdc6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5cdc6-118">Scenario description</span></span>
<span data-ttu-id="5cdc6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5cdc6-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5cdc6-121">Ajout de Yardi eLearning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5cdc6-121">Adding Yardi eLearning from the gallery</span></span>
2. <span data-ttu-id="5cdc6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-the-gallery"></a><span data-ttu-id="5cdc6-123">Ajout de Yardi eLearning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5cdc6-123">Adding Yardi eLearning from the gallery</span></span>
<span data-ttu-id="5cdc6-124">Pour configurer l'intégration de Yardi eLearning à Azure AD, vous devez ajouter Yardi eLearning à votre liste d'applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-124">To configure the integration of Yardi eLearning into Azure AD, you need to add Yardi eLearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5cdc6-125">**Pour ajouter Yardi eLearning à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5cdc6-125">**To add Yardi eLearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5cdc6-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5cdc6-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5cdc6-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5cdc6-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5cdc6-133">Dans la zone de recherche, tapez **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-133">In the search box, type **Yardi eLearning**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_search.png)

5. <span data-ttu-id="5cdc6-135">Dans le volet de résultats, sélectionnez **Yardi eLearning**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-135">In the results panel, select **Yardi eLearning**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5cdc6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5cdc6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Yardi eLearning avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5cdc6-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5cdc6-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Yardi eLearning équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Yardi eLearning is to a user in Azure AD.</span></span> <span data-ttu-id="5cdc6-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Yardi eLearning associé.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-140">In other words, a link relationship between an Azure AD user and the related user in Yardi eLearning needs to be established.</span></span>

<span data-ttu-id="5cdc6-141">Dans Yardi eLearning, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-141">In Yardi eLearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5cdc6-142">Pour configurer et tester l'authentification unique Azure AD avec Yardi eLearning, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-142">To configure and test Azure AD single sign-on with Yardi eLearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5cdc6-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5cdc6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5cdc6-145">**[Création d’un utilisateur de test Yardi eLearning](#creating-a-yardi-elearning-test-user)** pour avoir un équivalent de Britta Simon dans Yardi eLearning lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - to have a counterpart of Britta Simon in Yardi eLearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5cdc6-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5cdc6-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5cdc6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5cdc6-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="5cdc6-150">**Pour configurer l'authentification unique Azure AD avec Yardi eLearning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5cdc6-150">**To configure Azure AD single sign-on with Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="5cdc6-151">Dans le portail Azure, dans la page d’intégration de l’application **Yardi eLearning**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-151">In the Azure portal, on the **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5cdc6-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

3. <span data-ttu-id="5cdc6-155">Dans la section **Domaine et URL Yardi eLearning**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-155">On the **Yardi eLearning Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="5cdc6-157">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-157">a.</span></span> <span data-ttu-id="5cdc6-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="5cdc6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="5cdc6-159">b.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-159">b.</span></span> <span data-ttu-id="5cdc6-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="5cdc6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5cdc6-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-161">These values are not real.</span></span> <span data-ttu-id="5cdc6-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5cdc6-163">Pour obtenir ces valeurs, contactez [l’équipe du support client Yardi eLearning](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="5cdc6-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) to get these values.</span></span> 
 
4. <span data-ttu-id="5cdc6-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

5. <span data-ttu-id="5cdc6-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5cdc6-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-yardielearning-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5cdc6-168">Pour configurer l’authentification unique côté **Yardi eLearning**, vous devez envoyer les **métadonnées XML** téléchargées à [l’équipe du support technique Yardi eLearning](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="5cdc6-168">To configure single sign-on on **Yardi eLearning** side, you need to send the downloaded **Metadata XML** to [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="5cdc6-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5cdc6-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5cdc6-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5cdc6-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5cdc6-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5cdc6-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5cdc6-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5cdc6-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5cdc6-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5cdc6-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5cdc6-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5cdc6-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5cdc6-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5cdc6-184">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-184">a.</span></span> <span data-ttu-id="5cdc6-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5cdc6-186">b.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-186">b.</span></span> <span data-ttu-id="5cdc6-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5cdc6-188">c.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-188">c.</span></span> <span data-ttu-id="5cdc6-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5cdc6-190">d.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-190">d.</span></span> <span data-ttu-id="5cdc6-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="5cdc6-192">Création d'un utilisateur de test Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5cdc6-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="5cdc6-193">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-193">The objective of this section is to create a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="5cdc6-194">Yardi eLearning prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5cdc6-195">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-195">There is no action item for you in this section.</span></span> <span data-ttu-id="5cdc6-196">Un utilisateur est créé lors d’une tentative d’accès à Yardi eLearning s’il n’en existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-196">A new user is created during an attempt to access Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="5cdc6-197">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique Yardi eLearning](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="5cdc6-197">If you need to create a user manually, you need to contact the [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5cdc6-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cdc6-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5cdc6-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yardi eLearning.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5cdc6-201">**Pour affecter Britta Simon à Yardi eLearning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5cdc6-201">**To assign Britta Simon to Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="5cdc6-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5cdc6-204">Dans la liste des applications, sélectionnez **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-204">In the applications list, select **Yardi eLearning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_app.png) 

3. <span data-ttu-id="5cdc6-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5cdc6-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-208">Click **Add** button.</span></span> <span data-ttu-id="5cdc6-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5cdc6-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5cdc6-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5cdc6-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5cdc6-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5cdc6-214">Testing single sign-on</span></span>

<span data-ttu-id="5cdc6-215">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5cdc6-216">Lorsque vous cliquez sur la mosaïque Yardi eLearning dans le volet d'accès, vous êtes connecté automatiquement à votre application Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="5cdc6-216">When you click the Yardi eLearning tile in the Access Panel, you should get automatically signed-on to your Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5cdc6-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5cdc6-217">Additional resources</span></span>

* [<span data-ttu-id="5cdc6-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cdc6-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5cdc6-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5cdc6-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_203.png

