---
title: "Didacticiel : Intégration d’Azure Active Directory à NetDocuments | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="1e154-103">Didacticiel : Intégration d’Azure Active Directory à NetDocuments</span><span class="sxs-lookup"><span data-stu-id="1e154-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="1e154-104">Dans ce didacticiel, vous allez apprendre à intégrer NetDocuments à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e154-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e154-105">L’intégration de NetDocuments dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1e154-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e154-106">Dans Azure AD, vous pouvez contrôler qui a accès à NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="1e154-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="1e154-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à NetDocuments (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e154-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e154-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1e154-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e154-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e154-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e154-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1e154-110">Prerequisites</span></span>

<span data-ttu-id="1e154-111">Pour configurer l’intégration d’Azure AD avec NetDocuments, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1e154-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="1e154-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e154-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e154-113">Un abonnement NetDocuments pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1e154-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e154-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1e154-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e154-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1e154-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e154-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1e154-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e154-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e154-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e154-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1e154-118">Scenario description</span></span>
<span data-ttu-id="1e154-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1e154-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e154-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e154-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e154-121">Ajout de NetDocuments à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1e154-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="1e154-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e154-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="1e154-123">Ajout de NetDocuments à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1e154-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="1e154-124">Pour configurer l’intégration de NetDocuments à Azure AD, vous devez ajouter NetDocuments à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="1e154-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e154-125">**Pour ajouter NetDocuments à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e154-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e154-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e154-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e154-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1e154-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e154-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1e154-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1e154-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1e154-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1e154-133">Dans la zone de recherche, entrez **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="1e154-133">In the search box, type **NetDocuments**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="1e154-135">Dans le panneau des résultats, sélectionnez **NetDocuments**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1e154-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e154-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e154-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e154-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec NetDocuments avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1e154-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e154-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur NetDocuments équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e154-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="1e154-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur NetDocuments associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1e154-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="1e154-141">Dans NetDocuments, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1e154-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e154-142">Pour configurer et tester l’authentification unique Azure AD avec NetDocuments, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e154-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e154-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1e154-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e154-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e154-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e154-145">**[Création d’un utilisateur de test NetDocuments](#creating-a-netdocuments-test-user)** pour obtenir un équivalent de Britta Simon dans NetDocuments lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1e154-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e154-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e154-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e154-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1e154-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e154-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e154-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e154-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="1e154-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="1e154-150">**Pour configurer l’authentification unique Azure AD avec NetDocuments, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e154-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="1e154-151">Dans le portail Azure, sur la page d’intégration de l’application **NetDocuments**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1e154-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1e154-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1e154-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="1e154-155">Dans la section **Domaine et URL NetDocuments**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e154-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="1e154-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e154-157">a.</span></span> <span data-ttu-id="1e154-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="1e154-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="1e154-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e154-159">b.</span></span> <span data-ttu-id="1e154-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="1e154-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e154-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1e154-161">These values are not real.</span></span> <span data-ttu-id="1e154-162">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="1e154-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="1e154-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique NetDocuments](https://support.netdocuments.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="1e154-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="1e154-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1e154-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="1e154-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1e154-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e154-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise NetDocuments en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1e154-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="1e154-169">Accédez à **Admin**.</span><span class="sxs-lookup"><span data-stu-id="1e154-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="1e154-170">Cliquez sur **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1e154-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="1e154-171">![Référentiel](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Référentiel")</span><span class="sxs-lookup"><span data-stu-id="1e154-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="1e154-172">Cliquez sur **Configure advanced authentication options**.</span><span class="sxs-lookup"><span data-stu-id="1e154-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="1e154-173">![Configurer les options d’authentification avancées](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurer les options d’authentification avancées")</span><span class="sxs-lookup"><span data-stu-id="1e154-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="1e154-174">Dans la boîte de dialogue **Identité fédérée**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e154-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="1e154-175">![Identité fédérée](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identité fédérée")</span><span class="sxs-lookup"><span data-stu-id="1e154-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="1e154-176">a.</span><span class="sxs-lookup"><span data-stu-id="1e154-176">a.</span></span> <span data-ttu-id="1e154-177">Pour **Federated identity server type**, sélectionnez **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="1e154-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="1e154-178">b.</span><span class="sxs-lookup"><span data-stu-id="1e154-178">b.</span></span> <span data-ttu-id="1e154-179">Cliquez sur **Choisir un fichier**, pour importer le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1e154-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="1e154-180">c.</span><span class="sxs-lookup"><span data-stu-id="1e154-180">c.</span></span> <span data-ttu-id="1e154-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e154-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="1e154-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1e154-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e154-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1e154-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e154-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e154-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e154-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e154-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e154-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1e154-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1e154-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e154-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e154-189">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e154-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e154-191">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1e154-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e154-193">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1e154-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e154-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e154-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e154-197">a.</span><span class="sxs-lookup"><span data-stu-id="1e154-197">a.</span></span> <span data-ttu-id="1e154-198">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e154-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e154-199">b.</span><span class="sxs-lookup"><span data-stu-id="1e154-199">b.</span></span> <span data-ttu-id="1e154-200">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e154-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e154-201">c.</span><span class="sxs-lookup"><span data-stu-id="1e154-201">c.</span></span> <span data-ttu-id="1e154-202">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1e154-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e154-203">d.</span><span class="sxs-lookup"><span data-stu-id="1e154-203">d.</span></span> <span data-ttu-id="1e154-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1e154-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="1e154-205">Création d’un utilisateur de test NetDocuments</span><span class="sxs-lookup"><span data-stu-id="1e154-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="1e154-206">Pour permettre aux utilisateurs Azure AD de se connecter à NetDocuments, vous devez les configurer dans NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="1e154-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="1e154-207">Dans le cas de NetDocuments, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="1e154-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="1e154-208">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e154-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1e154-209">Connectez-vous à votre site d’entreprise **NetDocuments** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1e154-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="1e154-210">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="1e154-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="1e154-211">![Administrateur](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="1e154-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="1e154-212">Cliquez sur **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1e154-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="1e154-213">![Référentiel](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Référentiel")</span><span class="sxs-lookup"><span data-stu-id="1e154-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="1e154-214">Dans la zone de texte **Email Address**, tapez l’adresse e-mail d’un compte Azure Active Directory valide à approvisionner, puis cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1e154-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="1e154-215">![Adresse de messagerie](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "adresse de messagerie")</span><span class="sxs-lookup"><span data-stu-id="1e154-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1e154-216">Le titulaire du compte Azure Active Directory recevra un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="1e154-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="1e154-217">Vous pouvez utiliser n’importe quels outils ou API de création de compte utilisateur, fournis par NetDocuments, pour approvisionner des comptes utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e154-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e154-218">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e154-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e154-219">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="1e154-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1e154-221">**Pour affecter Britta Simon à NetDocuments, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e154-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="1e154-222">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1e154-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1e154-224">Dans la liste des applications, sélectionnez **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="1e154-224">In the applications list, select **NetDocuments**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="1e154-226">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1e154-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1e154-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1e154-228">Click **Add** button.</span></span> <span data-ttu-id="1e154-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1e154-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1e154-231">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1e154-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e154-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1e154-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e154-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1e154-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e154-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1e154-234">Testing single sign-on</span></span>

<span data-ttu-id="1e154-235">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1e154-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e154-236">Lorsque vous cliquez sur la vignette NetDocuments dans le panneau d’accès, vous êtes automatiquement connecté à votre application NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="1e154-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="1e154-237">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e154-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e154-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1e154-238">Additional resources</span></span>

* [<span data-ttu-id="1e154-239">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e154-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e154-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1e154-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

