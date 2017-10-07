---
title: "Didacticiel : Intégration d’Azure Active Directory à Capriza Platform | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la plateforme de Capriza."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1c4adb737bb5ba4690bbf74688010238c5c83f3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="73c43-103">Didacticiel : Intégration d’Azure Active Directory à Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="73c43-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="73c43-104">Dans ce didacticiel, vous apprendrez comment toointegrate plateforme Capriza avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73c43-104">In this tutorial, you learn how toointegrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73c43-105">Intégration Capriza plate-forme à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="73c43-105">Integrating Capriza Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73c43-106">Vous pouvez contrôler dans Azure AD qui a accès tooCapriza plateforme</span><span class="sxs-lookup"><span data-stu-id="73c43-106">You can control in Azure AD who has access tooCapriza Platform</span></span>
- <span data-ttu-id="73c43-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCapriza plateforme (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-107">You can enable your users tooautomatically get signed-on tooCapriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73c43-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="73c43-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73c43-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73c43-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73c43-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="73c43-110">Prerequisites</span></span>

<span data-ttu-id="73c43-111">tooconfigure intégration d’Azure AD avec Capriza plateforme, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="73c43-111">tooconfigure Azure AD integration with Capriza Platform, you need hello following items:</span></span>

- <span data-ttu-id="73c43-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73c43-113">Un abonnement Capriza Platform pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="73c43-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73c43-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="73c43-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73c43-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="73c43-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73c43-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="73c43-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73c43-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73c43-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73c43-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="73c43-118">Scenario description</span></span>
<span data-ttu-id="73c43-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="73c43-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73c43-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="73c43-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73c43-121">Ajout de Capriza plate-forme à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="73c43-121">Adding Capriza Platform from hello gallery</span></span>
2. <span data-ttu-id="73c43-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-hello-gallery"></a><span data-ttu-id="73c43-123">Ajout de Capriza plate-forme à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="73c43-123">Adding Capriza Platform from hello gallery</span></span>
<span data-ttu-id="73c43-124">intégration de hello tooconfigure de Capriza plateforme dans Azure AD, vous devez tooadd Capriza plate-forme à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="73c43-124">tooconfigure hello integration of Capriza Platform into Azure AD, you need tooadd Capriza Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73c43-125">**tooadd plateforme Capriza à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="73c43-125">**tooadd Capriza Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c43-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="73c43-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73c43-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="73c43-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73c43-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="73c43-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="73c43-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="73c43-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="73c43-133">Dans la zone de recherche de hello, tapez **Capriza plateforme**.</span><span class="sxs-lookup"><span data-stu-id="73c43-133">In hello search box, type **Capriza Platform**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="73c43-135">Dans le volet de résultats hello, sélectionnez **Capriza plateforme**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="73c43-135">In hello results panel, select **Capriza Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73c43-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73c43-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Capriza Platform avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="73c43-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73c43-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Capriza plate-forme est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73c43-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Capriza Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="73c43-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Capriza plate-forme doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="73c43-140">In other words, a link relationship between an Azure AD user and hello related user in Capriza Platform needs toobe established.</span></span>

