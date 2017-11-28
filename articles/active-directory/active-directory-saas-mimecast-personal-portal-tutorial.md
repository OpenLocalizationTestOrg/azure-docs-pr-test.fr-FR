---
title: "Didacticiel : Intégration d’Azure Active Directory avec Mimecast Personal Portal | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Mimecast Personal Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="c4add-103">Didacticiel : Intégration d’Azure Active Directory avec Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="c4add-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="c4add-104">Dans ce didacticiel, vous apprendrez comment toointegrate Mimecast Personal Portal avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4add-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4add-105">Intégration de Mimecast Personal Portal à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c4add-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4add-106">Vous pouvez contrôler dans Azure AD qui a accès tooMimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="c4add-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="c4add-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMimecast Personal Portal (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4add-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c4add-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4add-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4add-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4add-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c4add-110">Prerequisites</span></span>

<span data-ttu-id="c4add-111">tooconfigure intégration d’Azure AD avec Mimecast Personal Portal, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c4add-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="c4add-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4add-113">Un abonnement Mimecast Personal Portal pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c4add-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4add-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c4add-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4add-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c4add-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4add-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c4add-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4add-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4add-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4add-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c4add-118">Scenario description</span></span>
<span data-ttu-id="c4add-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c4add-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4add-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c4add-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4add-121">Ajout de Mimecast Personal Portal à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c4add-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="c4add-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="c4add-123">Ajout de Mimecast Personal Portal à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c4add-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="c4add-124">intégration de hello tooconfigure de Mimecast Personal Portal dans Azure AD, vous devez tooadd Mimecast Personal Portal à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c4add-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4add-125">**tooadd Mimecast Personal Portal à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4add-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4add-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c4add-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4add-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c4add-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4add-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c4add-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c4add-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c4add-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c4add-133">Dans la zone de recherche de hello, tapez **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="c4add-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="c4add-135">Dans le volet de résultats hello, sélectionnez **Mimecast Personal Portal**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c4add-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4add-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4add-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mimecast Personal Portal sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c4add-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4add-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mimecast Personal Portal est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4add-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="c4add-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Mimecast Personal Portal doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c4add-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="c4add-141">Dans Mimecast Personal Portal, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c4add-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4add-142">tooconfigure et test Azure AD l’authentification unique avec Mimecast Personal Portal, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c4add-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4add-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c4add-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4add-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4add-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4add-145">**[Création d’un utilisateur de test de Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)**  -toohave un équivalent de Britta Simon dans Mimecast Personal Portal est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c4add-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4add-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c4add-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4add-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c4add-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4add-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4add-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="c4add-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="c4add-150">**tooconfigure Azure AD l’authentification unique avec Mimecast Personal Portal, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4add-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4add-151">Bonjour portail Azure, sur hello **Mimecast Personal Portal** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c4add-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c4add-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c4add-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="c4add-155">Sur hello **Mimecast Personal Portal domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4add-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="c4add-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4add-157">a.</span></span> <span data-ttu-id="c4add-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="c4add-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="c4add-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4add-159">b.</span></span> <span data-ttu-id="c4add-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="c4add-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="c4add-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c4add-161">These values are not real.</span></span> <span data-ttu-id="c4add-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="c4add-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4add-163">Contact [équipe de support technique de Mimecast Personal Portal Client](https://www.mimecast.com/customer-success/technical-support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c4add-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="c4add-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c4add-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="c4add-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c4add-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4add-168">Sur hello **Mimecast Personal Portal Configuration** , cliquez sur **configurer Mimecast Personal Portal** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c4add-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4add-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c4add-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="c4add-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mimecast Personal Portal en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c4add-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="c4add-172">Accédez trop**Services \> Applications**.</span><span class="sxs-lookup"><span data-stu-id="c4add-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="c4add-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="c4add-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="c4add-174">Cliquez sur **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="c4add-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="c4add-175">![Profils d’authentification](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Profils d’authentification")</span><span class="sxs-lookup"><span data-stu-id="c4add-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="c4add-176">Cliquez sur **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="c4add-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="c4add-177">![Nouveau profil d’authentification](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "Nouveau profil d’authentification")</span><span class="sxs-lookup"><span data-stu-id="c4add-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="c4add-178">Bonjour **profil d’authentification** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4add-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c4add-179">![Profil d’authentification](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Profil d’authentification")</span><span class="sxs-lookup"><span data-stu-id="c4add-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="c4add-180">a.</span><span class="sxs-lookup"><span data-stu-id="c4add-180">a.</span></span> <span data-ttu-id="c4add-181">Bonjour **Description** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="c4add-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="c4add-182">b.</span><span class="sxs-lookup"><span data-stu-id="c4add-182">b.</span></span> <span data-ttu-id="c4add-183">Sélectionnez **Enforce SAML Authentication for Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="c4add-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="c4add-184">c.</span><span class="sxs-lookup"><span data-stu-id="c4add-184">c.</span></span> <span data-ttu-id="c4add-185">Pour **Provider**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4add-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="c4add-186">d.</span><span class="sxs-lookup"><span data-stu-id="c4add-186">d.</span></span> <span data-ttu-id="c4add-187">Dans **URL de l’émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4add-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c4add-188">e.</span><span class="sxs-lookup"><span data-stu-id="c4add-188">e.</span></span> <span data-ttu-id="c4add-189">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4add-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c4add-190">f.</span><span class="sxs-lookup"><span data-stu-id="c4add-190">f.</span></span> <span data-ttu-id="c4add-191">Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4add-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c4add-192">g.</span><span class="sxs-lookup"><span data-stu-id="c4add-192">g.</span></span> <span data-ttu-id="c4add-193">Ouvrez votre **base-64** certificat dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de fournisseur d’identité (métadonnées)** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c4add-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="c4add-194">h.</span><span class="sxs-lookup"><span data-stu-id="c4add-194">h.</span></span> <span data-ttu-id="c4add-195">Sélectionnez **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="c4add-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="c4add-196">i.</span><span class="sxs-lookup"><span data-stu-id="c4add-196">i.</span></span> <span data-ttu-id="c4add-197">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c4add-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c4add-198">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c4add-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4add-199">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c4add-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4add-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4add-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4add-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4add-202">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c4add-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c4add-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4add-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4add-205">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c4add-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4add-207">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c4add-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4add-209">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c4add-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4add-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4add-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4add-213">a.</span><span class="sxs-lookup"><span data-stu-id="c4add-213">a.</span></span> <span data-ttu-id="c4add-214">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4add-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4add-215">b.</span><span class="sxs-lookup"><span data-stu-id="c4add-215">b.</span></span> <span data-ttu-id="c4add-216">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4add-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4add-217">c.</span><span class="sxs-lookup"><span data-stu-id="c4add-217">c.</span></span> <span data-ttu-id="c4add-218">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c4add-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4add-219">d.</span><span class="sxs-lookup"><span data-stu-id="c4add-219">d.</span></span> <span data-ttu-id="c4add-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4add-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="c4add-221">Création d’un utilisateur de test Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="c4add-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="c4add-222">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Mimecast Personal Portal, vous devez les configurer dans Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="c4add-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="c4add-223">Dans les cas de hello de Mimecast Personal Portal, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c4add-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="c4add-224">Vous devez tooregister un domaine avant de pouvoir créer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c4add-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="c4add-225">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4add-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4add-226">Ouverture de session tooyour **Mimecast Personal Portal** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c4add-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="c4add-227">Accédez trop**répertoires \> interne**.</span><span class="sxs-lookup"><span data-stu-id="c4add-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="c4add-228">![Répertoires](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Répertoires")</span><span class="sxs-lookup"><span data-stu-id="c4add-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="c4add-229">Cliquez sur **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="c4add-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="c4add-230">![Enregistrer un nouveau domaine](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Enregistrer un nouveau domaine")</span><span class="sxs-lookup"><span data-stu-id="c4add-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="c4add-231">Après avoir créé votre domaine, cliquez sur **New Address**.</span><span class="sxs-lookup"><span data-stu-id="c4add-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="c4add-232">![Nouvelle adresse](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Nouvelle adresse")</span><span class="sxs-lookup"><span data-stu-id="c4add-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="c4add-233">Dans hello adresse boîte de dialogue Nouveau, effectuez hello suivant les étapes d’un Azure valide compte AD tooprovision :</span><span class="sxs-lookup"><span data-stu-id="c4add-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="c4add-234">![Enregistrer](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "enregistrer")</span><span class="sxs-lookup"><span data-stu-id="c4add-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="c4add-235">a.</span><span class="sxs-lookup"><span data-stu-id="c4add-235">a.</span></span> <span data-ttu-id="c4add-236">Bonjour **adresse de messagerie** zone de texte, type **adresse de messagerie** d’utilisateur hello en tant que  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c4add-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="c4add-237">b.</span><span class="sxs-lookup"><span data-stu-id="c4add-237">b.</span></span> <span data-ttu-id="c4add-238">Bonjour **nom Global** hello de type zone de texte **nom d’utilisateur** en tant que **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4add-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="c4add-239">c.</span><span class="sxs-lookup"><span data-stu-id="c4add-239">c.</span></span> <span data-ttu-id="c4add-240">Bonjour **mot de passe**, et **confirmer le mot de passe** zones de texte, hello de type **mot de passe** d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="c4add-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="c4add-241">b.</span><span class="sxs-lookup"><span data-stu-id="c4add-241">b.</span></span> <span data-ttu-id="c4add-242">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c4add-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c4add-243">Vous pouvez utiliser tout autre outil de création de compte utilisateur Mimecast Personal Portal ou API fournie par les comptes d’utilisateur Mimecast Personal Portal tooprovision Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4add-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4add-244">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4add-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4add-245">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="c4add-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c4add-247">**tooassign Britta Simon tooMimecast Personal Portal, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4add-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4add-248">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c4add-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c4add-250">Dans la liste des applications hello, sélectionnez **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="c4add-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="c4add-252">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c4add-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c4add-254">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c4add-254">Click **Add** button.</span></span> <span data-ttu-id="c4add-255">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c4add-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c4add-257">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c4add-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4add-258">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c4add-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4add-259">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c4add-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4add-260">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c4add-260">Testing single sign-on</span></span>
<span data-ttu-id="c4add-261">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c4add-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4add-262">Lorsque vous cliquez sur mosaïque de Mimecast Personal Portal hello Bonjour volet d’accès, vous devez obtenir l’application de Mimecast Personal Portal tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="c4add-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="c4add-263">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4add-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4add-264">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c4add-264">Additional resources</span></span>

* [<span data-ttu-id="c4add-265">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4add-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4add-266">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c4add-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

