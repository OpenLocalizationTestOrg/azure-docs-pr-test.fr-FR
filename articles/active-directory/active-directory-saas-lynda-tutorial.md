---
title: "Didacticiel : Intégration d’Azure Active Directory avec Lynda.com | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="b3ed9-103">Didacticiel : Intégration d’Azure Active Directory à Lynda.com</span><span class="sxs-lookup"><span data-stu-id="b3ed9-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="b3ed9-104">Dans ce didacticiel, vous allez apprendre à intégrer Lynda.com à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3ed9-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3ed9-105">Intégrer Lynda.com à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b3ed9-106">Dans Azure AD, vous pouvez contrôler l’accès à Lynda.com</span><span class="sxs-lookup"><span data-stu-id="b3ed9-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="b3ed9-107">Vous pouvez autoriser les utilisateurs à être automatiquement connectés à Lynda.com (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3ed9-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b3ed9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b3ed9-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3ed9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3ed9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b3ed9-110">Prerequisites</span></span>

<span data-ttu-id="b3ed9-111">Pour configurer l’intégration d’Azure AD avec Lynda.com, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="b3ed9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3ed9-113">Un abonnement Lynda.com pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b3ed9-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3ed9-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3ed9-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3ed9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3ed9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3ed9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3ed9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b3ed9-118">Scenario description</span></span>
<span data-ttu-id="b3ed9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3ed9-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3ed9-121">Ajouter Lynda.com à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b3ed9-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="b3ed9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="b3ed9-123">Ajouter Lynda.com à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b3ed9-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="b3ed9-124">Pour configurer l’intégration de Lynda.com à Azure AD, vous devez ajouter Lynda.com à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b3ed9-125">**Pour ajouter Lynda.com à partir de la galerie, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="b3ed9-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b3ed9-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3ed9-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b3ed9-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b3ed9-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b3ed9-133">Dans la zone de recherche, entrez **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-133">In the search box, type **Lynda.com**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="b3ed9-135">Dans le panneau de résultats, sélectionnez **Lynda.com**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3ed9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3ed9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lynda.com grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b3ed9-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3ed9-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Lynda.com équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="b3ed9-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Lynda.com associé.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="b3ed9-141">Pour cela, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** dans Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="b3ed9-142">Pour configurer et tester l’authentification unique Azure AD avec Lynda.com, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b3ed9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b3ed9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3ed9-145">**[Création d’un utilisateur de test Lynda.com](#creating-a-lyndacom-test-user)** pour avoir un équivalent de Britta Simon dans Lynda.com qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3ed9-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3ed9-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3ed9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3ed9-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="b3ed9-150">**Pour configurer l’authentification unique Azure AD avec Lynda.com, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="b3ed9-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="b3ed9-151">Dans le portail Azure, sur la page d’intégration de l’application **Lynda.com**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b3ed9-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="b3ed9-155">Dans la section **Domaine et URL Lynda.com**, réalisez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="b3ed9-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="b3ed9-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3ed9-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-158">This value is not real.</span></span> <span data-ttu-id="b3ed9-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b3ed9-160">Pour obtenir ces valeurs, contactez l’[équipe de support technique Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="b3ed9-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="b3ed9-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="b3ed9-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b3ed9-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3ed9-165">Pour configurer l’authentification unique du côté **Lynda.com**, vous devez envoyer le **XML des métadonnées** téléchargé à l’[équipe de support Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="b3ed9-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3ed9-166">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3ed9-167">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b3ed9-169">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b3ed9-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b3ed9-170">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3ed9-172">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3ed9-174">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3ed9-176">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b3ed9-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3ed9-178">a.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-178">a.</span></span> <span data-ttu-id="b3ed9-179">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3ed9-180">b.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-180">b.</span></span> <span data-ttu-id="b3ed9-181">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3ed9-182">c.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-182">c.</span></span> <span data-ttu-id="b3ed9-183">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b3ed9-184">d.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-184">d.</span></span> <span data-ttu-id="b3ed9-185">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="b3ed9-186">Créer un utilisateur de test Lynda.com</span><span class="sxs-lookup"><span data-stu-id="b3ed9-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="b3ed9-187">Aucun élément d'action ne vous permet de configurer l’approvisionnement des utilisateurs dans Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="b3ed9-188">Lorsqu'un utilisateur assigné tente de se connecter à Lynda.com à l'aide du panneau d'accès, Lynda.com vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="b3ed9-189">Si aucun compte d'utilisateur n’est disponible, Lynda.com le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="b3ed9-190">Vous pouvez utiliser n'importe quel outil ou API de création de compte utilisateur, fourni par Lynda.com, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b3ed9-191">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3ed9-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b3ed9-192">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b3ed9-194">**Pour assigner Britta Simon à Lynda.com, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b3ed9-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="b3ed9-195">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b3ed9-197">Dans la liste des applications, sélectionnez **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-197">In the applications list, select **Lynda.com**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="b3ed9-199">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b3ed9-201">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-201">Click **Add** button.</span></span> <span data-ttu-id="b3ed9-202">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b3ed9-204">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b3ed9-205">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3ed9-206">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3ed9-207">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b3ed9-207">Testing single sign-on</span></span>

<span data-ttu-id="b3ed9-208">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b3ed9-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b3ed9-209">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b3ed9-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b3ed9-210">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b3ed9-210">Additional resources</span></span>

* [<span data-ttu-id="b3ed9-211">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3ed9-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3ed9-212">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b3ed9-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

