---
title: "Didacticiel : Intégration d’Azure Active Directory à Adaptative Suite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de la Suite adaptative."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="d9d16-103">Didacticiel : Intégration d’Azure Active Directory à Adaptative Suite</span><span class="sxs-lookup"><span data-stu-id="d9d16-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="d9d16-104">Dans ce didacticiel, vous apprendrez comment toointegrate Suite adaptative avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9d16-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9d16-105">Intégration Suite adaptative à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d9d16-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9d16-106">Vous pouvez contrôler dans Azure AD qui a accès tooAdaptive Suite</span><span class="sxs-lookup"><span data-stu-id="d9d16-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="d9d16-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAdaptive Suite (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9d16-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9d16-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9d16-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9d16-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9d16-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9d16-110">Prerequisites</span></span>

<span data-ttu-id="d9d16-111">tooconfigure intégration d’Azure AD avec Suite adaptative, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d9d16-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="d9d16-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9d16-113">Un abonnement Adaptive Suite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d9d16-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9d16-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d9d16-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9d16-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d9d16-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9d16-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d9d16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9d16-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9d16-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9d16-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d9d16-118">Scenario description</span></span>
<span data-ttu-id="d9d16-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d9d16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9d16-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d9d16-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9d16-121">Ajout de Suite adaptative à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d9d16-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="d9d16-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="d9d16-123">Ajout de Suite adaptative à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d9d16-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="d9d16-124">intégration de hello tooconfigure de Suite adaptative dans Azure AD, vous devez tooadd Suite adaptative à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d9d16-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9d16-125">**tooadd Suite adaptative à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9d16-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d16-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d9d16-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9d16-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9d16-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d9d16-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d9d16-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d9d16-133">Dans la zone de recherche de hello, tapez **Suite adaptative**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="d9d16-135">Dans le volet de résultats hello, sélectionnez **Suite adaptative**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d9d16-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9d16-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9d16-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Adaptive Suite, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d9d16-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9d16-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Suite adaptative est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9d16-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="d9d16-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la Suite adaptative hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d9d16-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="d9d16-141">Dans la Suite adaptative, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="d9d16-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d9d16-142">tooconfigure et test Azure AD l’authentification unique avec Suite adaptative, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d9d16-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9d16-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d9d16-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9d16-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9d16-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9d16-145">**[Création d’un utilisateur de test Suite adaptative](#creating-an-adaptive-suite-test-user)**  -toohave un équivalent de Britta Simon dans Suite adaptative qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9d16-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9d16-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d9d16-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9d16-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d9d16-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9d16-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9d16-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Suite adaptative.</span><span class="sxs-lookup"><span data-stu-id="d9d16-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="d9d16-150">**tooconfigure Azure AD single sign-on avec Suite adaptative, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9d16-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d16-151">Bonjour portail Azure, sur hello **Suite adaptative** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d9d16-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d9d16-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="d9d16-155">Sur hello **adaptative Suite de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9d16-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="d9d16-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="d9d16-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="d9d16-158">Vous pouvez obtenir cette valeur à partir de hello Suite adaptative **SAML SSO Settings** page.</span><span class="sxs-lookup"><span data-stu-id="d9d16-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="d9d16-159">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d9d16-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="d9d16-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d9d16-161">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9d16-163">Sur hello **Configuration de la Suite adaptative** , cliquez sur **configurer la Suite adaptative** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d9d16-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d9d16-164">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d9d16-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="d9d16-166">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour Suite adaptative en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d9d16-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="d9d16-167">Accédez trop**Admin**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="d9d16-168">![Administrateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="d9d16-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="d9d16-169">Bonjour **utilisateurs et rôles** , cliquez sur **gérer les paramètres de l’authentification unique SAML**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="d9d16-170">![Gérer les paramètres d’authentification unique de SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gérer les paramètres d’authentification unique de SAML")</span><span class="sxs-lookup"><span data-stu-id="d9d16-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="d9d16-171">Sur hello **SAML SSO Settings** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9d16-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d9d16-172">![Paramètres d’authentification unique de SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Paramètres d’authentification unique de SAML")</span><span class="sxs-lookup"><span data-stu-id="d9d16-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="d9d16-173">a.</span><span class="sxs-lookup"><span data-stu-id="d9d16-173">a.</span></span> <span data-ttu-id="d9d16-174">Bonjour **nom de fournisseur d’identité** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="d9d16-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="d9d16-175">b.</span><span class="sxs-lookup"><span data-stu-id="d9d16-175">b.</span></span> <span data-ttu-id="d9d16-176">Hello de coller **ID d’entité SAML** valeur copiée à partir du portail Azure dans hello **fournisseur d’identité de l’entité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d9d16-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="d9d16-177">c.</span><span class="sxs-lookup"><span data-stu-id="d9d16-177">c.</span></span> <span data-ttu-id="d9d16-178">Hello de coller **SAML Sign-On URL du Service unique** valeur copiée à partir du portail Azure dans hello **fournisseur d’identité URL SSO** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d9d16-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="d9d16-179">d.</span><span class="sxs-lookup"><span data-stu-id="d9d16-179">d.</span></span> <span data-ttu-id="d9d16-180">Hello de coller **SAML Sign-On URL du Service unique** valeur copiée à partir du portail Azure dans hello **URL de déconnexion personnalisé** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d9d16-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="d9d16-181">e.</span><span class="sxs-lookup"><span data-stu-id="d9d16-181">e.</span></span> <span data-ttu-id="d9d16-182">tooupload votre certificat téléchargé, cliquez sur **choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="d9d16-183">f.</span><span class="sxs-lookup"><span data-stu-id="d9d16-183">f.</span></span> <span data-ttu-id="d9d16-184">Sélectionnez hello qui suit, pour :</span><span class="sxs-lookup"><span data-stu-id="d9d16-184">Select hello following, for:</span></span>
    * <span data-ttu-id="d9d16-185">Pour **SAML user id**, sélectionnez **User’s Adaptive Insights user name**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="d9d16-186">Pour **SAML user id location**, sélectionnez **User id in NameID of Subject**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="d9d16-187">Pour **SAML NameID format**, sélectionnez **Email address**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="d9d16-188">Pour **Enable SAML**, sélectionnez **Allow SAML SSO and direct Adaptive Insights login**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="d9d16-189">g.</span><span class="sxs-lookup"><span data-stu-id="d9d16-189">g.</span></span> <span data-ttu-id="d9d16-190">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d9d16-191">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d9d16-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9d16-192">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d9d16-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9d16-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9d16-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9d16-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9d16-195">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d9d16-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d9d16-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9d16-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d16-198">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d9d16-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9d16-200">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9d16-202">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d9d16-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9d16-204">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9d16-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9d16-206">a.</span><span class="sxs-lookup"><span data-stu-id="d9d16-206">a.</span></span> <span data-ttu-id="d9d16-207">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9d16-208">b.</span><span class="sxs-lookup"><span data-stu-id="d9d16-208">b.</span></span> <span data-ttu-id="d9d16-209">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9d16-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9d16-210">c.</span><span class="sxs-lookup"><span data-stu-id="d9d16-210">c.</span></span> <span data-ttu-id="d9d16-211">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9d16-212">d.</span><span class="sxs-lookup"><span data-stu-id="d9d16-212">d.</span></span> <span data-ttu-id="d9d16-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="d9d16-214">Création d’un utilisateur de test Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="d9d16-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="d9d16-215">tooenable Azure AD les utilisateurs toolog dans tooAdaptive Suite, vous devez les configurer dans Suite adaptative.</span><span class="sxs-lookup"><span data-stu-id="d9d16-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="d9d16-216">Dans les cas de hello de Suite adaptative, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="d9d16-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="d9d16-217">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9d16-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="d9d16-218">Connectez-vous à tooyour **Suite adaptative** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d9d16-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="d9d16-219">Accédez trop**Admin**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="d9d16-220">![Administrateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="d9d16-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="d9d16-221">Bonjour **utilisateurs et rôles** , cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="d9d16-222">![Ajouter un utilisateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="d9d16-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="d9d16-223">Bonjour **nouvel utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9d16-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d9d16-224">![Envoyer](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Envoyer")</span><span class="sxs-lookup"><span data-stu-id="d9d16-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="d9d16-225">a.</span><span class="sxs-lookup"><span data-stu-id="d9d16-225">a.</span></span> <span data-ttu-id="d9d16-226">Hello de type **nom**, **connexion**, **messagerie**, **mot de passe** d’un utilisateur Azure Active Directory valide que vous souhaitez tooprovision dans hello liée zones de texte.</span><span class="sxs-lookup"><span data-stu-id="d9d16-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="d9d16-227">b.</span><span class="sxs-lookup"><span data-stu-id="d9d16-227">b.</span></span> <span data-ttu-id="d9d16-228">Sélectionnez un **rôle**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="d9d16-229">c.</span><span class="sxs-lookup"><span data-stu-id="d9d16-229">c.</span></span> <span data-ttu-id="d9d16-230">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="d9d16-231">Vous pouvez utiliser n’importe quel autre Suite adaptative utilisateur compte outil de création ou API fournie par la Suite adaptative tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="d9d16-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9d16-232">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d16-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9d16-233">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="d9d16-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d9d16-235">**tooassign Britta Simon tooAdaptive Suite, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9d16-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9d16-236">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d9d16-238">Dans la liste des applications hello, sélectionnez **Suite adaptative**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="d9d16-240">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d9d16-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-242">Click **Add** button.</span></span> <span data-ttu-id="d9d16-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d9d16-245">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d9d16-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9d16-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9d16-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d9d16-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9d16-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d9d16-248">Testing single sign-on</span></span>

<span data-ttu-id="d9d16-249">objectif Hello de cette section est tootest votre Microsoft Azure AD Single Sign-On configuration à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d9d16-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9d16-250">Lorsque vous cliquez sur mosaïque Suite adaptative hello hello volet d’accès, vous devez obtenir l’application de Suite adaptative tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="d9d16-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d9d16-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d9d16-251">Additional resources</span></span>

* [<span data-ttu-id="d9d16-252">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9d16-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9d16-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d9d16-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

