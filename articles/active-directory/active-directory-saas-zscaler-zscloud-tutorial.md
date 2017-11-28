---
title: "Didacticiel : Intégration d’Azure Active Directory avec Zscaler ZSCloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="e4628-103">Didacticiel : Intégration d’Azure Active Directory avec Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e4628-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="e4628-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zscaler ZSCloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e4628-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4628-105">Intégration de Zscaler ZSCloud à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e4628-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e4628-106">Vous pouvez contrôler dans Azure AD qui a accès tooZscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e4628-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="e4628-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZscaler ZSCloud (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4628-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e4628-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e4628-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e4628-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4628-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e4628-110">Prerequisites</span></span>

<span data-ttu-id="e4628-111">tooconfigure intégration d’Azure AD à Zscaler ZSCloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e4628-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="e4628-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4628-113">Un abonnement Zscaler ZSCloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e4628-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4628-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e4628-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4628-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e4628-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4628-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e4628-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4628-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4628-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4628-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e4628-118">Scenario description</span></span>
<span data-ttu-id="e4628-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e4628-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4628-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e4628-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4628-121">Ajout de Zscaler ZSCloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e4628-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="e4628-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="e4628-123">Ajout de Zscaler ZSCloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e4628-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="e4628-124">intégration de hello tooconfigure de Zscaler ZSCloud dans Azure AD, vous devez tooadd Zscaler ZSCloud à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e4628-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e4628-125">**tooadd Zscaler ZSCloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e4628-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4628-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e4628-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4628-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e4628-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e4628-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e4628-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e4628-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e4628-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e4628-133">Dans la zone de recherche de hello, tapez **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="e4628-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="e4628-135">Dans le volet de résultats hello, sélectionnez **Zscaler ZSCloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e4628-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4628-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4628-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler ZSCloud grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e4628-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e4628-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zscaler ZSCloud est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4628-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="e4628-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zscaler ZSCloud doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e4628-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="e4628-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e4628-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="e4628-142">tooconfigure et test Azure AD l’authentification unique avec Zscaler ZSCloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e4628-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e4628-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e4628-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e4628-144">**[Configuration des paramètres proxy](#configuring-proxy-settings)**  -paramètres de proxy tooconfigure hello dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="e4628-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="e4628-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4628-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4628-146">**[Création d’un utilisateur de test de Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave un équivalent de Britta Simon dans Zscaler ZSCloud qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e4628-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4628-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e4628-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4628-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e4628-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4628-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4628-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e4628-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="e4628-151">**tooconfigure Azure AD single sign-on avec Zscaler ZSCloud, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e4628-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4628-152">Bonjour portail Azure, sur hello **Zscaler ZSCloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e4628-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e4628-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e4628-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="e4628-156">Sur hello **Zscaler ZSCloud domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="e4628-158">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour application ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e4628-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e4628-159">Vous avez tooupdate cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="e4628-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e4628-160">Contact [équipe de support technique Zscaler ZSCloud Client](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e4628-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="e4628-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e4628-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="e4628-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e4628-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4628-165">Sur hello **Zscaler ZSCloud Configuration** , cliquez sur **configurer Zscaler ZSCloud** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e4628-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e4628-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e4628-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="e4628-168">Dans une fenêtre de navigateur web, connectez-vous tooyour site de société ZScaler ZSCloud en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e4628-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="e4628-169">Dans le menu hello haut de hello, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="e4628-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="e4628-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="e4628-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="e4628-171">Sous **Manage Administrators & Roles**, cliquez sur **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="e4628-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="e4628-172">![Gérer les utilisateurs et l’authentification](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Gérer les utilisateurs et l’authentification")</span><span class="sxs-lookup"><span data-stu-id="e4628-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="e4628-173">Bonjour **choisir les Options d’authentification pour votre organisation** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="e4628-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="e4628-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="e4628-175">a.</span><span class="sxs-lookup"><span data-stu-id="e4628-175">a.</span></span> <span data-ttu-id="e4628-176">Sélectionnez **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e4628-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="e4628-177">b.</span><span class="sxs-lookup"><span data-stu-id="e4628-177">b.</span></span> <span data-ttu-id="e4628-178">Cliquez sur **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="e4628-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="e4628-179">Sur hello **Configure SAML Single Sign-On Parameters** page de boîte de dialogue, effectuer hello comme suit, puis cliquez sur **terminé**</span><span class="sxs-lookup"><span data-stu-id="e4628-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="e4628-180">![Authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="e4628-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="e4628-181">a.</span><span class="sxs-lookup"><span data-stu-id="e4628-181">a.</span></span> <span data-ttu-id="e4628-182">Hello de coller **SAML Sign-On URL du Service unique** valeur hello **URL d’utilisateurs de toowhich hello portail SAML sont envoyés pour l’authentification** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e4628-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="e4628-183">b.</span><span class="sxs-lookup"><span data-stu-id="e4628-183">b.</span></span> <span data-ttu-id="e4628-184">Bonjour **attribut contenant le nom de connexion** zone de texte, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="e4628-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="e4628-185">c.</span><span class="sxs-lookup"><span data-stu-id="e4628-185">c.</span></span> <span data-ttu-id="e4628-186">tooupload votre certificat téléchargé, cliquez sur **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="e4628-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="e4628-187">d.</span><span class="sxs-lookup"><span data-stu-id="e4628-187">d.</span></span> <span data-ttu-id="e4628-188">Sélectionnez **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="e4628-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="e4628-189">Sur hello **configurer l’authentification utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="e4628-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="e4628-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="e4628-191">a.</span><span class="sxs-lookup"><span data-stu-id="e4628-191">a.</span></span> <span data-ttu-id="e4628-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e4628-192">Click **Save**.</span></span>

    <span data-ttu-id="e4628-193">b.</span><span class="sxs-lookup"><span data-stu-id="e4628-193">b.</span></span> <span data-ttu-id="e4628-194">Cliquez sur **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="e4628-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="e4628-195">Configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="e4628-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="e4628-196">paramètres de proxy tooconfigure hello dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="e4628-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="e4628-197">Démarrez **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e4628-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="e4628-198">Sélectionnez **options Internet** de hello **outils** menu Ouvrir hello **Options Internet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e4628-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="e4628-199">![Options Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Options Internet")</span><span class="sxs-lookup"><span data-stu-id="e4628-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="e4628-200">Cliquez sur hello **connexions** onglet.</span><span class="sxs-lookup"><span data-stu-id="e4628-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="e4628-201">![Connexions](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connexions")</span><span class="sxs-lookup"><span data-stu-id="e4628-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="e4628-202">Cliquez sur **paramètres LAN** tooopen hello **paramètres LAN** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e4628-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="e4628-203">Dans la section serveur Proxy de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="e4628-204">![Serveur proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Serveur proxy")</span><span class="sxs-lookup"><span data-stu-id="e4628-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="e4628-205">a.</span><span class="sxs-lookup"><span data-stu-id="e4628-205">a.</span></span> <span data-ttu-id="e4628-206">Sélectionnez **Utiliser un serveur proxy pour le réseau local**.</span><span class="sxs-lookup"><span data-stu-id="e4628-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="e4628-207">b.</span><span class="sxs-lookup"><span data-stu-id="e4628-207">b.</span></span> <span data-ttu-id="e4628-208">Dans la zone de texte adresse hello, tapez **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="e4628-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="e4628-209">c.</span><span class="sxs-lookup"><span data-stu-id="e4628-209">c.</span></span> <span data-ttu-id="e4628-210">Dans la zone de texte Port hello, tapez **80**.</span><span class="sxs-lookup"><span data-stu-id="e4628-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="e4628-211">d.</span><span class="sxs-lookup"><span data-stu-id="e4628-211">d.</span></span> <span data-ttu-id="e4628-212">Sélectionnez **Ne pas utiliser de serveur proxy pour les adresses locales**.</span><span class="sxs-lookup"><span data-stu-id="e4628-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="e4628-213">e.</span><span class="sxs-lookup"><span data-stu-id="e4628-213">e.</span></span> <span data-ttu-id="e4628-214">Cliquez sur **OK** tooclose hello **les paramètres de réseau local (LAN)** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e4628-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="e4628-215">Cliquez sur **OK** tooclose hello **Options Internet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e4628-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4628-216">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4628-217">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e4628-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e4628-219">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e4628-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4628-220">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e4628-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4628-222">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e4628-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4628-224">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e4628-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4628-226">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4628-228">a.</span><span class="sxs-lookup"><span data-stu-id="e4628-228">a.</span></span> <span data-ttu-id="e4628-229">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e4628-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4628-230">b.</span><span class="sxs-lookup"><span data-stu-id="e4628-230">b.</span></span> <span data-ttu-id="e4628-231">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e4628-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4628-232">c.</span><span class="sxs-lookup"><span data-stu-id="e4628-232">c.</span></span> <span data-ttu-id="e4628-233">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e4628-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e4628-234">d.</span><span class="sxs-lookup"><span data-stu-id="e4628-234">d.</span></span> <span data-ttu-id="e4628-235">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4628-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="e4628-236">Créer un utilisateur de test Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e4628-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="e4628-237">tooenable Azure AD les utilisateurs toolog tooZScaler ZSCloud, elles doivent être mis en service tooZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e4628-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="e4628-238">Dans les cas de hello de ZScaler ZSCloud, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e4628-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="e4628-239">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="e4628-240">Connectez-vous à tooyour **Zscaler** client.</span><span class="sxs-lookup"><span data-stu-id="e4628-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="e4628-241">Cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="e4628-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="e4628-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="e4628-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="e4628-243">Cliquez sur **User Management**.</span><span class="sxs-lookup"><span data-stu-id="e4628-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="e4628-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="e4628-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="e4628-245">Bonjour **utilisateurs** , cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e4628-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="e4628-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="e4628-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="e4628-247">Dans la section Ajouter un utilisateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4628-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="e4628-248">![Ajouter un utilisateur](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="e4628-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="e4628-249">a.</span><span class="sxs-lookup"><span data-stu-id="e4628-249">a.</span></span> <span data-ttu-id="e4628-250">Hello de type **UserID**, **nom d’utilisateur complet**, **mot de passe**, **confirmer le mot de passe**, puis sélectionnez **groupes**et hello **service** d’un compte AAD valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="e4628-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="e4628-251">b.</span><span class="sxs-lookup"><span data-stu-id="e4628-251">b.</span></span> <span data-ttu-id="e4628-252">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e4628-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e4628-253">Vous pouvez utiliser n’importe quel autre ZScaler ZSCloud utilisateur compte outil de création ou API fournie par ZScaler ZSCloud tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="e4628-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e4628-254">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4628-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e4628-255">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e4628-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e4628-257">**tooassign Britta Simon tooZscaler ZSCloud, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e4628-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4628-258">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e4628-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e4628-260">Dans la liste des applications hello, sélectionnez **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="e4628-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="e4628-262">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e4628-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e4628-264">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e4628-264">Click **Add** button.</span></span> <span data-ttu-id="e4628-265">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e4628-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e4628-267">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e4628-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e4628-268">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e4628-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4628-269">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e4628-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4628-270">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e4628-270">Testing single sign-on</span></span>

<span data-ttu-id="e4628-271">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e4628-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="e4628-272">Lorsque vous cliquez sur hello Zscaler ZSCloud vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e4628-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="e4628-273">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e4628-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e4628-274">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e4628-274">Additional resources</span></span>

* [<span data-ttu-id="e4628-275">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4628-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4628-276">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e4628-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