<span data-ttu-id="73c43-141">Dans la plate-forme Capriza, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="73c43-141">In Capriza Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73c43-142">tooconfigure et test Azure AD l’authentification unique avec la plateforme de Capriza, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="73c43-142">tooconfigure and test Azure AD single sign-on with Capriza Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73c43-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="73c43-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73c43-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73c43-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73c43-145">**[Création d’un utilisateur de test de plateforme de Capriza](#creating-a-capriza-platform-test-user)**  -toohave un équivalent de Britta Simon dans Capriza plate-forme qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="73c43-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - toohave a counterpart of Britta Simon in Capriza Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73c43-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="73c43-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73c43-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="73c43-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73c43-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73c43-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de plateforme de Capriza.</span><span class="sxs-lookup"><span data-stu-id="73c43-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="73c43-150">**tooconfigure Azure AD authentification unique avec les plateformes Capriza, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="73c43-150">**tooconfigure Azure AD single sign-on with Capriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c43-151">Bonjour portail Azure, sur hello **Capriza plateforme** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="73c43-151">In hello Azure portal, on hello **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="73c43-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="73c43-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="73c43-155">Sur hello **Capriza plate-forme de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="73c43-155">On hello **Capriza Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="73c43-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="73c43-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73c43-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="73c43-158">This value is not real.</span></span> <span data-ttu-id="73c43-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="73c43-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="73c43-160">Contact [équipe de support Client de plateforme Capriza](mailTo:support@capriza.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="73c43-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) tooget this value.</span></span> 

4. <span data-ttu-id="73c43-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="73c43-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="73c43-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="73c43-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73c43-165">Sur hello **Configuration de la plateforme Capriza** , cliquez sur **configurer la plateforme de Capriza** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="73c43-165">On hello **Capriza Platform Configuration** section, click **Configure Capriza Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73c43-166">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="73c43-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="73c43-168">tooconfigure l’authentification unique sur **Capriza plateforme** côté, vous devez hello toosend téléchargé **certificat**, **URL de déconnexion**, **ID d’entité SAML** et **SAML Sign-On URL du Service unique** trop[équipe de support de plate-forme de Capriza](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="73c43-168">tooconfigure single sign-on on **Capriza Platform** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="73c43-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="73c43-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="73c43-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="73c43-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73c43-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="73c43-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73c43-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73c43-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73c43-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="73c43-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="73c43-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="73c43-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="73c43-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c43-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="73c43-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73c43-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="73c43-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73c43-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="73c43-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73c43-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="73c43-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73c43-185">a.</span><span class="sxs-lookup"><span data-stu-id="73c43-185">a.</span></span> <span data-ttu-id="73c43-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73c43-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73c43-187">b.</span><span class="sxs-lookup"><span data-stu-id="73c43-187">b.</span></span> <span data-ttu-id="73c43-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73c43-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73c43-189">c.</span><span class="sxs-lookup"><span data-stu-id="73c43-189">c.</span></span> <span data-ttu-id="73c43-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="73c43-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73c43-191">d.</span><span class="sxs-lookup"><span data-stu-id="73c43-191">d.</span></span> <span data-ttu-id="73c43-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="73c43-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="73c43-193">Création d’un utilisateur test Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="73c43-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="73c43-194">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Capriza.</span><span class="sxs-lookup"><span data-stu-id="73c43-194">hello objective of this section is toocreate a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="73c43-195">Capriza prend en charge l'approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="73c43-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="73c43-196">**Vérifiez que votre nom de domaine a été correctement configuré avec Capriza pour l’approvisionnement des utilisateurs. Configuration de l’utilisateur de juste-à-temps fonctionne après que hello uniquement.**</span><span class="sxs-lookup"><span data-stu-id="73c43-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only hello just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="73c43-197">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="73c43-197">There is no action item for you in this section.</span></span> <span data-ttu-id="73c43-198">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Capriza s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="73c43-198">A new user will be created during an attempt tooaccess Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73c43-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="73c43-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73c43-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCapriza plateforme.</span><span class="sxs-lookup"><span data-stu-id="73c43-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCapriza Platform.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="73c43-202">**tooassign Britta Simon tooCapriza plateforme, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="73c43-202">**tooassign Britta Simon tooCapriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="73c43-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="73c43-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="73c43-205">Dans la liste des applications hello, sélectionnez **Capriza plateforme**.</span><span class="sxs-lookup"><span data-stu-id="73c43-205">In hello applications list, select **Capriza Platform**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="73c43-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="73c43-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="73c43-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="73c43-209">Click **Add** button.</span></span> <span data-ttu-id="73c43-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="73c43-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="73c43-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="73c43-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73c43-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="73c43-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73c43-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="73c43-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73c43-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="73c43-215">Testing single sign-on</span></span>

<span data-ttu-id="73c43-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="73c43-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73c43-217">Lorsque vous cliquez sur hello Capriza plateforme vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Capriza application.</span><span class="sxs-lookup"><span data-stu-id="73c43-217">When you click hello Capriza Platform tile in hello Access Panel, you should get automatically signed-on tooyour Capriza application.</span></span> <span data-ttu-id="73c43-218">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73c43-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="73c43-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="73c43-219">Additional resources</span></span>

* [<span data-ttu-id="73c43-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73c43-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73c43-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="73c43-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

