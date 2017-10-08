---
title: "Didacticiel : intégration d’Azure Active Directory dans HappyFox | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="496aa-103">Didacticiel : intégration d’Azure Active Directory dans HappyFox</span><span class="sxs-lookup"><span data-stu-id="496aa-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="496aa-104">Dans ce didacticiel, vous apprendrez comment toointegrate HappyFox avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="496aa-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="496aa-105">Intégration HappyFox à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="496aa-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="496aa-106">Vous pouvez contrôler dans Azure AD qui a accès tooHappyFox</span><span class="sxs-lookup"><span data-stu-id="496aa-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="496aa-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHappyFox (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="496aa-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="496aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="496aa-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="496aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="496aa-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="496aa-110">Prerequisites</span></span>

<span data-ttu-id="496aa-111">tooconfigure intégration d’Azure AD avec HappyFox, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="496aa-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="496aa-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="496aa-113">Un abonnement HappyFox pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="496aa-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="496aa-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="496aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="496aa-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="496aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="496aa-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="496aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="496aa-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="496aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="496aa-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="496aa-118">Scenario description</span></span>
<span data-ttu-id="496aa-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="496aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="496aa-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="496aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="496aa-121">Ajout de HappyFox à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="496aa-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="496aa-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="496aa-123">Ajout de HappyFox à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="496aa-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="496aa-124">intégration de hello tooconfigure de HappyFox dans Azure AD, vous devez tooadd HappyFox à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="496aa-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="496aa-125">**tooadd HappyFox à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="496aa-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="496aa-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="496aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="496aa-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="496aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="496aa-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="496aa-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="496aa-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="496aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="496aa-133">Dans la zone de recherche de hello, tapez **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="496aa-133">In hello search box, type **HappyFox**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="496aa-135">Dans le volet de résultats hello, sélectionnez **HappyFox**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="496aa-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="496aa-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="496aa-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HappyFox, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="496aa-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="496aa-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans HappyFox est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="496aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="496aa-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans HappyFox doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="496aa-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="496aa-141">Dans HappyFox, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="496aa-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="496aa-142">tooconfigure et test Azure AD l’authentification unique avec HappyFox, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="496aa-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="496aa-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="496aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="496aa-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="496aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="496aa-145">**[Création d’un utilisateur de test HappyFox](#creating-a-happyfox-test-user)**  -toohave un équivalent de Britta Simon dans HappyFox est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="496aa-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="496aa-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="496aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="496aa-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="496aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="496aa-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="496aa-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application HappyFox.</span><span class="sxs-lookup"><span data-stu-id="496aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="496aa-150">**tooconfigure Azure AD single sign-on avec HappyFox, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="496aa-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="496aa-151">Bonjour portail Azure, sur hello **HappyFox** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="496aa-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="496aa-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="496aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="496aa-155">Sur hello **HappyFox domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="496aa-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="496aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="496aa-157">a.</span></span> <span data-ttu-id="496aa-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="496aa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="496aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="496aa-159">b.</span></span> <span data-ttu-id="496aa-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="496aa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="496aa-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="496aa-161">These values are not real.</span></span> <span data-ttu-id="496aa-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="496aa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="496aa-163">Contact [équipe de support Client de HappyFox](https://support.happyfox.com/home) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="496aa-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="496aa-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="496aa-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="496aa-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="496aa-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="496aa-168">Sur hello **HappyFox Configuration** , cliquez sur **HappyFox de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="496aa-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="496aa-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="496aa-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="496aa-171">Se connecter sur le portail d’équipe tooyour HappyFox et accédez trop**gérer**, cliquez sur **intégrations** onglet.</span><span class="sxs-lookup"><span data-stu-id="496aa-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="496aa-173">Dans l’onglet d’intégrations hello, cliquez sur **configurer** sous **SAML intégration** tooopen hello Single Sign On Settings.</span><span class="sxs-lookup"><span data-stu-id="496aa-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="496aa-175">Dans la section de configuration de SAML, collez hello **SAML Sign-On URL du Service unique** que vous avez copié à partir du portail Azure en **URL cible de l’authentification unique** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="496aa-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="496aa-177">Ouvrir le certificat hello téléchargé à partir du portail Azure dans le bloc-notes et copiez son contenu dans **IdP Signature** section.</span><span class="sxs-lookup"><span data-stu-id="496aa-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="496aa-179">Cliquez sur le bouton **Enregistrer les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="496aa-179">Click **Save Settings** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="496aa-181">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="496aa-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="496aa-182">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="496aa-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="496aa-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="496aa-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="496aa-184">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="496aa-185">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="496aa-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="496aa-187">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="496aa-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="496aa-188">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="496aa-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="496aa-190">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="496aa-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="496aa-192">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="496aa-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="496aa-194">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="496aa-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="496aa-196">a.</span><span class="sxs-lookup"><span data-stu-id="496aa-196">a.</span></span> <span data-ttu-id="496aa-197">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="496aa-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="496aa-198">b.</span><span class="sxs-lookup"><span data-stu-id="496aa-198">b.</span></span> <span data-ttu-id="496aa-199">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="496aa-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="496aa-200">c.</span><span class="sxs-lookup"><span data-stu-id="496aa-200">c.</span></span> <span data-ttu-id="496aa-201">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="496aa-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="496aa-202">d.</span><span class="sxs-lookup"><span data-stu-id="496aa-202">d.</span></span> <span data-ttu-id="496aa-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="496aa-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="496aa-204">Création d’un utilisateur de test HappyFox</span><span class="sxs-lookup"><span data-stu-id="496aa-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="496aa-205">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="496aa-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="496aa-206">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="496aa-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="496aa-207">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHappyFox.</span><span class="sxs-lookup"><span data-stu-id="496aa-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="496aa-209">**tooassign Britta Simon tooHappyFox, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="496aa-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="496aa-210">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="496aa-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="496aa-212">Dans la liste des applications hello, sélectionnez **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="496aa-212">In hello applications list, select **HappyFox**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="496aa-214">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="496aa-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="496aa-216">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="496aa-216">Click **Add** button.</span></span> <span data-ttu-id="496aa-217">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="496aa-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="496aa-219">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="496aa-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="496aa-220">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="496aa-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="496aa-221">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="496aa-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="496aa-222">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="496aa-222">Testing single sign-on</span></span>

<span data-ttu-id="496aa-223">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="496aa-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="496aa-224">Lorsque vous cliquez sur mosaïque HappyFox hello hello volet d’accès, vous devez obtenir la page de connexion de l’application de HappyFox.</span><span class="sxs-lookup"><span data-stu-id="496aa-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="496aa-225">Vous devez voir hello **'SAML'** bouton sur la page de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="496aa-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Plug-in](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="496aa-227">Cliquez sur hello **'SAML'** toolog de bouton dans tooHappyFox à l’aide de votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="496aa-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="496aa-228">Pour plus d’informations sur hello volet d’accès, consultez [présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="496aa-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="496aa-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="496aa-229">Additional resources</span></span>

* [<span data-ttu-id="496aa-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="496aa-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="496aa-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="496aa-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

