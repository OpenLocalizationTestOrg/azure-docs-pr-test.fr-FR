---
title: "Didacticiel : Intégration d’Azure Active Directory à Origami | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="27209-103">Didacticiel : Intégration d’Azure Active Directory à Origami</span><span class="sxs-lookup"><span data-stu-id="27209-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="27209-104">Dans ce didacticiel, vous apprendrez comment toointegrate Origami avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27209-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27209-105">Intégration Origami à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="27209-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27209-106">Vous pouvez contrôler dans Azure AD qui a accès tooOrigami</span><span class="sxs-lookup"><span data-stu-id="27209-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="27209-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOrigami (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27209-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="27209-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27209-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27209-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27209-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="27209-110">Prerequisites</span></span>

<span data-ttu-id="27209-111">tooconfigure intégration d’Azure AD avec Origami, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="27209-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="27209-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27209-113">Un abonnement Origami pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="27209-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27209-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="27209-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27209-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="27209-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27209-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="27209-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27209-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27209-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27209-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="27209-118">Scenario description</span></span>
<span data-ttu-id="27209-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="27209-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27209-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="27209-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27209-121">Ajout de Origami à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="27209-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="27209-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="27209-123">Ajout de Origami à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="27209-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="27209-124">tooconfigure hello intégration de Origami dans Azure AD, vous devez tooadd Origami à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="27209-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27209-125">**tooadd Origami à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="27209-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27209-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="27209-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27209-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="27209-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27209-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="27209-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="27209-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="27209-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="27209-133">Dans la zone de recherche de hello, tapez **Origami**.</span><span class="sxs-lookup"><span data-stu-id="27209-133">In hello search box, type **Origami**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="27209-135">Dans le volet de résultats hello, sélectionnez **Origami**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27209-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27209-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27209-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Origami avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="27209-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27209-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Origami est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27209-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="27209-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Origami doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="27209-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="27209-141">Dans Origami, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="27209-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27209-142">tooconfigure et test Azure AD l’authentification unique avec Origami, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="27209-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27209-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="27209-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27209-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27209-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27209-145">**[Création d’un utilisateur de test Origami](#creating-an-origami-test-user)**  -toohave un équivalent de Britta Simon dans Origami qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="27209-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27209-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="27209-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27209-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="27209-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27209-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27209-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Origami.</span><span class="sxs-lookup"><span data-stu-id="27209-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="27209-150">**tooconfigure Azure AD single sign-on avec Origami, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="27209-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="27209-151">Bonjour portail Azure, sur hello **Origami** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="27209-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="27209-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="27209-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="27209-155">Sur hello **Origami domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="27209-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="27209-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="27209-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="27209-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="27209-158">hello value is not real.</span></span> <span data-ttu-id="27209-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="27209-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="27209-160">Contact [équipe de support Client de Origami](https://wordpress.org/support/theme/origami) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="27209-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="27209-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="27209-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="27209-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="27209-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27209-165">Sur hello **Origami Configuration** , cliquez sur **configurer un Origami** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="27209-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27209-166">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="27209-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="27209-168">Ouvrez une session dans toohello compte de Origami avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="27209-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="27209-169">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="27209-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="27209-171">Sur la page de boîte de dialogue d’authentification unique sur l’installation de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="27209-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="27209-173">a.</span><span class="sxs-lookup"><span data-stu-id="27209-173">a.</span></span> <span data-ttu-id="27209-174">Sélectionnez **Activer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="27209-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="27209-175">b.</span><span class="sxs-lookup"><span data-stu-id="27209-175">b.</span></span> <span data-ttu-id="27209-176">Bonjour **Page URL de connexion du fournisseur d’identité** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="27209-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="27209-177">c.</span><span class="sxs-lookup"><span data-stu-id="27209-177">c.</span></span> <span data-ttu-id="27209-178">Bonjour **URL de Page de déconnexion du fournisseur d’identité** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="27209-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="27209-179">d.</span><span class="sxs-lookup"><span data-stu-id="27209-179">d.</span></span> <span data-ttu-id="27209-180">Cliquez sur **Parcourir** certificat de hello tooupload vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="27209-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="27209-181">e.</span><span class="sxs-lookup"><span data-stu-id="27209-181">e.</span></span> <span data-ttu-id="27209-182">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="27209-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="27209-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="27209-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27209-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="27209-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27209-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27209-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27209-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="27209-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="27209-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="27209-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="27209-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27209-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="27209-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27209-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="27209-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27209-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="27209-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27209-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="27209-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27209-198">a.</span><span class="sxs-lookup"><span data-stu-id="27209-198">a.</span></span> <span data-ttu-id="27209-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27209-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27209-200">b.</span><span class="sxs-lookup"><span data-stu-id="27209-200">b.</span></span> <span data-ttu-id="27209-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27209-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27209-202">c.</span><span class="sxs-lookup"><span data-stu-id="27209-202">c.</span></span> <span data-ttu-id="27209-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="27209-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27209-204">d.</span><span class="sxs-lookup"><span data-stu-id="27209-204">d.</span></span> <span data-ttu-id="27209-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="27209-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="27209-206">Création d’un utilisateur de test Origami</span><span class="sxs-lookup"><span data-stu-id="27209-206">Creating an Origami test user</span></span>

