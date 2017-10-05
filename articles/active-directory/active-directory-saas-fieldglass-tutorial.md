---
title: "Didacticiel : Intégration d’Azure Active Directory à Fieldglass | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Fieldglass."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 18926dd88b19cd672f11ae05f18e354e79a6b397
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="5b55c-103">Didacticiel : Intégration d’Azure Active Directory à Fieldglass</span><span class="sxs-lookup"><span data-stu-id="5b55c-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="5b55c-104">Dans ce didacticiel, vous allez apprendre à intégrer Fieldglass à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b55c-104">In this tutorial, you learn how to integrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b55c-105">L’intégration de Fieldglass à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5b55c-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b55c-106">Dans Azure AD, vous pouvez contrôler qui a accès à Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5b55c-106">You can control in Azure AD who has access to Fieldglass</span></span>
- <span data-ttu-id="5b55c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Fieldglass (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b55c-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b55c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5b55c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5b55c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b55c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b55c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5b55c-110">Prerequisites</span></span>

<span data-ttu-id="5b55c-111">Pour configurer l’intégration d’Azure AD à Fieldglass, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5b55c-111">To configure Azure AD integration with Fieldglass, you need the following items:</span></span>

- <span data-ttu-id="5b55c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b55c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b55c-113">Un abonnement Fieldglass pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5b55c-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b55c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5b55c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b55c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b55c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b55c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5b55c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b55c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b55c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b55c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5b55c-118">Scenario description</span></span>
<span data-ttu-id="5b55c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5b55c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b55c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b55c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b55c-121">Ajout de Fieldglass à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5b55c-121">Adding Fieldglass from the gallery</span></span>
2. <span data-ttu-id="5b55c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b55c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-the-gallery"></a><span data-ttu-id="5b55c-123">Ajout de Fieldglass à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5b55c-123">Adding Fieldglass from the gallery</span></span>
<span data-ttu-id="5b55c-124">Pour configurer l’intégration de Fieldglass à Azure AD, vous devez ajouter Fieldglass à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5b55c-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b55c-125">**Pour ajouter Fieldglass à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b55c-125">**To add Fieldglass from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b55c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b55c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b55c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5b55c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5b55c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5b55c-133">Dans la zone de recherche, tapez **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-133">In the search box, type **Fieldglass**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_search.png)

5. <span data-ttu-id="5b55c-135">Dans le panneau de résultats, sélectionnez **Fieldglass**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5b55c-135">In the results panel, select **Fieldglass**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b55c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b55c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b55c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Fieldglass à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5b55c-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5b55c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Fieldglass équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b55c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass is to a user in Azure AD.</span></span> <span data-ttu-id="5b55c-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Fieldglass associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5b55c-140">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span></span>

