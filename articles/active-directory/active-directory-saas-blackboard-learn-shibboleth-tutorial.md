---
title: "Didacticiel : Intégration d’Azure Active Directory à Blackboard Learn - Shibboleth | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Blackboard Learn - Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 014b0671eb8604235a823c2cf4324a49d94df702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="0f948-103">Didacticiel : Intégration d’Azure Active Directory à Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="0f948-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="0f948-104">Dans ce didacticiel, vous allez apprendre à intégrer Blackboard Learn - Shibboleth à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f948-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f948-105">L’intégration de Blackboard Learn- Shibboleth dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0f948-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0f948-106">Dans Azure AD, vous pouvez contrôler qui a accès à Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="0f948-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="0f948-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Blackboard Learn - Shibboleth (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f948-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0f948-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0f948-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f948-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f948-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0f948-110">Prerequisites</span></span>

<span data-ttu-id="0f948-111">Pour configurer l’intégration d’Azure AD à Blackboard Learn - Shibboleth, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0f948-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="0f948-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f948-113">Un abonnement actif à connexion unique à Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="0f948-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f948-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0f948-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f948-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0f948-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f948-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0f948-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f948-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f948-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f948-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0f948-118">Scenario description</span></span>
<span data-ttu-id="0f948-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0f948-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f948-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f948-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f948-121">Ajout de Blackboard Learn - Shibboleth à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0f948-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="0f948-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="0f948-123">Ajout de Blackboard Learn - Shibboleth à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0f948-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="0f948-124">Pour configurer l’intégration de Blackboard Learn - Shibboleth à Azure AD, vous devez ajouter Blackboard Learn - Shibboleth de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0f948-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0f948-125">**Pour ajouter Blackboard Learn - Shibboleth à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0f948-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0f948-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f948-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f948-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0f948-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0f948-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0f948-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0f948-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0f948-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0f948-133">Dans la zone de recherche, tapez **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="0f948-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="0f948-135">Dans le volet de résultats, sélectionnez **Blackboard Learn - Shibboleth**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0f948-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f948-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f948-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Blackboard Learn - Shibboleth avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0f948-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0f948-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Blackboard Learn - Shibboleth équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f948-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="0f948-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Blackboard Learn - Shibboleth associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0f948-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="0f948-141">Dans Blackboard Learn - Shibboleth, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="0f948-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0f948-142">Pour configurer et tester l’authentification unique Azure AD avec Blackboard Learn - Shibboleth, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f948-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0f948-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0f948-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0f948-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f948-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f948-145">**[Création d’un utilisateur de test Blackboard Learn - Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)** pour avoir un équivalent de Britta Simon dans Blackboard Learn - Shibboleth lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="0f948-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f948-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f948-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f948-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0f948-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f948-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f948-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="0f948-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="0f948-150">**Pour configurer l’authentification unique Azure AD avec Blackboard Learn - Shibboleth, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0f948-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="0f948-151">Dans le portail Azure, dans la page d’intégration de l’application **Blackboard Learn - Shibboleth**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0f948-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0f948-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0f948-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="0f948-155">Dans la section **Domaine et URL Blackboard Learn - Shibboleth**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f948-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="0f948-157">a.</span><span class="sxs-lookup"><span data-stu-id="0f948-157">a.</span></span> <span data-ttu-id="0f948-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="0f948-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="0f948-159">b.</span><span class="sxs-lookup"><span data-stu-id="0f948-159">b.</span></span> <span data-ttu-id="0f948-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="0f948-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="0f948-161">c.</span><span class="sxs-lookup"><span data-stu-id="0f948-161">c.</span></span> <span data-ttu-id="0f948-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="0f948-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="0f948-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="0f948-163">These values are not real.</span></span> <span data-ttu-id="0f948-164">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="0f948-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0f948-165">Pour obtenir ces valeurs, contactez [l’équipe du support Blackboard Learn - Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f948-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

4. <span data-ttu-id="0f948-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0f948-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="0f948-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0f948-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0f948-170">Dans la section **Configuration de Blackboard Learn - Shibboleth**, cliquez sur **Configurer Blackboard Learn - Shibboleth** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0f948-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0f948-171">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="0f948-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="0f948-173">Pour configurer l’authentification unique côté **Blackboard Learn - Shibboleth**, vous devez envoyer le fichier **XML de métadonnées** téléchargé, **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe du support Blackboard Learn - Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f948-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="0f948-174">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="0f948-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0f948-175">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="0f948-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0f948-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f948-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f948-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f948-178">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f948-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0f948-180">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0f948-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0f948-181">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f948-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f948-183">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0f948-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f948-185">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0f948-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f948-187">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f948-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f948-189">a.</span><span class="sxs-lookup"><span data-stu-id="0f948-189">a.</span></span> <span data-ttu-id="0f948-190">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f948-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f948-191">b.</span><span class="sxs-lookup"><span data-stu-id="0f948-191">b.</span></span> <span data-ttu-id="0f948-192">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f948-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f948-193">c.</span><span class="sxs-lookup"><span data-stu-id="0f948-193">c.</span></span> <span data-ttu-id="0f948-194">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0f948-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0f948-195">d.</span><span class="sxs-lookup"><span data-stu-id="0f948-195">d.</span></span> <span data-ttu-id="0f948-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0f948-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="0f948-197">Création d’un utilisateur de test Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="0f948-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="0f948-198">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="0f948-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="0f948-199">Pour ajouter des utilisateurs dans la plateforme Blackboard Learn - Shibboleth, contactez [l’équipe du support Blackboard Learn - Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f948-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0f948-200">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f948-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0f948-201">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="0f948-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0f948-203">**Pour affecter Britta Simon à Blackboard Learn - Shibboleth, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0f948-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="0f948-204">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0f948-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0f948-206">Dans la liste des applications, sélectionnez **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="0f948-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="0f948-208">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0f948-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0f948-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0f948-210">Click **Add** button.</span></span> <span data-ttu-id="0f948-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0f948-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0f948-213">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0f948-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0f948-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0f948-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f948-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0f948-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f948-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0f948-216">Testing single sign-on</span></span>

<span data-ttu-id="0f948-217">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0f948-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0f948-218">Lorsque vous cliquez sur la vignette Blackboard Learn - Shibboleth dans le volet d’accès, vous devez être connecté automatiquement à votre application Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="0f948-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f948-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0f948-219">Additional resources</span></span>

* [<span data-ttu-id="0f948-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f948-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f948-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0f948-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

