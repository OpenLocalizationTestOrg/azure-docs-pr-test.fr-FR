---
title: "Didacticiel : Intégration d’Azure Active Directory avec RolePoint | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 8629dd87c17d44ab89251ebbd19156c6d6cbedc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="ae07b-103">Didacticiel : Intégration d’Azure Active Directory avec RolePoint</span><span class="sxs-lookup"><span data-stu-id="ae07b-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="ae07b-104">Dans ce didacticiel, vous apprendrez comment toointegrate RolePoint avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae07b-104">In this tutorial, you learn how toointegrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae07b-105">Intégration RolePoint à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ae07b-105">Integrating RolePoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae07b-106">Vous pouvez contrôler dans Azure AD qui a accès tooRolePoint</span><span class="sxs-lookup"><span data-stu-id="ae07b-106">You can control in Azure AD who has access tooRolePoint</span></span>
- <span data-ttu-id="ae07b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRolePoint (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-107">You can enable your users tooautomatically get signed-on tooRolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae07b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae07b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ae07b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae07b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae07b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae07b-110">Prerequisites</span></span>

<span data-ttu-id="ae07b-111">tooconfigure intégration d’Azure AD avec RolePoint, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae07b-111">tooconfigure Azure AD integration with RolePoint, you need hello following items:</span></span>

- <span data-ttu-id="ae07b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae07b-113">Un abonnement RolePoint pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ae07b-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae07b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ae07b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae07b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ae07b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae07b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ae07b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae07b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae07b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae07b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ae07b-118">Scenario description</span></span>
<span data-ttu-id="ae07b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ae07b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae07b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ae07b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae07b-121">Ajout de RolePoint à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ae07b-121">Adding RolePoint from hello gallery</span></span>
2. <span data-ttu-id="ae07b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-hello-gallery"></a><span data-ttu-id="ae07b-123">Ajout de RolePoint à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ae07b-123">Adding RolePoint from hello gallery</span></span>
<span data-ttu-id="ae07b-124">intégration de hello tooconfigure de RolePoint dans Azure AD, vous devez tooadd RolePoint à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ae07b-124">tooconfigure hello integration of RolePoint into Azure AD, you need tooadd RolePoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae07b-125">**tooadd RolePoint à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae07b-125">**tooadd RolePoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae07b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ae07b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae07b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae07b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ae07b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae07b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ae07b-133">Dans la zone de recherche de hello, tapez **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-133">In hello search box, type **RolePoint**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="ae07b-135">Dans le volet de résultats hello, sélectionnez **RolePoint**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ae07b-135">In hello results panel, select **RolePoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae07b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae07b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RolePoint grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ae07b-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae07b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans RolePoint est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae07b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RolePoint is tooa user in Azure AD.</span></span> <span data-ttu-id="ae07b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans RolePoint doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ae07b-140">In other words, a link relationship between an Azure AD user and hello related user in RolePoint needs toobe established.</span></span>

<span data-ttu-id="ae07b-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans RolePoint.</span><span class="sxs-lookup"><span data-stu-id="ae07b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in RolePoint.</span></span>

<span data-ttu-id="ae07b-142">tooconfigure et test Azure AD l’authentification unique avec RolePoint, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ae07b-142">tooconfigure and test Azure AD single sign-on with RolePoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae07b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ae07b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae07b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae07b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae07b-145">**[Création d’un utilisateur de test RolePoint](#creating-a-rolepoint-test-user)**  -toohave un équivalent de Britta Simon dans RolePoint est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ae07b-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - toohave a counterpart of Britta Simon in RolePoint that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae07b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ae07b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae07b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ae07b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae07b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae07b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application RolePoint.</span><span class="sxs-lookup"><span data-stu-id="ae07b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="ae07b-150">**tooconfigure Azure AD single sign-on avec RolePoint, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae07b-150">**tooconfigure Azure AD single sign-on with RolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae07b-151">Bonjour portail Azure, sur hello **RolePoint** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-151">In hello Azure portal, on hello **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ae07b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ae07b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="ae07b-155">Sur hello **RolePoint domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae07b-155">On hello **RolePoint Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="ae07b-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae07b-157">a.</span></span> <span data-ttu-id="ae07b-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="ae07b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="ae07b-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae07b-159">b.</span></span> <span data-ttu-id="ae07b-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ae07b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae07b-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="ae07b-161">These values are not hello real.</span></span> <span data-ttu-id="ae07b-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="ae07b-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="ae07b-163">Ici nous vous suggérons toouse hello unique valeur chaîne Bonjour Identifier.Contact [équipe de support RolePoint](mailto:info@rolepoint.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="ae07b-163">Here we suggest you toouse hello unique value of string in hello Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="ae07b-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ae07b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="ae07b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ae07b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="ae07b-168">tooconfigure l’authentification unique sur **RolePoint** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="ae07b-168">tooconfigure single sign-on on **RolePoint** side, you need toosend hello downloaded **Metadata XML** too[RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="ae07b-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ae07b-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ae07b-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ae07b-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ae07b-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae07b-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae07b-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae07b-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ae07b-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ae07b-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae07b-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae07b-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ae07b-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae07b-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae07b-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ae07b-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae07b-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae07b-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae07b-184">a.</span><span class="sxs-lookup"><span data-stu-id="ae07b-184">a.</span></span> <span data-ttu-id="ae07b-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae07b-186">b.</span><span class="sxs-lookup"><span data-stu-id="ae07b-186">b.</span></span> <span data-ttu-id="ae07b-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae07b-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae07b-188">c.</span><span class="sxs-lookup"><span data-stu-id="ae07b-188">c.</span></span> <span data-ttu-id="ae07b-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae07b-190">d.</span><span class="sxs-lookup"><span data-stu-id="ae07b-190">d.</span></span> <span data-ttu-id="ae07b-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="ae07b-192">Création d’un utilisateur de test RolePoint</span><span class="sxs-lookup"><span data-stu-id="ae07b-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="ae07b-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans RolePoint.</span><span class="sxs-lookup"><span data-stu-id="ae07b-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="ae07b-194">Travailler avec [équipe de support RolePoint](mailto:info@rolepoint.com) tooadd les utilisateurs de hello dans la plateforme de RolePoint hello.</span><span class="sxs-lookup"><span data-stu-id="ae07b-194">Work with [RolePoint support team](mailto:info@rolepoint.com) tooadd hello users in hello RolePoint platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae07b-195">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae07b-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae07b-196">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRolePoint.</span><span class="sxs-lookup"><span data-stu-id="ae07b-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRolePoint.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ae07b-198">**tooassign Britta Simon tooRolePoint, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae07b-198">**tooassign Britta Simon tooRolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae07b-199">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ae07b-201">Dans la liste des applications hello, sélectionnez **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-201">In hello applications list, select **RolePoint**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="ae07b-203">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ae07b-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-205">Click **Add** button.</span></span> <span data-ttu-id="ae07b-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ae07b-208">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ae07b-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae07b-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae07b-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ae07b-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae07b-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ae07b-211">Testing single sign-on</span></span>

<span data-ttu-id="ae07b-212">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ae07b-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ae07b-213">Lorsque vous cliquez sur mosaïque RolePoint hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour RolePoint application.</span><span class="sxs-lookup"><span data-stu-id="ae07b-213">When you click hello RolePoint tile in hello Access Panel, you should get automatically signed-on tooyour RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ae07b-214">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ae07b-214">Additional resources</span></span>

* [<span data-ttu-id="ae07b-215">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae07b-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae07b-216">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ae07b-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

