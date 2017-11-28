---
title: "Didacticiel : Intégration d’Azure Active Directory à Zscaler Two | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zscaler Two."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: dcd13d399f093f24a945f234401cd5b7e527ed34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="66d94-103">Didacticiel : Intégration d’Azure Active Directory à Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="66d94-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="66d94-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zscaler Two avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66d94-104">In this tutorial, you learn how toointegrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66d94-105">Intégration de Zscaler Two à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="66d94-105">Integrating Zscaler Two with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66d94-106">Vous pouvez contrôler dans Azure AD qui a tooZscaler accès deux</span><span class="sxs-lookup"><span data-stu-id="66d94-106">You can control in Azure AD who has access tooZscaler Two</span></span>
- <span data-ttu-id="66d94-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZscaler deux (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-107">You can enable your users tooautomatically get signed-on tooZscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66d94-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="66d94-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66d94-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66d94-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66d94-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="66d94-110">Prerequisites</span></span>

<span data-ttu-id="66d94-111">tooconfigure intégration d’Azure AD à Zscaler Two, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="66d94-111">tooconfigure Azure AD integration with Zscaler Two, you need hello following items:</span></span>

- <span data-ttu-id="66d94-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66d94-113">Un abonnement Zscaler Two pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="66d94-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66d94-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="66d94-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66d94-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="66d94-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66d94-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="66d94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66d94-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66d94-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66d94-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="66d94-118">Scenario description</span></span>
<span data-ttu-id="66d94-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="66d94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66d94-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="66d94-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66d94-121">Ajout de Zscaler Two à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="66d94-121">Adding Zscaler Two from hello gallery</span></span>
2. <span data-ttu-id="66d94-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-hello-gallery"></a><span data-ttu-id="66d94-123">Ajout de Zscaler Two à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="66d94-123">Adding Zscaler Two from hello gallery</span></span>
<span data-ttu-id="66d94-124">intégration de hello tooconfigure de Zscaler Two dans Azure AD, vous devez tooadd Zscaler Two à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="66d94-124">tooconfigure hello integration of Zscaler Two into Azure AD, you need tooadd Zscaler Two from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66d94-125">**tooadd Zscaler Two à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="66d94-125">**tooadd Zscaler Two from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66d94-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="66d94-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66d94-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="66d94-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66d94-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="66d94-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="66d94-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="66d94-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="66d94-133">Dans la zone de recherche de hello, tapez **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="66d94-133">In hello search box, type **Zscaler Two**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. <span data-ttu-id="66d94-135">Dans le volet de résultats hello, sélectionnez **Zscaler Two**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="66d94-135">In hello results panel, select **Zscaler Two**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66d94-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66d94-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler Two grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="66d94-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66d94-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zscaler Two est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66d94-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Two is tooa user in Azure AD.</span></span> <span data-ttu-id="66d94-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zscaler Two doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="66d94-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Two needs toobe established.</span></span>

<span data-ttu-id="66d94-141">Dans Zscaler Two, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="66d94-141">In Zscaler Two, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66d94-142">tooconfigure et test Azure AD l’authentification unique avec Zscaler Two, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="66d94-142">tooconfigure and test Azure AD single sign-on with Zscaler Two, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66d94-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="66d94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66d94-144">**[Configuration des paramètres proxy](#configuring-proxy-settings)**  -paramètres de proxy tooconfigure hello dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="66d94-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="66d94-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66d94-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="66d94-146">**[Création d’un utilisateur test Zscaler Two](#creating-a-zscaler-two-test-user)**  -toohave un équivalent de Britta Simon dans Zscaler Two qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="66d94-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - toohave a counterpart of Britta Simon in Zscaler Two that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="66d94-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="66d94-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="66d94-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="66d94-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66d94-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66d94-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="66d94-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="66d94-151">**tooconfigure Azure AD single sign-on avec Zscaler Two, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="66d94-151">**tooconfigure Azure AD single sign-on with Zscaler Two, perform hello following steps:**</span></span>

