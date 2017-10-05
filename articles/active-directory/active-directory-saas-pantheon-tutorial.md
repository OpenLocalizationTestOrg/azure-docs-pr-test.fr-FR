---
title: "Didacticiel : Intégration d’Azure Active Directory à Pantheon | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="81ef8-103">Didacticiel : Intégration d’Azure Active Directory à Pantheon</span><span class="sxs-lookup"><span data-stu-id="81ef8-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="81ef8-104">Dans ce didacticiel, vous allez apprendre à intégrer Pantheon à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81ef8-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81ef8-105">L’intégration de Pantheon dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="81ef8-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81ef8-106">Dans Azure AD, vous pouvez contrôler qui a accès à Pantheon</span><span class="sxs-lookup"><span data-stu-id="81ef8-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="81ef8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Pantheon (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81ef8-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="81ef8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81ef8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81ef8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81ef8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="81ef8-110">Prerequisites</span></span>

<span data-ttu-id="81ef8-111">Pour configurer l’intégration d’Azure AD à Pantheon, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="81ef8-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="81ef8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81ef8-113">Un abonnement Pantheon pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="81ef8-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81ef8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="81ef8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81ef8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="81ef8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81ef8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="81ef8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81ef8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81ef8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81ef8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="81ef8-118">Scenario description</span></span>
<span data-ttu-id="81ef8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="81ef8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81ef8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="81ef8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81ef8-121">Ajout de Pantheon à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="81ef8-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="81ef8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="81ef8-123">Ajout de Pantheon à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="81ef8-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="81ef8-124">Pour configurer l’intégration de Pantheon avec Azure AD, vous devez ajouter Pantheon à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="81ef8-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81ef8-125">**Pour ajouter Pantheon à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81ef8-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81ef8-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81ef8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81ef8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="81ef8-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="81ef8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="81ef8-133">Dans le champ de recherche, tapez **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-133">In the search box, type **Pantheon**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="81ef8-135">Dans le panneau des résultats, sélectionnez **Pantheon**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="81ef8-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81ef8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81ef8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pantheon avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="81ef8-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81ef8-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Pantheon équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ef8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="81ef8-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Pantheon associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="81ef8-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="81ef8-141">Dans Pantheon, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="81ef8-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81ef8-142">Pour configurer et tester l’authentification unique Azure AD avec Pantheon, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="81ef8-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81ef8-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="81ef8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81ef8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81ef8-145">**[Création d’un utilisateur de test Pantheon](#creating-a-pantheon-test-user)** pour obtenir un équivalent de Britta Simon dans Pantheon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="81ef8-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81ef8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ef8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81ef8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="81ef8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81ef8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81ef8-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Pantheon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="81ef8-150">**Pour configurer l’authentification unique Azure AD avec Pantheon, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81ef8-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="81ef8-151">Dans le Portail Azure, sur la page d’intégration de l’application **Pantheon**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="81ef8-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81ef8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="81ef8-155">Dans la section **Domaine et URL Pantheon**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="81ef8-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="81ef8-157">a.</span><span class="sxs-lookup"><span data-stu-id="81ef8-157">a.</span></span> <span data-ttu-id="81ef8-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="81ef8-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="81ef8-159">b.</span><span class="sxs-lookup"><span data-stu-id="81ef8-159">b.</span></span> <span data-ttu-id="81ef8-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="81ef8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81ef8-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="81ef8-161">These values are not real.</span></span> <span data-ttu-id="81ef8-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="81ef8-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="81ef8-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Pantheon](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="81ef8-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="81ef8-164">L’application Pantheon attend l’assertion SAML dans un format spécifique. Vous devez donc définir la valeur de l’attribut UserIdentifier avec l’adresse e-mail de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81ef8-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="81ef8-165">Par défaut, Azure AD utilise UserPrincipalName pour l’attribut UserIdentifier.</span><span class="sxs-lookup"><span data-stu-id="81ef8-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="81ef8-166">Mais pour une intégration réussie, vous devez ajuster cette valeur pour la faire correspondre à l’adresse électronique de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81ef8-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="81ef8-167">L’intégration ne fonctionnera qu’une fois le mappage correct effectué.</span><span class="sxs-lookup"><span data-stu-id="81ef8-167">The integration will only work after doing the correct mapping.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="81ef8-169">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="81ef8-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="81ef8-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="81ef8-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="81ef8-173">Dans la section **Configuration de Pantheon**, cliquez sur **Configurer Pantheon** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81ef8-174">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="81ef8-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="81ef8-176">Pour configurer l’authentification unique côté **Pantheon**, vous devez envoyer le **Certificat** téléchargé et **l’URL du service d’authentification unique SAML** à [l’équipe de support technique Pantheon](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="81ef8-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="81ef8-177">Vous devez également fournir les informations des domaines de messagerie et des dates/heures auxquelles vous souhaitez activer cette connexion.</span><span class="sxs-lookup"><span data-stu-id="81ef8-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="81ef8-178">Vous trouverez plus de détails à ce propos [ici](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="81ef8-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="81ef8-179">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="81ef8-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81ef8-180">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="81ef8-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81ef8-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81ef8-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81ef8-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="81ef8-183">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="81ef8-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="81ef8-185">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81ef8-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81ef8-186">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81ef8-188">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81ef8-190">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="81ef8-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81ef8-192">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="81ef8-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81ef8-194">a.</span><span class="sxs-lookup"><span data-stu-id="81ef8-194">a.</span></span> <span data-ttu-id="81ef8-195">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81ef8-196">b.</span><span class="sxs-lookup"><span data-stu-id="81ef8-196">b.</span></span> <span data-ttu-id="81ef8-197">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81ef8-198">c.</span><span class="sxs-lookup"><span data-stu-id="81ef8-198">c.</span></span> <span data-ttu-id="81ef8-199">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81ef8-200">d.</span><span class="sxs-lookup"><span data-stu-id="81ef8-200">d.</span></span> <span data-ttu-id="81ef8-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="81ef8-202">Création d’un utilisateur de test Pantheon</span><span class="sxs-lookup"><span data-stu-id="81ef8-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="81ef8-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Pantheon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="81ef8-204">Suivez les étapes ci-dessous pour ajouter l’utilisateur dans Pantheon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="81ef8-205">Pour que l’authentification unique fonctionne, vous devez d’abord créer un utilisateur dans Pantheon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="81ef8-206">Connectez-vous à Pantheon avec les informations d’identification de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="81ef8-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="81ef8-207">Accédez à la page de tableau de bord **Organisation**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="81ef8-208">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-208">Click **People**.</span></span>

4. <span data-ttu-id="81ef8-209">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-209">Click **Add user**.</span></span>

5. <span data-ttu-id="81ef8-210">Saisissez l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81ef8-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="81ef8-211">Choisissez le rôle de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81ef8-211">Choose the user's role.</span></span>

7. <span data-ttu-id="81ef8-212">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81ef8-213">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ef8-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81ef8-214">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Pantheon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="81ef8-216">**Pour affecter Britta Simon à Pantheon, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81ef8-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="81ef8-217">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="81ef8-219">Dans la liste des applications, sélectionnez **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-219">In the applications list, select **Pantheon**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="81ef8-221">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="81ef8-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-223">Click **Add** button.</span></span> <span data-ttu-id="81ef8-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="81ef8-226">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="81ef8-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81ef8-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81ef8-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="81ef8-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81ef8-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="81ef8-229">Testing single sign-on</span></span>

<span data-ttu-id="81ef8-230">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="81ef8-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81ef8-231">Quand vous cliquez sur la vignette Pantheon dans le volet d’accès, vous devez être connecté automatiquement à votre application Pantheon.</span><span class="sxs-lookup"><span data-stu-id="81ef8-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="81ef8-232">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81ef8-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="81ef8-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="81ef8-233">Additional resources</span></span>

* [<span data-ttu-id="81ef8-234">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81ef8-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81ef8-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="81ef8-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

