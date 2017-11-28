---
title: "Didacticiel : Intégration d’Azure Active Directory à Zscaler Beta | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zscaler Beta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="86a64-103">Didacticiel : Intégration d’Active Directory à Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="86a64-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="86a64-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zscaler Beta avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86a64-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86a64-105">Intégration de Zscaler Beta à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="86a64-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86a64-106">Vous pouvez contrôler dans Azure AD qui a accès tooZscaler bêta</span><span class="sxs-lookup"><span data-stu-id="86a64-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="86a64-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZscaler bêta (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86a64-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="86a64-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86a64-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86a64-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a64-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="86a64-110">Prerequisites</span></span>

<span data-ttu-id="86a64-111">tooconfigure intégration d’Azure AD à Zscaler Beta, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="86a64-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="86a64-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86a64-113">Un abonnement Zscaler Beta pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="86a64-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86a64-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="86a64-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86a64-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="86a64-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86a64-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="86a64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86a64-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86a64-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86a64-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="86a64-118">Scenario description</span></span>
<span data-ttu-id="86a64-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="86a64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86a64-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="86a64-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86a64-121">Ajout de Zscaler Beta à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="86a64-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="86a64-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="86a64-123">Ajout de Zscaler Beta à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="86a64-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="86a64-124">intégration de hello tooconfigure de Zscaler Beta dans Azure AD, vous devez tooadd Zscaler Beta à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="86a64-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86a64-125">**tooadd Zscaler Beta à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86a64-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a64-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="86a64-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86a64-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="86a64-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86a64-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="86a64-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="86a64-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86a64-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="86a64-133">Dans la zone de recherche de hello, tapez **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="86a64-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="86a64-135">Dans le volet de résultats hello, sélectionnez **Zscaler Beta**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="86a64-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86a64-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86a64-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler Beta grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="86a64-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86a64-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zscaler Beta est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a64-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="86a64-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zscaler Beta doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="86a64-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="86a64-141">Dans Zscaler Beta, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="86a64-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="86a64-142">tooconfigure et test Azure AD l’authentification unique sur Zscaler Beta, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="86a64-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86a64-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="86a64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86a64-144">**[Configuration des paramètres proxy](#configuring-proxy-settings)**  -paramètres de proxy tooconfigure hello dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="86a64-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="86a64-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a64-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="86a64-146">**[Création d’un utilisateur de test de Zscaler Beta](#creating-a-zscaler-beta-test-user)**  -toohave un équivalent de Britta Simon dans Zscaler Beta qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86a64-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="86a64-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="86a64-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="86a64-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="86a64-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86a64-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86a64-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="86a64-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="86a64-151">**tooconfigure Azure AD l’authentification unique sur Zscaler Beta, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86a64-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a64-152">Bonjour portail Azure, sur hello **Zscaler Beta** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="86a64-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="86a64-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="86a64-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="86a64-156">Sur hello **Zscaler Beta domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="86a64-158">Zone de texte URL hello Sign-on, tapez hello l’URL utilisée par vos utilisateurs sur toosign tooyour application Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="86a64-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86a64-159">Vous avez tooupdate cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="86a64-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="86a64-160">Contact [équipe de support technique Zscaler Beta Client](https://www.zscaler.com/company/contact) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="86a64-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="86a64-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="86a64-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="86a64-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="86a64-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86a64-165">Sur hello **Zscaler Beta Configuration** , cliquez sur **configurer Zscaler Beta** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="86a64-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="86a64-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="86a64-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="86a64-168">Dans une fenêtre de navigateur web, connectez-vous tooyour site de société Zscaler Beta en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="86a64-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="86a64-169">Dans le menu hello haut de hello, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="86a64-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="86a64-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="86a64-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="86a64-171">Sous **Manage Administrators & Roles**, cliquez sur **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="86a64-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="86a64-172">![Gérer les utilisateurs et l’authentification](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Gérer les utilisateurs et l’authentification")</span><span class="sxs-lookup"><span data-stu-id="86a64-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="86a64-173">Bonjour **choisir les Options d’authentification pour votre organisation** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="86a64-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="86a64-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="86a64-175">a.</span><span class="sxs-lookup"><span data-stu-id="86a64-175">a.</span></span> <span data-ttu-id="86a64-176">Sélectionnez **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="86a64-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="86a64-177">b.</span><span class="sxs-lookup"><span data-stu-id="86a64-177">b.</span></span> <span data-ttu-id="86a64-178">Cliquez sur **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="86a64-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="86a64-179">Sur hello **Configure SAML Single Sign-On Parameters** page de boîte de dialogue, effectuer hello comme suit, puis cliquez sur **terminé**</span><span class="sxs-lookup"><span data-stu-id="86a64-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="86a64-180">![Authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="86a64-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="86a64-181">a.</span><span class="sxs-lookup"><span data-stu-id="86a64-181">a.</span></span> <span data-ttu-id="86a64-182">Hello de coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **URL d’utilisateurs de toowhich hello portail SAML sont envoyés pour l’authentification** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="86a64-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="86a64-183">b.</span><span class="sxs-lookup"><span data-stu-id="86a64-183">b.</span></span> <span data-ttu-id="86a64-184">Bonjour **attribut contenant le nom de connexion** zone de texte, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="86a64-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="86a64-185">c.</span><span class="sxs-lookup"><span data-stu-id="86a64-185">c.</span></span> <span data-ttu-id="86a64-186">tooupload votre certificat téléchargé, cliquez sur **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="86a64-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="86a64-187">d.</span><span class="sxs-lookup"><span data-stu-id="86a64-187">d.</span></span> <span data-ttu-id="86a64-188">Sélectionnez **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="86a64-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="86a64-189">Sur hello **configurer l’authentification utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="86a64-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="86a64-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="86a64-191">a.</span><span class="sxs-lookup"><span data-stu-id="86a64-191">a.</span></span> <span data-ttu-id="86a64-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="86a64-192">Click **Save**.</span></span>

    <span data-ttu-id="86a64-193">b.</span><span class="sxs-lookup"><span data-stu-id="86a64-193">b.</span></span> <span data-ttu-id="86a64-194">Cliquez sur **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="86a64-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="86a64-195">Configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="86a64-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="86a64-196">paramètres de proxy tooconfigure hello dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="86a64-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="86a64-197">Démarrez **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="86a64-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="86a64-198">Sélectionnez **options Internet** de hello **outils** menu Ouvrir hello **Options Internet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86a64-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="86a64-199">![Options Internet](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Options Internet")</span><span class="sxs-lookup"><span data-stu-id="86a64-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="86a64-200">Cliquez sur hello **connexions** onglet.</span><span class="sxs-lookup"><span data-stu-id="86a64-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="86a64-201">![Connexions](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connexions")</span><span class="sxs-lookup"><span data-stu-id="86a64-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="86a64-202">Cliquez sur **paramètres LAN** tooopen hello **paramètres LAN** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86a64-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="86a64-203">Dans la section serveur Proxy de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="86a64-204">![Serveur proxy](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Serveur proxy")</span><span class="sxs-lookup"><span data-stu-id="86a64-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="86a64-205">a.</span><span class="sxs-lookup"><span data-stu-id="86a64-205">a.</span></span> <span data-ttu-id="86a64-206">Sélectionnez **Utiliser un serveur proxy pour le réseau local**.</span><span class="sxs-lookup"><span data-stu-id="86a64-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="86a64-207">b.</span><span class="sxs-lookup"><span data-stu-id="86a64-207">b.</span></span> <span data-ttu-id="86a64-208">Dans la zone de texte adresse hello, tapez **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="86a64-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="86a64-209">c.</span><span class="sxs-lookup"><span data-stu-id="86a64-209">c.</span></span> <span data-ttu-id="86a64-210">Dans la zone de texte Port hello, tapez **80**.</span><span class="sxs-lookup"><span data-stu-id="86a64-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="86a64-211">d.</span><span class="sxs-lookup"><span data-stu-id="86a64-211">d.</span></span> <span data-ttu-id="86a64-212">Sélectionnez **Ne pas utiliser de serveur proxy pour les adresses locales**.</span><span class="sxs-lookup"><span data-stu-id="86a64-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="86a64-213">e.</span><span class="sxs-lookup"><span data-stu-id="86a64-213">e.</span></span> <span data-ttu-id="86a64-214">Cliquez sur **OK** tooclose hello **les paramètres de réseau local (LAN)** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86a64-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="86a64-215">Cliquez sur **OK** tooclose hello **Options Internet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86a64-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="86a64-216">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="86a64-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86a64-217">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="86a64-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86a64-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86a64-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86a64-219">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="86a64-220">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="86a64-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="86a64-222">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86a64-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a64-223">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="86a64-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86a64-225">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="86a64-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86a64-227">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="86a64-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86a64-229">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86a64-231">a.</span><span class="sxs-lookup"><span data-stu-id="86a64-231">a.</span></span> <span data-ttu-id="86a64-232">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86a64-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86a64-233">b.</span><span class="sxs-lookup"><span data-stu-id="86a64-233">b.</span></span> <span data-ttu-id="86a64-234">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86a64-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86a64-235">c.</span><span class="sxs-lookup"><span data-stu-id="86a64-235">c.</span></span> <span data-ttu-id="86a64-236">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="86a64-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86a64-237">d.</span><span class="sxs-lookup"><span data-stu-id="86a64-237">d.</span></span> <span data-ttu-id="86a64-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="86a64-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="86a64-239">Création d’un utilisateur de test Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="86a64-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="86a64-240">tooenable Azure AD les utilisateurs toolog tooZscaler bêta, elles doivent être mis en service tooZscaler bêta.</span><span class="sxs-lookup"><span data-stu-id="86a64-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="86a64-241">Dans les cas de hello de Zscaler Beta, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="86a64-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="86a64-242">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="86a64-243">Connectez-vous à tooyour **Zscaler Beta** client.</span><span class="sxs-lookup"><span data-stu-id="86a64-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="86a64-244">Cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="86a64-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="86a64-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="86a64-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="86a64-246">Cliquez sur **User Management**.</span><span class="sxs-lookup"><span data-stu-id="86a64-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="86a64-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span><span class="sxs-lookup"><span data-stu-id="86a64-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="86a64-248">Bonjour **utilisateurs** , cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="86a64-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="86a64-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="86a64-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="86a64-250">Dans la section Ajouter un utilisateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86a64-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="86a64-251">![Ajouter un utilisateur](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="86a64-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="86a64-252">a.</span><span class="sxs-lookup"><span data-stu-id="86a64-252">a.</span></span> <span data-ttu-id="86a64-253">Hello de type **UserID**, **nom d’utilisateur complet**, **mot de passe**, **confirmer le mot de passe**, puis sélectionnez **groupes**et hello **service** d’un Azure valide compte AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="86a64-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="86a64-254">b.</span><span class="sxs-lookup"><span data-stu-id="86a64-254">b.</span></span> <span data-ttu-id="86a64-255">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="86a64-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="86a64-256">Vous pouvez utiliser n’importe quel autre Zscaler Beta utilisateur compte outil de création ou API fournie par Zscaler Beta tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a64-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86a64-257">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a64-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86a64-258">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZscaler bêta.</span><span class="sxs-lookup"><span data-stu-id="86a64-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="86a64-260">**tooassign Britta Simon tooZscaler bêta, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86a64-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a64-261">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="86a64-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="86a64-263">Dans la liste des applications hello, sélectionnez **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="86a64-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="86a64-265">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="86a64-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="86a64-267">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="86a64-267">Click **Add** button.</span></span> <span data-ttu-id="86a64-268">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="86a64-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="86a64-270">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="86a64-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86a64-271">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="86a64-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86a64-272">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="86a64-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86a64-273">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="86a64-273">Testing single sign-on</span></span>

<span data-ttu-id="86a64-274">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="86a64-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="86a64-275">Lorsque vous cliquez sur hello Zscaler Beta vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="86a64-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="86a64-276">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86a64-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86a64-277">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="86a64-277">Additional resources</span></span>

* [<span data-ttu-id="86a64-278">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86a64-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86a64-279">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="86a64-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

