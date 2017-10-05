---
title: "Didacticiel : intégration d’Azure Active Directory à RedVector | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RedVector."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99042f39-0ab2-475b-8df8-3016d7f875e9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: d7aedd360ba1d4c11da210f8fae7be6035007c22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-redvector"></a><span data-ttu-id="7dd60-103">Didacticiel : Intégration d’Azure AD à RedVector</span><span class="sxs-lookup"><span data-stu-id="7dd60-103">Tutorial: Azure Active Directory integration with RedVector</span></span>

<span data-ttu-id="7dd60-104">Dans ce didacticiel, vous allez apprendre à intégrer RedVector avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7dd60-104">In this tutorial, you learn how to integrate RedVector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7dd60-105">L’intégration de RedVector à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7dd60-105">Integrating RedVector with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7dd60-106">Dans Azure AD, vous pouvez contrôler qui a accès à RedVector</span><span class="sxs-lookup"><span data-stu-id="7dd60-106">You can control in Azure AD who has access to RedVector</span></span>
- <span data-ttu-id="7dd60-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à RedVector (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-107">You can enable your users to automatically get signed-on to RedVector (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7dd60-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7dd60-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7dd60-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7dd60-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dd60-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7dd60-110">Prerequisites</span></span>

<span data-ttu-id="7dd60-111">Pour configurer l’intégration d’Azure AD à RedVector, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7dd60-111">To configure Azure AD integration with RedVector, you need the following items:</span></span>

- <span data-ttu-id="7dd60-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7dd60-113">Un abonnement RedVector pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7dd60-113">A RedVector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7dd60-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7dd60-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7dd60-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7dd60-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7dd60-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7dd60-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7dd60-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7dd60-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7dd60-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7dd60-118">Scenario description</span></span>
<span data-ttu-id="7dd60-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7dd60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7dd60-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7dd60-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7dd60-121">Ajout de RedVector à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7dd60-121">Adding RedVector from the gallery</span></span>
2. <span data-ttu-id="7dd60-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-redvector-from-the-gallery"></a><span data-ttu-id="7dd60-123">Ajout de RedVector à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7dd60-123">Adding RedVector from the gallery</span></span>
<span data-ttu-id="7dd60-124">Pour configurer l’intégration de RedVector avec Azure AD, vous devez ajouter RedVector, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7dd60-124">To configure the integration of RedVector into Azure AD, you need to add RedVector from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7dd60-125">**Pour ajouter RedVector à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7dd60-125">**To add RedVector from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd60-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7dd60-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7dd60-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7dd60-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7dd60-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7dd60-133">Dans la zone de recherche, tapez **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-133">In the search box, type **RedVector**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_search.png)

5. <span data-ttu-id="7dd60-135">Dans le panneau de résultats, sélectionnez **RedVector**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7dd60-135">In the results panel, select **RedVector**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7dd60-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7dd60-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RedVector, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7dd60-138">In this section, you configure and test Azure AD single sign-on with RedVector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7dd60-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur RedVector équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dd60-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RedVector is to a user in Azure AD.</span></span> <span data-ttu-id="7dd60-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur RedVector associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="7dd60-140">In other words, a link relationship between an Azure AD user and the related user in RedVector needs to be established.</span></span>

<span data-ttu-id="7dd60-141">Dans RedVector, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="7dd60-141">In RedVector, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7dd60-142">Pour configurer et tester l’authentification unique Azure AD avec RedVector, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7dd60-142">To configure and test Azure AD single sign-on with RedVector, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7dd60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7dd60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7dd60-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dd60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7dd60-145">**[Création d’un utilisateur de test RedVector](#creating-a-redvector-test-user)** pour obtenir un équivalent de Britta Simon dans RedVector lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="7dd60-145">**[Creating a RedVector test user](#creating-a-redvector-test-user)** - to have a counterpart of Britta Simon in RedVector that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7dd60-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dd60-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7dd60-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7dd60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7dd60-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7dd60-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RedVector.</span><span class="sxs-lookup"><span data-stu-id="7dd60-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RedVector application.</span></span>

<span data-ttu-id="7dd60-150">**Pour configurer l’authentification unique Azure AD avec RedVector, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7dd60-150">**To configure Azure AD single sign-on with RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd60-151">Dans le portail Azure, sur la page d’intégration de l’application **RedVector**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-151">In the Azure portal, on the **RedVector** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7dd60-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7dd60-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_samlbase.png)

3. <span data-ttu-id="7dd60-155">Dans la section **Domaine et URL RedVector**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7dd60-155">On the **RedVector Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_url.png)

    <span data-ttu-id="7dd60-157">a.</span><span class="sxs-lookup"><span data-stu-id="7dd60-157">a.</span></span> <span data-ttu-id="7dd60-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://sso2.redvector.com/adfs/<Companyname>`</span><span class="sxs-lookup"><span data-stu-id="7dd60-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso2.redvector.com/adfs/<Companyname>`</span></span>

    <span data-ttu-id="7dd60-159">b.</span><span class="sxs-lookup"><span data-stu-id="7dd60-159">b.</span></span> <span data-ttu-id="7dd60-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<Companyname>.redvector.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="7dd60-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Companyname>.redvector.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7dd60-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7dd60-161">These values are not real.</span></span> <span data-ttu-id="7dd60-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="7dd60-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7dd60-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique RedVector](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="7dd60-163">Contact [RedVector Client support team](mailto:sso@redvector.com) to get these values.</span></span> 
 
4. <span data-ttu-id="7dd60-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7dd60-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_certificate.png) 

5. <span data-ttu-id="7dd60-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7dd60-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-redvector-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7dd60-168">Dans la section **Configuration de RedVector**, cliquez sur **Configurer RedVector** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-168">On the **RedVector Configuration** section, click **Configure RedVector** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7dd60-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7dd60-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_configure.png) 

7. <span data-ttu-id="7dd60-171">Pour configurer l’authentification unique côté **RedVector**, vous devez envoyer le **Certificat (Base64)** téléchargé et **l’URL du service d’authentification unique SAML** à [l’équipe de support technique RedVector](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="7dd60-171">To configure single sign-on on **RedVector** side, you need to send the downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** to [RedVector support team](mailto:sso@redvector.com).</span></span> <span data-ttu-id="7dd60-172">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="7dd60-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7dd60-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7dd60-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7dd60-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7dd60-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7dd60-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7dd60-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7dd60-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="7dd60-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd60-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7dd60-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7dd60-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd60-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7dd60-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7dd60-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7dd60-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7dd60-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7dd60-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7dd60-188">a.</span><span class="sxs-lookup"><span data-stu-id="7dd60-188">a.</span></span> <span data-ttu-id="7dd60-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7dd60-190">b.</span><span class="sxs-lookup"><span data-stu-id="7dd60-190">b.</span></span> <span data-ttu-id="7dd60-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dd60-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7dd60-192">c.</span><span class="sxs-lookup"><span data-stu-id="7dd60-192">c.</span></span> <span data-ttu-id="7dd60-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7dd60-194">d.</span><span class="sxs-lookup"><span data-stu-id="7dd60-194">d.</span></span> <span data-ttu-id="7dd60-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-195">Click **Create**.</span></span>
 
### <a name="creating-a-redvector-test-user"></a><span data-ttu-id="7dd60-196">Création d’un utilisateur de test RedVector</span><span class="sxs-lookup"><span data-stu-id="7dd60-196">Creating a RedVector test user</span></span>

<span data-ttu-id="7dd60-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans RedVector.</span><span class="sxs-lookup"><span data-stu-id="7dd60-197">In this section, you create a user called Britta Simon in RedVector.</span></span> <span data-ttu-id="7dd60-198">Si vous ne savez pas comment ajouter Britta Simon dans RedVector, rapprochez-vous de [l’équipe de support RedVector](mailto:sso@redvector.com) pour ajouter l’utilisateur de test et activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7dd60-198">If you don't know how to add Britta Simon in RedVector, Work with [RedVector support team](mailto:sso@redvector.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7dd60-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd60-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7dd60-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RedVector.</span><span class="sxs-lookup"><span data-stu-id="7dd60-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RedVector.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7dd60-202">**Pour affecter Britta Simon à RedVector, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7dd60-202">**To assign Britta Simon to RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd60-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7dd60-205">Dans la liste des applications, sélectionnez **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-205">In the applications list, select **RedVector**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_app.png) 

3. <span data-ttu-id="7dd60-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7dd60-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-209">Click **Add** button.</span></span> <span data-ttu-id="7dd60-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7dd60-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7dd60-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7dd60-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7dd60-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7dd60-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7dd60-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7dd60-215">Testing single sign-on</span></span>

<span data-ttu-id="7dd60-216">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7dd60-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7dd60-217">Lorsque vous cliquez sur la vignette RedVector dans le panneau d’accès, vous êtes automatiquement connecté à votre application RedVector.</span><span class="sxs-lookup"><span data-stu-id="7dd60-217">When you click the RedVector tile in the Access Panel, you should get automatically signed-on to your RedVector application..</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7dd60-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7dd60-218">Additional resources</span></span>

* [<span data-ttu-id="7dd60-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7dd60-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7dd60-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7dd60-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_203.png