<span data-ttu-id="5b55c-141">Dans Fieldglass, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5b55c-141">In Fieldglass, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b55c-142">Pour configurer et tester l’authentification unique Azure AD avec Fieldglass, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b55c-142">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b55c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5b55c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b55c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b55c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b55c-145">**[Création d’un utilisateur de test Fieldglass](#creating-a-fieldglass-test-user)** pour avoir un équivalent de Britta Simon dans Fieldglass lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b55c-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b55c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b55c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b55c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5b55c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b55c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b55c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b55c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5b55c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="5b55c-150">**Pour configurer l’authentification unique Azure AD avec Fieldglass, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b55c-150">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="5b55c-151">Dans le portail Azure, sur la page d’intégration de l’application **Fieldglass**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-151">In the Azure portal, on the **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5b55c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5b55c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

3. <span data-ttu-id="5b55c-155">Dans la section **Fieldglass Domain and URLs** (Domaine et URL Fieldglass), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b55c-155">On the **Fieldglass Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="5b55c-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b55c-157">a.</span></span> <span data-ttu-id="5b55c-158">Dans la zone de texte **Identificateur**, entrez une URL comme `https://www.fieldglass.com` ou suivez le modèle : `https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="5b55c-158">In the **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow the pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="5b55c-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b55c-159">b.</span></span> <span data-ttu-id="5b55c-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="5b55c-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="5b55c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5b55c-161">These values are not real.</span></span> <span data-ttu-id="5b55c-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="5b55c-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5b55c-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Fieldglass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="5b55c-163">Contact [Fieldglass support team](http://www.fieldglass.com/solutions/support) to get these values.</span></span>
 
4. <span data-ttu-id="5b55c-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5b55c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

5. <span data-ttu-id="5b55c-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5b55c-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fieldglass-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b55c-168">Dans la section **Fieldglass Configuration** (Configuration de Fieldglass), cliquez sur **Configure Fieldglass** (Configurer Fieldglass) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-168">On the **Fieldglass Configuration** section, click **Configure Fieldglass** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5b55c-169">Copiez **l’URL de déconnexion et l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-169">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_configure.png) 

7. <span data-ttu-id="5b55c-171">Pour configurer l’authentification unique du côté **Fieldglass**, vous devez envoyer le **certificat (Base64)** téléchargé et **l’URL de déconnexion et l’ID d’entité SAML** à [l’équipe de support technique Fieldglass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="5b55c-171">To configure single sign-on on **Fieldglass** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** to [Fieldglass support team](http://www.fieldglass.com/solutions/support).</span></span> <span data-ttu-id="5b55c-172">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="5b55c-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5b55c-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5b55c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b55c-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5b55c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b55c-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b55c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b55c-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b55c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b55c-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b55c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5b55c-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b55c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b55c-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b55c-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b55c-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5b55c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b55c-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b55c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b55c-188">a.</span><span class="sxs-lookup"><span data-stu-id="5b55c-188">a.</span></span> <span data-ttu-id="5b55c-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b55c-190">b.</span><span class="sxs-lookup"><span data-stu-id="5b55c-190">b.</span></span> <span data-ttu-id="5b55c-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b55c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b55c-192">c.</span><span class="sxs-lookup"><span data-stu-id="5b55c-192">c.</span></span> <span data-ttu-id="5b55c-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5b55c-194">d.</span><span class="sxs-lookup"><span data-stu-id="5b55c-194">d.</span></span> <span data-ttu-id="5b55c-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="5b55c-196">Création d’un utilisateur de test Fieldglass</span><span class="sxs-lookup"><span data-stu-id="5b55c-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="5b55c-197">L’objectif de cette section est de créer un utilisateur nommé Britta Simon dans FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="5b55c-197">The objective of this section is to create a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="5b55c-198">Travaillez avec [l’équipe de support technique FieldGlass](http://www.fieldglass.com/solutions/support) pour ajouter les utilisateurs au compte FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="5b55c-198">Please work with your [Fieldglass support team](http://www.fieldglass.com/solutions/support) to add the users in the Fieldglass account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5b55c-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b55c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5b55c-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="5b55c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fieldglass.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5b55c-202">**Pour affecter Britta Simon à Fieldglass, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b55c-202">**To assign Britta Simon to Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="5b55c-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5b55c-205">Dans la liste des applications, sélectionnez **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-205">In the applications list, select **Fieldglass**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_app.png) 

3. <span data-ttu-id="5b55c-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5b55c-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-209">Click **Add** button.</span></span> <span data-ttu-id="5b55c-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5b55c-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5b55c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b55c-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b55c-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5b55c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b55c-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5b55c-215">Testing single sign-on</span></span>

<span data-ttu-id="5b55c-216">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b55c-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b55c-217">Si vous cliquez sur la mosaïque Fieldglass dans le volet d’accès, vous devez être connecté automatiquement à votre application Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5b55c-217">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b55c-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5b55c-218">Additional resources</span></span>

* [<span data-ttu-id="5b55c-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b55c-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b55c-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5b55c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png

