---
title: "Didacticiel : Intégration d’Azure Active Directory à Weekdone | Microsoft Azure"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="628cf-103">Didacticiel : Intégration d’Azure Active Directory à Weekdone</span><span class="sxs-lookup"><span data-stu-id="628cf-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="628cf-104">Dans ce didacticiel, vous allez découvrir comment intégrer Weekdone à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="628cf-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="628cf-105">L’intégration de Weekdone à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="628cf-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="628cf-106">Dans Azure AD, vous pouvez contrôler qui a accès à Weekdone.</span><span class="sxs-lookup"><span data-stu-id="628cf-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="628cf-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Weekdone (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="628cf-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="628cf-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="628cf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="628cf-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="628cf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="628cf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="628cf-110">Prerequisites</span></span>

<span data-ttu-id="628cf-111">Pour configurer l’intégration d’Azure AD à Weekdone, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="628cf-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="628cf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="628cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="628cf-113">Un abonnement Weekdone pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="628cf-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="628cf-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="628cf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="628cf-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="628cf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="628cf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="628cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="628cf-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="628cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="628cf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="628cf-118">Scenario description</span></span>
<span data-ttu-id="628cf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="628cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="628cf-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="628cf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="628cf-121">Ajout de Weekdone à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="628cf-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="628cf-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="628cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="628cf-123">Ajout de Weekdone à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="628cf-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="628cf-124">Pour configurer l’intégration de Weekdone à Azure AD, vous devez ajouter Weekdone à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="628cf-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="628cf-125">**Pour ajouter Weekdone à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628cf-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="628cf-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="628cf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="628cf-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="628cf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="628cf-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="628cf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="628cf-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="628cf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="628cf-133">Dans la zone de recherche, tapez **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="628cf-133">In the search box, type **Weekdone**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="628cf-135">Dans le volet de résultats, sélectionnez **Weekdone**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="628cf-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="628cf-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="628cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="628cf-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Weekdone avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="628cf-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="628cf-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Weekdone équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="628cf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="628cf-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Weekdone associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="628cf-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="628cf-141">Dans Weekdone, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="628cf-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="628cf-142">Pour configurer et tester l’authentification unique Azure AD avec Weekdone, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="628cf-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="628cf-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="628cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="628cf-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="628cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="628cf-145">**[Création d’un utilisateur de test Weekdone](#creating-a-weekdone-test-user)** pour avoir un équivalent de Britta Simon dans Weekdone lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="628cf-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="628cf-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="628cf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="628cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="628cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="628cf-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="628cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="628cf-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Weekdone.</span><span class="sxs-lookup"><span data-stu-id="628cf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="628cf-150">**Pour configurer l’authentification unique Azure AD avec Weekdone, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628cf-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="628cf-151">Dans le portail Azure, dans la page d’intégration de l’application **Weekdone**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="628cf-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="628cf-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="628cf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="628cf-155">Dans la section **Domaine et URL Weekdone**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="628cf-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="628cf-157">a.</span><span class="sxs-lookup"><span data-stu-id="628cf-157">a.</span></span> <span data-ttu-id="628cf-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="628cf-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="628cf-159">b.</span><span class="sxs-lookup"><span data-stu-id="628cf-159">b.</span></span> <span data-ttu-id="628cf-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="628cf-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="628cf-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="628cf-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="628cf-162">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="628cf-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="628cf-164">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="628cf-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="628cf-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="628cf-165">These values are not real.</span></span> <span data-ttu-id="628cf-166">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="628cf-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="628cf-167">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="628cf-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="628cf-168">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="628cf-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="628cf-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="628cf-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="628cf-172">Pour ouvrir la fenêtre **Configurer l’authentification**, dans la section **Configuration de Weekdone**, cliquez sur **Configurer Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="628cf-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="628cf-173">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="628cf-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="628cf-175">Pour configurer l’authentification unique côté **Weekdone**, vous devez envoyer le **XML de métadonnées, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** téléchargés à l’[équipe de support technique de Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="628cf-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="628cf-176">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="628cf-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="628cf-177">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="628cf-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="628cf-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="628cf-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="628cf-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="628cf-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="628cf-180">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="628cf-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="628cf-182">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628cf-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="628cf-183">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="628cf-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="628cf-185">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="628cf-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="628cf-187">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="628cf-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="628cf-189">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="628cf-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="628cf-191">a.</span><span class="sxs-lookup"><span data-stu-id="628cf-191">a.</span></span> <span data-ttu-id="628cf-192">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="628cf-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="628cf-193">b.</span><span class="sxs-lookup"><span data-stu-id="628cf-193">b.</span></span> <span data-ttu-id="628cf-194">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="628cf-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="628cf-195">c.</span><span class="sxs-lookup"><span data-stu-id="628cf-195">c.</span></span> <span data-ttu-id="628cf-196">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="628cf-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="628cf-197">d.</span><span class="sxs-lookup"><span data-stu-id="628cf-197">d.</span></span> <span data-ttu-id="628cf-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="628cf-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="628cf-199">Création d’un utilisateur de test Weekdone</span><span class="sxs-lookup"><span data-stu-id="628cf-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="628cf-200">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Weekdone.</span><span class="sxs-lookup"><span data-stu-id="628cf-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="628cf-201">Weekdone prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="628cf-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="628cf-202">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="628cf-202">There is no action item for you in this section.</span></span> <span data-ttu-id="628cf-203">Un utilisateur est créé lors d’une tentative d’accès à Weekdone s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="628cf-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="628cf-204">Si vous devez créer un utilisateur manuellement, contactez l’[équipe de support technique de Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="628cf-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="628cf-205">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="628cf-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="628cf-206">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Weekdone.</span><span class="sxs-lookup"><span data-stu-id="628cf-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="628cf-208">**Pour affecter Britta Simon à Weekdone, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628cf-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="628cf-209">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="628cf-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="628cf-211">Dans la liste des applications, sélectionnez **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="628cf-211">In the applications list, select **Weekdone**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="628cf-213">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="628cf-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="628cf-215">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="628cf-215">Click **Add** button.</span></span> <span data-ttu-id="628cf-216">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="628cf-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="628cf-218">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="628cf-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="628cf-219">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="628cf-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="628cf-220">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="628cf-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="628cf-221">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="628cf-221">Testing single sign-on</span></span>

<span data-ttu-id="628cf-222">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="628cf-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="628cf-223">Quand vous cliquez sur la vignette Weekdone dans le volet d’accès, vous devez être connecté automatiquement à votre application Weekdone.</span><span class="sxs-lookup"><span data-stu-id="628cf-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="628cf-224">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="628cf-224">Additional resources</span></span>

* [<span data-ttu-id="628cf-225">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="628cf-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="628cf-226">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="628cf-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

