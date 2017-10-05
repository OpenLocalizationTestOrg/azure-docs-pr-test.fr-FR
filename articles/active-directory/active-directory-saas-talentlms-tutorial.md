---
title: "Didacticiel :Intégration d’Azure Active Directory à TalentLMS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="dd86d-103">Didacticiel : Intégration d’Azure Active Directory à TalentLMS</span><span class="sxs-lookup"><span data-stu-id="dd86d-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="dd86d-104">Dans ce didacticiel, vous allez apprendre à intégrer TalentLMS à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd86d-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd86d-105">L’intégration de TalentLMS à Azure AD vous fait bénéficier des avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd86d-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd86d-106">Dans Azure AD, vous pouvez contrôler qui a accès à TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="dd86d-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="dd86d-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à TalentLMS (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd86d-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd86d-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd86d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd86d-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd86d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd86d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd86d-110">Prerequisites</span></span>

<span data-ttu-id="dd86d-111">Pour configurer l’intégration d’Azure AD à TalentLMS, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd86d-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="dd86d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd86d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd86d-113">Un abonnement TalentLMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd86d-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd86d-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd86d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd86d-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dd86d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd86d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd86d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd86d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd86d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd86d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd86d-118">Scenario description</span></span>
<span data-ttu-id="dd86d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd86d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd86d-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd86d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd86d-121">Ajout de TalentLMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dd86d-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="dd86d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd86d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="dd86d-123">Ajout de TalentLMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dd86d-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="dd86d-124">Pour configurer l’intégration de TalentLMS à Azure AD, vous devez ajouter TalentLMS à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd86d-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd86d-125">**Pour ajouter TalentLMS à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd86d-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd86d-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd86d-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd86d-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd86d-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd86d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd86d-133">Dans la zone de recherche, entrez **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-133">In the search box, type **TalentLMS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="dd86d-135">Dans le volet de résultats, sélectionnez **TalentLMS**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="dd86d-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd86d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd86d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd86d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de TalentLMS avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd86d-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd86d-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TalentLMS équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd86d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="dd86d-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur TalentLMS associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="dd86d-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="dd86d-141">Dans TalentLMS, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="dd86d-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dd86d-142">Pour configurer et tester l’authentification unique Azure AD auprès de TalentLMS, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd86d-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd86d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd86d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd86d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd86d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd86d-145">**[Création d’un utilisateur de test TalentLMS](#creating-a-talentlms-test-user)** pour avoir dans TalentLMS un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd86d-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd86d-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd86d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd86d-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="dd86d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd86d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd86d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd86d-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="dd86d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="dd86d-150">**Pour configurer l’authentification unique Azure AD auprès de TalentLMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd86d-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="dd86d-151">Dans le Portail Azure, dans la page d’intégration de l’application **TalentLMS**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd86d-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd86d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="dd86d-155">Dans la section **Domaine et URL TalentLMS**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd86d-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="dd86d-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd86d-157">a.</span></span> <span data-ttu-id="dd86d-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="dd86d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="dd86d-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd86d-159">b.</span></span> <span data-ttu-id="dd86d-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="dd86d-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd86d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="dd86d-161">These values are not real.</span></span> <span data-ttu-id="dd86d-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="dd86d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dd86d-163">Pour obtenir ces valeurs, contactez l’[équipe de support client de TalentLMS](https://www.talentlms.com/contact).</span><span class="sxs-lookup"><span data-stu-id="dd86d-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="dd86d-164">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="dd86d-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="dd86d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd86d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd86d-168">Dans la section **Configuration de TalentLMS**, cliquez sur **Configurer TalentLMS** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dd86d-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dd86d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="dd86d-171">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TalentLMS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd86d-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="dd86d-172">Dans la section **Account & Settings (Compte et paramètres)**, cliquez sur l’onglet **Users (Utilisateurs)**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="dd86d-173">![Compte et paramètres](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Compte et paramètres")</span><span class="sxs-lookup"><span data-stu-id="dd86d-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="dd86d-174">Cliquez sur **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="dd86d-175">Dans la section Single Sign-On, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd86d-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="dd86d-176">![Authentification unique](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="dd86d-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="dd86d-177">a.</span><span class="sxs-lookup"><span data-stu-id="dd86d-177">a.</span></span> <span data-ttu-id="dd86d-178">Dans la liste **SSO integration type (Type d’intégration SSO)**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="dd86d-179">b.</span><span class="sxs-lookup"><span data-stu-id="dd86d-179">b.</span></span> <span data-ttu-id="dd86d-180">Dans la zone de texte **Fournisseur d’identité**, collez la valeur de l’**ID d’entité SAML** copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd86d-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="dd86d-181">c.</span><span class="sxs-lookup"><span data-stu-id="dd86d-181">c.</span></span> <span data-ttu-id="dd86d-182">Collez la valeur de l’**empreinte** à partir du portail Azure dans la zone de texte **Empreinte du certificat**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="dd86d-183">d.</span><span class="sxs-lookup"><span data-stu-id="dd86d-183">d.</span></span>  <span data-ttu-id="dd86d-184">Dans la zone de texte **URL de connexion à distance**, collez la valeur de **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd86d-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="dd86d-185">e.</span><span class="sxs-lookup"><span data-stu-id="dd86d-185">e.</span></span> <span data-ttu-id="dd86d-186">Dans la zone de texte **URL de déconnexion à distance**, collez la valeur de **URL de déconnexion** que vous avez copiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd86d-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd86d-187">f.</span><span class="sxs-lookup"><span data-stu-id="dd86d-187">f.</span></span> <span data-ttu-id="dd86d-188">Renseignez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd86d-188">Fill in the following:</span></span> 

    * <span data-ttu-id="dd86d-189">Dans la zone de texte **TargetedID**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="dd86d-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="dd86d-190">Dans la zone de texte **Prénom**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="dd86d-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="dd86d-191">Dans la zone de texte **Nom**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="dd86d-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="dd86d-192">Dans la zone de texte **Email**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="dd86d-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="dd86d-193">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="dd86d-194">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="dd86d-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd86d-195">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="dd86d-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd86d-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd86d-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd86d-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd86d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd86d-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd86d-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd86d-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd86d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd86d-201">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd86d-203">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd86d-205">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd86d-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd86d-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd86d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd86d-209">a.</span><span class="sxs-lookup"><span data-stu-id="dd86d-209">a.</span></span> <span data-ttu-id="dd86d-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd86d-211">b.</span><span class="sxs-lookup"><span data-stu-id="dd86d-211">b.</span></span> <span data-ttu-id="dd86d-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd86d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd86d-213">c.</span><span class="sxs-lookup"><span data-stu-id="dd86d-213">c.</span></span> <span data-ttu-id="dd86d-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd86d-215">d.</span><span class="sxs-lookup"><span data-stu-id="dd86d-215">d.</span></span> <span data-ttu-id="dd86d-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="dd86d-217">Création d’un utilisateur de test TalentLMS</span><span class="sxs-lookup"><span data-stu-id="dd86d-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="dd86d-218">Pour se connecter à TalentLMS, les utilisateurs d’Azure AD doivent être approvisionnés dans TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="dd86d-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="dd86d-219">Dans le cas de TalentLMS, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="dd86d-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="dd86d-220">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd86d-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="dd86d-221">Connectez-vous à votre locataire **TalentLMS** .</span><span class="sxs-lookup"><span data-stu-id="dd86d-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="dd86d-222">Cliquez sur **Users (Utilisateurs)**, puis sur **Add User (Ajouter un utilisateur)**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="dd86d-223">Dans la boîte de dialogue **Add user** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd86d-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="dd86d-224">![Ajouter un utilisateur](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="dd86d-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="dd86d-225">a.</span><span class="sxs-lookup"><span data-stu-id="dd86d-225">a.</span></span> <span data-ttu-id="dd86d-226">Dans la zone de texte **First name**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="dd86d-227">b.</span><span class="sxs-lookup"><span data-stu-id="dd86d-227">b.</span></span> <span data-ttu-id="dd86d-228">Dans la zone de texte **Last name**, tapez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="dd86d-229">c.</span><span class="sxs-lookup"><span data-stu-id="dd86d-229">c.</span></span> <span data-ttu-id="dd86d-230">Dans la zone de texte **Email**, entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="dd86d-231">d.</span><span class="sxs-lookup"><span data-stu-id="dd86d-231">d.</span></span> <span data-ttu-id="dd86d-232">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="dd86d-233">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur, fourni par TalentLMS, pour approvisionner des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="dd86d-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd86d-234">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd86d-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd86d-235">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="dd86d-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd86d-237">**Pour affecter Britta Simon à TalentLMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd86d-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="dd86d-238">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd86d-240">Dans la liste des applications, sélectionnez **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-240">In the applications list, select **TalentLMS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="dd86d-242">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd86d-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-244">Click **Add** button.</span></span> <span data-ttu-id="dd86d-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd86d-247">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dd86d-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd86d-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd86d-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd86d-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd86d-250">Testing single sign-on</span></span>

<span data-ttu-id="dd86d-251">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd86d-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd86d-252">Lorsque vous cliquez sur la vignette TalentLMS dans le volet d’accès, vous devez être automatiquement connecté à votre application TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="dd86d-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd86d-253">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd86d-253">Additional resources</span></span>

* [<span data-ttu-id="dd86d-254">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd86d-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd86d-255">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd86d-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

