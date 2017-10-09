---
title: "Didacticiel : Intégration d’Azure Active Directory avec InTime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="42512-103">Didacticiel : Intégration d’Azure Active Directory avec InTime</span><span class="sxs-lookup"><span data-stu-id="42512-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="42512-104">Dans ce didacticiel, vous apprendrez comment toointegrate InTime avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42512-104">In this tutorial, you learn how toointegrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42512-105">Intégration InTime à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="42512-105">Integrating InTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42512-106">Vous pouvez contrôler dans Azure AD qui a accès tooInTime.</span><span class="sxs-lookup"><span data-stu-id="42512-106">You can control in Azure AD who has access tooInTime.</span></span>
- <span data-ttu-id="42512-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooInTime (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42512-107">You can enable your users tooautomatically get signed-on tooInTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="42512-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42512-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="42512-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42512-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42512-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="42512-110">Prerequisites</span></span>

<span data-ttu-id="42512-111">tooconfigure intégration d’Azure AD avec InTime, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="42512-111">tooconfigure Azure AD integration with InTime, you need hello following items:</span></span>

- <span data-ttu-id="42512-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="42512-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42512-113">Un abonnement InTime pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="42512-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42512-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="42512-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42512-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="42512-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42512-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42512-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42512-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42512-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42512-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="42512-118">Scenario description</span></span>
<span data-ttu-id="42512-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="42512-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42512-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="42512-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42512-121">Ajout de InTime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="42512-121">Adding InTime from hello gallery</span></span>
2. <span data-ttu-id="42512-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42512-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-hello-gallery"></a><span data-ttu-id="42512-123">Ajout de InTime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="42512-123">Adding InTime from hello gallery</span></span>
<span data-ttu-id="42512-124">tooconfigure hello intégration de InTime dans Azure AD, vous devez tooadd InTime à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="42512-124">tooconfigure hello integration of InTime into Azure AD, you need tooadd InTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42512-125">**tooadd InTime à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42512-125">**tooadd InTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42512-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="42512-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="42512-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="42512-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42512-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42512-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="42512-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42512-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="42512-133">Dans la zone de recherche de hello, tapez **InTime**, sélectionnez **InTime** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="42512-133">In hello search box, type **InTime**, select **InTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![InTime dans la liste des résultats hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="42512-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42512-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="42512-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec InTime, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="42512-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42512-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello InTime est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42512-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InTime is tooa user in Azure AD.</span></span> <span data-ttu-id="42512-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans InTime doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="42512-138">In other words, a link relationship between an Azure AD user and hello related user in InTime needs toobe established.</span></span>

<span data-ttu-id="42512-139">Dans InTime, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="42512-139">In InTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="42512-140">tooconfigure et test Azure AD l’authentification unique avec InTime, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="42512-140">tooconfigure and test Azure AD single sign-on with InTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42512-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="42512-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42512-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42512-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42512-143">**[Créer un utilisateur test InTime](#create-a-intime-test-user)**  -toohave un équivalent de Britta Simon dans InTime est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="42512-143">**[Create a InTime test user](#create-a-intime-test-user)** - toohave a counterpart of Britta Simon in InTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42512-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42512-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42512-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="42512-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="42512-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42512-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="42512-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application InTime.</span><span class="sxs-lookup"><span data-stu-id="42512-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="42512-148">**tooconfigure Azure AD single sign-on avec InTime, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42512-148">**tooconfigure Azure AD single sign-on with InTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="42512-149">Bonjour portail Azure, sur hello **InTime** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="42512-149">In hello Azure portal, on hello **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="42512-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42512-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="42512-153">Sur hello **InTime de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42512-153">On hello **InTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="42512-155">a.</span><span class="sxs-lookup"><span data-stu-id="42512-155">a.</span></span> <span data-ttu-id="42512-156">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="42512-156">In hello **Sign-on URL** textbox, type hello URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="42512-157">b.</span><span class="sxs-lookup"><span data-stu-id="42512-157">b.</span></span> <span data-ttu-id="42512-158">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="42512-158">In hello **Identifier** textbox, type hello URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="42512-159">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="42512-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="42512-161">Votre application InTime attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="42512-161">Your InTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="42512-162">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="42512-162">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="42512-163">Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais InTime attend ce toobe mappée avec une adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="42512-163">hello default value of **User Identifier** is **user.userprincipalname** but InTime expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="42512-164">Pour cela, vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de votre configuration de l’organisation</span><span class="sxs-lookup"><span data-stu-id="42512-164">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration</span></span> 

    ![Configurer l’attribut](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="42512-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="42512-166">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="42512-168">Sur hello **Configuration InTime** , cliquez sur **configurer InTime** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="42512-168">On hello **InTime Configuration** section, click **Configure InTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="42512-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="42512-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="42512-171">tooconfigure l’authentification unique sur **InTime** côté, vous devez hello toosend téléchargé **Metadata XML**, **URL de déconnexion et SAML Sign-On URL du Service unique** trop[Équipe de support inTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="42512-171">tooconfigure single sign-on on **InTime** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** too[InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="42512-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="42512-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="42512-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="42512-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42512-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="42512-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42512-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42512-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="42512-176">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42512-176">Create an Azure AD test user</span></span>

<span data-ttu-id="42512-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="42512-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="42512-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42512-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42512-180">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="42512-180">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="42512-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42512-182">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="42512-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42512-184">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="42512-186">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42512-186">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="42512-188">a.</span><span class="sxs-lookup"><span data-stu-id="42512-188">a.</span></span> <span data-ttu-id="42512-189">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42512-189">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42512-190">b.</span><span class="sxs-lookup"><span data-stu-id="42512-190">b.</span></span> <span data-ttu-id="42512-191">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42512-191">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="42512-192">c.</span><span class="sxs-lookup"><span data-stu-id="42512-192">c.</span></span> <span data-ttu-id="42512-193">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="42512-193">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="42512-194">d.</span><span class="sxs-lookup"><span data-stu-id="42512-194">d.</span></span> <span data-ttu-id="42512-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="42512-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="42512-196">Créer un utilisateur de test InTime</span><span class="sxs-lookup"><span data-stu-id="42512-196">Create a InTime test user</span></span>

<span data-ttu-id="42512-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans InTime.</span><span class="sxs-lookup"><span data-stu-id="42512-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="42512-198">Travailler avec [équipe de support InTime](mailto:hdollard@intimesoft.com) utilisateurs hello tooadd plateforme InTime de hello.</span><span class="sxs-lookup"><span data-stu-id="42512-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) tooadd hello users in hello InTime platform.</span></span> <span data-ttu-id="42512-199">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42512-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="42512-200">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="42512-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="42512-201">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooInTime.</span><span class="sxs-lookup"><span data-stu-id="42512-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInTime.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="42512-203">**tooassign Britta Simon tooInTime, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42512-203">**tooassign Britta Simon tooInTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="42512-204">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42512-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="42512-206">Dans la liste des applications hello, sélectionnez **InTime**.</span><span class="sxs-lookup"><span data-stu-id="42512-206">In hello applications list, select **InTime**.</span></span>

    ![Hello InTime lien dans la liste des Applications hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="42512-208">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42512-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="42512-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="42512-210">Click **Add** button.</span></span> <span data-ttu-id="42512-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42512-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="42512-213">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="42512-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42512-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42512-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42512-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42512-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="42512-216">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="42512-216">Test single sign-on</span></span>

<span data-ttu-id="42512-217">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="42512-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="42512-218">Lorsque vous cliquez sur la vignette de InTime hello dans hello volet d’accès, vous devez obtenir la page de connexion hello de votre application InTime.</span><span class="sxs-lookup"><span data-stu-id="42512-218">When you click hello InTime tile in hello Access Panel, you should get hello login page of your InTime application.</span></span> <span data-ttu-id="42512-219">Cliquez sur hello **connexion** bouton, une série de IdPs sera affichée sur une liste de boutons.</span><span class="sxs-lookup"><span data-stu-id="42512-219">Click hello **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="42512-220">Cliquez sur **nom de l’IDP** donné par [équipe de support InTime](mailto:hdollard@intimesoft.com) toologin dans votre application InTime.</span><span class="sxs-lookup"><span data-stu-id="42512-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) toologin into your InTime application.</span></span> <span data-ttu-id="42512-221">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42512-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42512-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="42512-222">Additional resources</span></span>

* [<span data-ttu-id="42512-223">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42512-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42512-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="42512-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

