---
title: "Didacticiel : Intégration d’Azure Active Directory à 10,000ft Plans | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et 10,000ft Plans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="dd9c0-103">Didacticiel : Intégration d’Azure Active Directory à 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="dd9c0-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="dd9c0-104">Dans ce didacticiel, vous allez apprendre à intégrer 10,000ft Plans à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd9c0-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd9c0-105">L’intégration de 10,000ft Plans avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd9c0-106">Vous pouvez contrôler qui a accès à 10,000ft Plans dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="dd9c0-107">Vous pouvez permettre à vos utilisateurs de se connecter automatiquement à 10,000ft Plans (en connexion unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd9c0-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd9c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd9c0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd9c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd9c0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd9c0-110">Prerequisites</span></span>

<span data-ttu-id="dd9c0-111">Pour configurer l’intégration d’Azure AD avec 10,000ft Plans, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="dd9c0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd9c0-113">Un abonnement à 10,000ft Plans pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd9c0-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd9c0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd9c0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd9c0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd9c0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’un mois.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd9c0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd9c0-118">Scenario description</span></span>
<span data-ttu-id="dd9c0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd9c0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd9c0-121">Ajout de 10,000ft Plans à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dd9c0-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="dd9c0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="dd9c0-123">Ajout de 10,000ft Plans à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dd9c0-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="dd9c0-124">Pour configurer l’intégration de 10,000ft Plans à Azure AD, vous devez ajouter 10,000ft Plans à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd9c0-125">**Pour ajouter 10,000ft Plans à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c0-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd9c0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd9c0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd9c0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd9c0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd9c0-133">Dans la zone de recherche, tapez **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="dd9c0-135">Dans le panneau de résultats, sélectionnez **10,000ft Plans**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd9c0-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd9c0-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 10,000ft Plans avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd9c0-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd9c0-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur 10,000ft Plans équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="dd9c0-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur 10,000ft Plans associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="dd9c0-141">Dans 10,000ft Plans, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dd9c0-142">Pour configurer et tester l’authentification unique Azure AD avec 10,000ft Plans, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd9c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd9c0-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd9c0-145">**[Création d’un utilisateur de test 10,000ft Plans](#creating-a-10000ft-plans-test-user)** pour avoir un équivalent de Britta Simon dans 10,000ft Plans lié à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd9c0-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd9c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd9c0-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd9c0-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="dd9c0-150">**Pour configurer l’authentification unique Azure AD avec 10,000ft Plans, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="dd9c0-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="dd9c0-151">Dans le portail Azure, dans la page d’intégration de l’application **10,000ft Plans**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd9c0-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="dd9c0-155">Dans la section **Domaine et URL 10,000ft Plans**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="dd9c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-157">a.</span></span> <span data-ttu-id="dd9c0-158">Dans la zone de texte **URL de connexion**, tapez l’URL : `https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="dd9c0-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="dd9c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-159">b.</span></span> <span data-ttu-id="dd9c0-160">Dans la zone de texte **Identificateur**, tapez l’URL : `https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="dd9c0-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd9c0-161">La valeur de **l’identificateur** est différente si vous avez un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="dd9c0-162">Pour obtenir cette valeur, contactez [l’équipe du support 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="dd9c0-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="dd9c0-163">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="dd9c0-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd9c0-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd9c0-167">Dans la section **Configuration de 10,000ft Plans**, cliquez sur **Configurer 10,000ft** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dd9c0-168">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dd9c0-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="dd9c0-170">Pour configurer l’authentification unique côté **10,000ft Plans**, vous devez envoyer le **Certificat (brut) téléchargé, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe du support 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="dd9c0-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="dd9c0-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd9c0-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd9c0-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd9c0-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd9c0-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd9c0-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd9c0-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c0-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd9c0-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd9c0-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd9c0-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd9c0-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd9c0-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd9c0-186">a.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-186">a.</span></span> <span data-ttu-id="dd9c0-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd9c0-188">b.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-188">b.</span></span> <span data-ttu-id="dd9c0-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd9c0-190">c.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-190">c.</span></span> <span data-ttu-id="dd9c0-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd9c0-192">d.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-192">d.</span></span> <span data-ttu-id="dd9c0-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="dd9c0-194">Création d’un utilisateur de test 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="dd9c0-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="dd9c0-195">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="dd9c0-196">10,000ft Plans prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="dd9c0-197">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-197">There is no action item for you in this section.</span></span> <span data-ttu-id="dd9c0-198">Un utilisateur est créé lors d’une tentative d’accès à 10,000ft Plans s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd9c0-199">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="dd9c0-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd9c0-200">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c0-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd9c0-201">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd9c0-203">**Pour affecter Britta Simon à 10,000ft Plans, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c0-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="dd9c0-204">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd9c0-206">Dans la liste des applications, sélectionnez **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="dd9c0-208">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd9c0-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-210">Click **Add** button.</span></span> <span data-ttu-id="dd9c0-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd9c0-213">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd9c0-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd9c0-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd9c0-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd9c0-216">Testing single sign-on</span></span>

<span data-ttu-id="dd9c0-217">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="dd9c0-218">Lorsque vous cliquez sur la vignette 10,000ft Plans dans le volet d’accès, vous devez être connecté automatiquement à votre application 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="dd9c0-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="dd9c0-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd9c0-219">Additional resources</span></span>

* [<span data-ttu-id="dd9c0-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd9c0-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd9c0-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd9c0-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