1. <span data-ttu-id="66d94-152">Bonjour portail Azure, sur hello **Zscaler Two** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="66d94-152">In hello Azure portal, on hello **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="66d94-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="66d94-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. <span data-ttu-id="66d94-156">Sur hello **Zscaler deux domaines et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-156">On hello **Zscaler Two Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="66d94-158">Dans la zone de texte URL de connexion hello, tapez Bonjour l’URL utilisée par vos utilisateurs sur toosign tooyour application ZScaler Two.</span><span class="sxs-lookup"><span data-stu-id="66d94-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66d94-159">Vous avez tooupdate cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="66d94-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="66d94-160">Contact [équipe de support technique Zscaler deux clients](https://www.zscaler.com/company/contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="66d94-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="66d94-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="66d94-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. <span data-ttu-id="66d94-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="66d94-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66d94-165">Sur hello **Configuration à deux Zscaler** , cliquez sur **configurer Zscaler Two** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="66d94-165">On hello **Zscaler Two Configuration** section, click **Configure Zscaler Two** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="66d94-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="66d94-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. <span data-ttu-id="66d94-168">Dans une fenêtre de navigateur web, ouvrez une session dans le site de société ZScaler Two tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="66d94-168">In a different web browser window, log in tooyour ZScaler Two company site as an administrator.</span></span>

8. <span data-ttu-id="66d94-169">Dans le menu hello haut de hello, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="66d94-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="66d94-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="66d94-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="66d94-171">Sous **Manage Administrators & Roles**, cliquez sur **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="66d94-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="66d94-172">![Gérer les utilisateurs et l’authentification](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Gérer les utilisateurs et l’authentification")</span><span class="sxs-lookup"><span data-stu-id="66d94-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="66d94-173">Bonjour **choisir les Options d’authentification pour votre organisation** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="66d94-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="66d94-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="66d94-175">a.</span><span class="sxs-lookup"><span data-stu-id="66d94-175">a.</span></span> <span data-ttu-id="66d94-176">Sélectionnez **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="66d94-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="66d94-177">b.</span><span class="sxs-lookup"><span data-stu-id="66d94-177">b.</span></span> <span data-ttu-id="66d94-178">Cliquez sur **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="66d94-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="66d94-179">Sur hello **Configure SAML Single Sign-On Parameters** page de boîte de dialogue, effectuer hello comme suit, puis cliquez sur **terminé**</span><span class="sxs-lookup"><span data-stu-id="66d94-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="66d94-180">![Authentification unique](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="66d94-180">![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="66d94-181">a.</span><span class="sxs-lookup"><span data-stu-id="66d94-181">a.</span></span> <span data-ttu-id="66d94-182">Hello de coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **URL d’utilisateurs de toowhich hello portail SAML sont envoyés pour l’authentification** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="66d94-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="66d94-183">b.</span><span class="sxs-lookup"><span data-stu-id="66d94-183">b.</span></span> <span data-ttu-id="66d94-184">Bonjour **attribut contenant le nom de connexion** zone de texte, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="66d94-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="66d94-185">c.</span><span class="sxs-lookup"><span data-stu-id="66d94-185">c.</span></span> <span data-ttu-id="66d94-186">tooupload votre certificat téléchargé, cliquez sur **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="66d94-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="66d94-187">d.</span><span class="sxs-lookup"><span data-stu-id="66d94-187">d.</span></span> <span data-ttu-id="66d94-188">Sélectionnez **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="66d94-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="66d94-189">Sur hello **configurer l’authentification utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="66d94-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="66d94-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="66d94-191">a.</span><span class="sxs-lookup"><span data-stu-id="66d94-191">a.</span></span> <span data-ttu-id="66d94-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="66d94-192">Click **Save**.</span></span>

    <span data-ttu-id="66d94-193">b.</span><span class="sxs-lookup"><span data-stu-id="66d94-193">b.</span></span> <span data-ttu-id="66d94-194">Cliquez sur **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="66d94-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="66d94-195">Configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="66d94-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="66d94-196">paramètres de proxy tooconfigure hello dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="66d94-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="66d94-197">Démarrez **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="66d94-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="66d94-198">Sélectionnez **options Internet** de hello **outils** menu Ouvrir hello **Options Internet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="66d94-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="66d94-199">![Options Internet](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Options Internet")</span><span class="sxs-lookup"><span data-stu-id="66d94-199">![Internet Options](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="66d94-200">Cliquez sur hello **connexions** onglet.</span><span class="sxs-lookup"><span data-stu-id="66d94-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="66d94-201">![Connexions](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connexions")</span><span class="sxs-lookup"><span data-stu-id="66d94-201">![Connections](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="66d94-202">Cliquez sur **paramètres LAN** tooopen hello **paramètres LAN** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="66d94-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="66d94-203">Dans la section serveur Proxy de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="66d94-204">![Serveur proxy](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Serveur proxy")</span><span class="sxs-lookup"><span data-stu-id="66d94-204">![Proxy server](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="66d94-205">a.</span><span class="sxs-lookup"><span data-stu-id="66d94-205">a.</span></span> <span data-ttu-id="66d94-206">Sélectionnez **Utiliser un serveur proxy pour le réseau local**.</span><span class="sxs-lookup"><span data-stu-id="66d94-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="66d94-207">b.</span><span class="sxs-lookup"><span data-stu-id="66d94-207">b.</span></span> <span data-ttu-id="66d94-208">Dans la zone de texte adresse hello, tapez **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="66d94-208">In hello Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="66d94-209">c.</span><span class="sxs-lookup"><span data-stu-id="66d94-209">c.</span></span> <span data-ttu-id="66d94-210">Dans la zone de texte Port hello, tapez **80**.</span><span class="sxs-lookup"><span data-stu-id="66d94-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="66d94-211">d.</span><span class="sxs-lookup"><span data-stu-id="66d94-211">d.</span></span> <span data-ttu-id="66d94-212">Sélectionnez **Ne pas utiliser de serveur proxy pour les adresses locales**.</span><span class="sxs-lookup"><span data-stu-id="66d94-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="66d94-213">e.</span><span class="sxs-lookup"><span data-stu-id="66d94-213">e.</span></span> <span data-ttu-id="66d94-214">Cliquez sur **OK** tooclose hello **les paramètres de réseau local (LAN)** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="66d94-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="66d94-215">Cliquez sur **OK** tooclose hello **Options Internet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="66d94-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="66d94-216">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="66d94-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66d94-217">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="66d94-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66d94-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66d94-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66d94-219">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="66d94-220">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="66d94-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="66d94-222">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="66d94-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66d94-223">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="66d94-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66d94-225">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="66d94-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66d94-227">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="66d94-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66d94-229">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66d94-231">a.</span><span class="sxs-lookup"><span data-stu-id="66d94-231">a.</span></span> <span data-ttu-id="66d94-232">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66d94-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66d94-233">b.</span><span class="sxs-lookup"><span data-stu-id="66d94-233">b.</span></span> <span data-ttu-id="66d94-234">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66d94-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66d94-235">c.</span><span class="sxs-lookup"><span data-stu-id="66d94-235">c.</span></span> <span data-ttu-id="66d94-236">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="66d94-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66d94-237">d.</span><span class="sxs-lookup"><span data-stu-id="66d94-237">d.</span></span> <span data-ttu-id="66d94-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="66d94-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="66d94-239">Création d’un utilisateur de test Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="66d94-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="66d94-240">tooenable Azure AD les utilisateurs toolog tooZScaler deux, elles doivent être mis en service tooZScaler deux.</span><span class="sxs-lookup"><span data-stu-id="66d94-240">tooenable Azure AD users toolog in tooZScaler Two, they must be provisioned tooZScaler Two.</span></span> <span data-ttu-id="66d94-241">Dans les cas de hello de ZScaler Two, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="66d94-241">In hello case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="66d94-242">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="66d94-243">Connectez-vous à tooyour **Zscaler Two** client.</span><span class="sxs-lookup"><span data-stu-id="66d94-243">Log in tooyour **Zscaler Two** tenant.</span></span>

2. <span data-ttu-id="66d94-244">Cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="66d94-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="66d94-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="66d94-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="66d94-246">Cliquez sur **User Management**.</span><span class="sxs-lookup"><span data-stu-id="66d94-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="66d94-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span><span class="sxs-lookup"><span data-stu-id="66d94-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="66d94-248">Bonjour **utilisateurs** , cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="66d94-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="66d94-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="66d94-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="66d94-250">Dans la section Ajouter un utilisateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="66d94-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="66d94-251">![Ajouter un utilisateur](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="66d94-251">![Add User](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="66d94-252">a.</span><span class="sxs-lookup"><span data-stu-id="66d94-252">a.</span></span> <span data-ttu-id="66d94-253">Hello de type **UserID**, **nom d’utilisateur complet**, **mot de passe**, **confirmer le mot de passe**, puis sélectionnez **groupes**et hello **service** d’un Azure valide compte AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="66d94-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="66d94-254">b.</span><span class="sxs-lookup"><span data-stu-id="66d94-254">b.</span></span> <span data-ttu-id="66d94-255">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="66d94-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="66d94-256">Vous pouvez utiliser n’importe quel autre ZScaler Two utilisateur compte outil de création ou API fournie par ZScaler Two tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66d94-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66d94-257">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="66d94-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66d94-258">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZscaler deux.</span><span class="sxs-lookup"><span data-stu-id="66d94-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Two.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="66d94-260">**tooassign Britta Simon tooZscaler deux, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="66d94-260">**tooassign Britta Simon tooZscaler Two, perform hello following steps:**</span></span>

1. <span data-ttu-id="66d94-261">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="66d94-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="66d94-263">Dans la liste des applications hello, sélectionnez **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="66d94-263">In hello applications list, select **Zscaler Two**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. <span data-ttu-id="66d94-265">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="66d94-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="66d94-267">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="66d94-267">Click **Add** button.</span></span> <span data-ttu-id="66d94-268">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="66d94-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="66d94-270">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="66d94-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66d94-271">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="66d94-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66d94-272">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="66d94-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66d94-273">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="66d94-273">Testing single sign-on</span></span>

<span data-ttu-id="66d94-274">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="66d94-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66d94-275">Lorsque vous cliquez sur hello vignette Zscaler Two Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="66d94-275">When you click hello Zscaler Two tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Two application.</span></span>
<span data-ttu-id="66d94-276">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66d94-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66d94-277">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="66d94-277">Additional resources</span></span>

* [<span data-ttu-id="66d94-278">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66d94-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66d94-279">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="66d94-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png

