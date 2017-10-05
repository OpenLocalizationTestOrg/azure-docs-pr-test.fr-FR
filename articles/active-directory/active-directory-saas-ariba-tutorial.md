---
title: "Didacticiel : Intégration d’Azure Active Directory à Ariba | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="1713c-103">Didacticiel : Intégration d’Azure Active Directory à Ariba</span><span class="sxs-lookup"><span data-stu-id="1713c-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="1713c-104">Dans ce didacticiel, vous allez apprendre à intégrer Ariba à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1713c-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1713c-105">L’intégration d’Ariba dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1713c-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1713c-106">Dans Azure AD, vous pouvez contrôler qui a accès à Ariba.</span><span class="sxs-lookup"><span data-stu-id="1713c-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="1713c-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Ariba (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1713c-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1713c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1713c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1713c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1713c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1713c-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="1713c-110">Prerequisites</span></span>

<span data-ttu-id="1713c-111">Pour configurer l’intégration d’Azure AD à Ariba, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1713c-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="1713c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1713c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1713c-113">Un abonnement Ariba pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1713c-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1713c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1713c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1713c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1713c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1713c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1713c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1713c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1713c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1713c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1713c-118">Scenario description</span></span>
<span data-ttu-id="1713c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1713c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1713c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1713c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1713c-121">Ajout d’Ariba à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1713c-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="1713c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1713c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="1713c-123">Ajout d’Ariba à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1713c-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="1713c-124">Pour configurer l’intégration d’Ariba à Azure AD, vous devez ajouter Ariba à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1713c-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1713c-125">**Pour ajouter Ariba à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1713c-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1713c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1713c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1713c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1713c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1713c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1713c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1713c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1713c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1713c-133">Dans la zone de recherche, tapez **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="1713c-133">In the search box, type **Ariba**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="1713c-135">Dans le volet de résultats, sélectionnez **Ariba**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1713c-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1713c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1713c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1713c-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Ariba au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1713c-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1713c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Ariba correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1713c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="1713c-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Ariba associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1713c-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="1713c-141">Dans Ariba, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1713c-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1713c-142">Pour configurer et tester l’authentification unique Azure AD avec Ariba, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1713c-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1713c-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1713c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1713c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1713c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1713c-145">**[Création d’un utilisateur de test Ariba](#creating-an-ariba-test-user)** pour avoir dans Ariba un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1713c-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1713c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1713c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1713c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1713c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1713c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1713c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1713c-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Ariba.</span><span class="sxs-lookup"><span data-stu-id="1713c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="1713c-150">**Pour configurer l’authentification unique Azure AD avec Ariba, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1713c-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="1713c-151">Dans le portail Azure, sur la page d’intégration de l’application **Ariba**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1713c-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1713c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1713c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="1713c-155">Dans la section **Domaine et URL Ariba**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1713c-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="1713c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1713c-157">a.</span></span> <span data-ttu-id="1713c-158">Dans la zone de texte **URL de connexion**, entrez une URL au format suivant : `https://<subdomain>.sourcing.ariba.com` ou `https://<subdomain>.supplier.ariba.com`.</span><span class="sxs-lookup"><span data-stu-id="1713c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="1713c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1713c-159">b.</span></span> <span data-ttu-id="1713c-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="1713c-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1713c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1713c-161">These values are not real.</span></span> <span data-ttu-id="1713c-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="1713c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1713c-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="1713c-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="1713c-164">Pour obtenir ces valeurs, contactez l’équipe du support technique d’Ariba au **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="1713c-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="1713c-165">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (Base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1713c-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="1713c-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1713c-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1713c-169">Pour configurer SSO en fonction de votre application, appelez l’équipe du support technique d’Ariba au **1-866-218-2155**. Elle vous expliquera comment procéder pour lui envoyer le fichier **Certificat (Base64)** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="1713c-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="1713c-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1713c-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1713c-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1713c-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1713c-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1713c-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1713c-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1713c-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1713c-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1713c-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1713c-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1713c-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1713c-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1713c-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1713c-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1713c-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1713c-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1713c-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1713c-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1713c-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1713c-185">a.</span><span class="sxs-lookup"><span data-stu-id="1713c-185">a.</span></span> <span data-ttu-id="1713c-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1713c-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1713c-187">b.</span><span class="sxs-lookup"><span data-stu-id="1713c-187">b.</span></span> <span data-ttu-id="1713c-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1713c-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1713c-189">c.</span><span class="sxs-lookup"><span data-stu-id="1713c-189">c.</span></span> <span data-ttu-id="1713c-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1713c-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1713c-191">d.</span><span class="sxs-lookup"><span data-stu-id="1713c-191">d.</span></span> <span data-ttu-id="1713c-192">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1713c-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="1713c-193">Création d’un utilisateur de test Ariba</span><span class="sxs-lookup"><span data-stu-id="1713c-193">Creating an Ariba test user</span></span>

<span data-ttu-id="1713c-194">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Ariba.</span><span class="sxs-lookup"><span data-stu-id="1713c-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="1713c-195">Contactez l’équipe du support technique d’Ariba en appelant le **1-866-218-2155** pour ajouter les utilisateurs au système Ariba.</span><span class="sxs-lookup"><span data-stu-id="1713c-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="1713c-196">Si vous devez créer un utilisateur manuellement, contactez l’équipe du support technique d’Ariba au **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="1713c-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1713c-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1713c-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1713c-198">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Ariba.</span><span class="sxs-lookup"><span data-stu-id="1713c-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1713c-200">**Pour affecter Britta Simon à Ariba, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1713c-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="1713c-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1713c-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1713c-203">Dans la liste des applications, sélectionnez **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="1713c-203">In the applications list, select **Ariba**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="1713c-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1713c-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1713c-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1713c-207">Click **Add** button.</span></span> <span data-ttu-id="1713c-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1713c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1713c-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1713c-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1713c-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1713c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1713c-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1713c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1713c-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1713c-213">Testing single sign-on</span></span>
<span data-ttu-id="1713c-214">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1713c-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1713c-215">Lorsque vous cliquez sur la vignette Ariba dans le volet d’accès, vous devez être connecté automatiquement à votre application Ariba.</span><span class="sxs-lookup"><span data-stu-id="1713c-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1713c-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1713c-216">Additional resources</span></span>

* [<span data-ttu-id="1713c-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1713c-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1713c-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1713c-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

