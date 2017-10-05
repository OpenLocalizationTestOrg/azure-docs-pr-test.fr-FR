---
title: "Didacticiel : Intégration d’Azure Active Directory à Convercent | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="494bd-103">Didacticiel : Intégration d’Azure Active Directory à Convercent</span><span class="sxs-lookup"><span data-stu-id="494bd-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="494bd-104">Dans ce didacticiel, vous allez apprendre à intégrer Convercent à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="494bd-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="494bd-105">L’intégration de Convercent à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="494bd-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="494bd-106">Dans Azure AD, vous pouvez contrôler qui a accès à Convercent.</span><span class="sxs-lookup"><span data-stu-id="494bd-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="494bd-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Convercent (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="494bd-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="494bd-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="494bd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="494bd-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="494bd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="494bd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="494bd-110">Prerequisites</span></span>

<span data-ttu-id="494bd-111">Pour configurer l’intégration d’Azure AD à Convercent, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="494bd-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="494bd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="494bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="494bd-113">Un abonnement Convercent pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="494bd-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="494bd-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="494bd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="494bd-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="494bd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="494bd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="494bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="494bd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="494bd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="494bd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="494bd-118">Scenario description</span></span>
<span data-ttu-id="494bd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="494bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="494bd-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="494bd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="494bd-121">Ajout de Convercent à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="494bd-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="494bd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="494bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="494bd-123">Ajout de Convercent à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="494bd-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="494bd-124">Pour configurer l’intégration de Convercent à Azure AD, vous devez ajouter Convercent à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="494bd-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="494bd-125">**Pour ajouter Convercent à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="494bd-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="494bd-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="494bd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="494bd-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="494bd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="494bd-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="494bd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="494bd-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="494bd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="494bd-133">Dans la zone de recherche, tapez **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="494bd-133">In the search box, type **Convercent**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="494bd-135">Dans le volet des résultats, sélectionnez **Convercent**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="494bd-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="494bd-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="494bd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="494bd-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Convercent avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="494bd-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="494bd-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Convercent équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="494bd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="494bd-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Convercent associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="494bd-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="494bd-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Username** dans Convercent.</span><span class="sxs-lookup"><span data-stu-id="494bd-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="494bd-142">Pour configurer et tester l’authentification unique Azure AD avec Convercent, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="494bd-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="494bd-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="494bd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="494bd-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="494bd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="494bd-145">**[Création d’un utilisateur de test Convercent](#creating-a-convercent-test-user)** : pour avoir un équivalent de Britta Simon dans Convercent lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="494bd-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="494bd-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="494bd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="494bd-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="494bd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="494bd-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="494bd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="494bd-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Convercent.</span><span class="sxs-lookup"><span data-stu-id="494bd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="494bd-150">**Pour configurer l’authentification unique Azure AD avec Convercent, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="494bd-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="494bd-151">Dans le portail Azure, dans la page d’intégration de l’application **Convercent**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="494bd-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="494bd-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="494bd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="494bd-155">Dans la section **Domaines et URL Convercent**, si vous souhaitez configurer l’application en **Mode initié par IDP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="494bd-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="494bd-157">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="494bd-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="494bd-158">Si vous souhaitez configurer l’application en **Mode initié par SP**, dans la section **Domaine et URL Convercent**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="494bd-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="494bd-160">a.</span><span class="sxs-lookup"><span data-stu-id="494bd-160">a.</span></span> <span data-ttu-id="494bd-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="494bd-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="494bd-162">b.</span><span class="sxs-lookup"><span data-stu-id="494bd-162">b.</span></span> <span data-ttu-id="494bd-163">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="494bd-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="494bd-164">c.</span><span class="sxs-lookup"><span data-stu-id="494bd-164">c.</span></span> <span data-ttu-id="494bd-165">Dans la zone de texte **État de relais**, tapez une valeur en respectant le format suivant : `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="494bd-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="494bd-166">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="494bd-166">These values are not the real values.</span></span> <span data-ttu-id="494bd-167">Mettez à jour ces valeurs avec l’URL de connexion, l’identificateur et l’état de relais réels.</span><span class="sxs-lookup"><span data-stu-id="494bd-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="494bd-168">Pour obtenir ces valeurs, contactez [l’équipe du support client Convercent](http://support.convercent.com).</span><span class="sxs-lookup"><span data-stu-id="494bd-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="494bd-169">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="494bd-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="494bd-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="494bd-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="494bd-173">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support Convercent](mailto:support@convercent.com) en lui fournissant les **métadonnées XML** téléchargées.</span><span class="sxs-lookup"><span data-stu-id="494bd-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="494bd-174">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="494bd-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="494bd-175">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="494bd-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="494bd-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="494bd-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="494bd-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="494bd-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="494bd-178">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="494bd-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="494bd-180">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="494bd-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="494bd-181">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="494bd-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="494bd-183">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="494bd-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="494bd-185">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="494bd-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="494bd-187">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="494bd-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="494bd-189">a.</span><span class="sxs-lookup"><span data-stu-id="494bd-189">a.</span></span> <span data-ttu-id="494bd-190">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="494bd-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="494bd-191">b.</span><span class="sxs-lookup"><span data-stu-id="494bd-191">b.</span></span> <span data-ttu-id="494bd-192">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="494bd-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="494bd-193">c.</span><span class="sxs-lookup"><span data-stu-id="494bd-193">c.</span></span> <span data-ttu-id="494bd-194">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="494bd-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="494bd-195">d.</span><span class="sxs-lookup"><span data-stu-id="494bd-195">d.</span></span> <span data-ttu-id="494bd-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="494bd-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="494bd-197">Création d’un utilisateur de test Convercent</span><span class="sxs-lookup"><span data-stu-id="494bd-197">Creating a Convercent test user</span></span>

<span data-ttu-id="494bd-198">Collaborez avec [l’équipe de support Convercent](mailto:support@convercent.com) pour ajouter les utilisateurs dans la plateforme Convercent.</span><span class="sxs-lookup"><span data-stu-id="494bd-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="494bd-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="494bd-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="494bd-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Convercent.</span><span class="sxs-lookup"><span data-stu-id="494bd-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="494bd-202">**Pour affecter Britta Simon à Convercent, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="494bd-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="494bd-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="494bd-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="494bd-205">Dans la liste des applications, sélectionnez **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="494bd-205">In the applications list, select **Convercent**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="494bd-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="494bd-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="494bd-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="494bd-209">Click **Add** button.</span></span> <span data-ttu-id="494bd-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="494bd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="494bd-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="494bd-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="494bd-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="494bd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="494bd-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="494bd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="494bd-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="494bd-215">Testing single sign-on</span></span>

<span data-ttu-id="494bd-216">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="494bd-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="494bd-217">Lorsque vous cliquez sur la mosaïque Convercent dans le volet d’accès, vous devez être connecté automatiquement à votre application Convercent.</span><span class="sxs-lookup"><span data-stu-id="494bd-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="494bd-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="494bd-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="494bd-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="494bd-219">Additional resources</span></span>

* [<span data-ttu-id="494bd-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="494bd-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="494bd-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="494bd-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