<span data-ttu-id="27209-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Origami.</span><span class="sxs-lookup"><span data-stu-id="27209-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="27209-208">Ouvrez une session dans toohello compte de Origami avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="27209-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="27209-209">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="27209-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="27209-211">Sur hello **les utilisateurs et sécurité** boîte de dialogue, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="27209-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="27209-213">Cliquez sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="27209-213">Click **Add New User**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="27209-215">Dans la boîte de dialogue Ajouter un nouvel utilisateur hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="27209-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="27209-217">a.</span><span class="sxs-lookup"><span data-stu-id="27209-217">a.</span></span> <span data-ttu-id="27209-218">Bonjour **nom d’utilisateur** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="27209-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="27209-219">b.</span><span class="sxs-lookup"><span data-stu-id="27209-219">b.</span></span> <span data-ttu-id="27209-220">Bonjour **mot de passe** zone de texte, tapez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="27209-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="27209-221">c.</span><span class="sxs-lookup"><span data-stu-id="27209-221">c.</span></span> <span data-ttu-id="27209-222">Bonjour **confirmer le mot de passe** zone de texte, type hello mot de passe.</span><span class="sxs-lookup"><span data-stu-id="27209-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="27209-223">d.</span><span class="sxs-lookup"><span data-stu-id="27209-223">d.</span></span> <span data-ttu-id="27209-224">Bonjour **prénom** zone de texte, entrez hello premier nom d’utilisateur comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="27209-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="27209-225">e.</span><span class="sxs-lookup"><span data-stu-id="27209-225">e.</span></span> <span data-ttu-id="27209-226">Bonjour **nom** zone de texte, entrez le nom d’utilisateur comme hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="27209-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="27209-227">f.</span><span class="sxs-lookup"><span data-stu-id="27209-227">f.</span></span> <span data-ttu-id="27209-228">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="27209-228">Click **Save**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="27209-230">Affecter **rôles d’utilisateur** et **accès Client** toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="27209-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27209-232">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27209-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27209-233">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOrigami.</span><span class="sxs-lookup"><span data-stu-id="27209-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="27209-235">**tooassign Britta Simon tooOrigami, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="27209-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="27209-236">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="27209-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="27209-238">Dans la liste des applications hello, sélectionnez **Origami**.</span><span class="sxs-lookup"><span data-stu-id="27209-238">In hello applications list, select **Origami**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="27209-240">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="27209-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="27209-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="27209-242">Click **Add** button.</span></span> <span data-ttu-id="27209-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="27209-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="27209-245">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="27209-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27209-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="27209-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27209-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="27209-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27209-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="27209-248">Testing single sign-on</span></span>

<span data-ttu-id="27209-249">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="27209-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27209-250">Lorsque vous cliquez sur mosaïque Origami hello hello volet d’accès, vous devez obtenir l’application de Origami automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="27209-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27209-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="27209-251">Additional resources</span></span>

* [<span data-ttu-id="27209-252">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27209-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27209-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="27209-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

