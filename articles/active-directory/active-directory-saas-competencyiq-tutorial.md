---
title: "Didacticiel : Intégration d’Azure Active Directory à CompetencyIQ | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et CompetencyIQ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: c032884b092da85684e24e98f75371475e09322d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="ee391-103">Didacticiel : Intégration d’Azure Active Directory à CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ee391-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="ee391-104">Dans ce didacticiel, vous apprendrez comment toointegrate CompetencyIQ avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee391-104">In this tutorial, you learn how toointegrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee391-105">Intégration CompetencyIQ à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ee391-105">Integrating CompetencyIQ with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee391-106">Vous pouvez contrôler dans Azure AD qui a accès tooCompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ee391-106">You can control in Azure AD who has access tooCompetencyIQ</span></span>
- <span data-ttu-id="ee391-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCompetencyIQ (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-107">You can enable your users tooautomatically get signed-on tooCompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee391-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ee391-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee391-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee391-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee391-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ee391-110">Prerequisites</span></span>

<span data-ttu-id="ee391-111">tooconfigure intégration d’Azure AD avec CompetencyIQ, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ee391-111">tooconfigure Azure AD integration with CompetencyIQ, you need hello following items:</span></span>

- <span data-ttu-id="ee391-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee391-113">Un abonnement CompetencyIQ pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ee391-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee391-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ee391-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee391-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ee391-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee391-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ee391-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee391-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee391-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee391-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ee391-118">Scenario description</span></span>
<span data-ttu-id="ee391-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ee391-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee391-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ee391-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee391-121">Ajout de CompetencyIQ à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ee391-121">Adding CompetencyIQ from hello gallery</span></span>
2. <span data-ttu-id="ee391-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-hello-gallery"></a><span data-ttu-id="ee391-123">Ajout de CompetencyIQ à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ee391-123">Adding CompetencyIQ from hello gallery</span></span>
<span data-ttu-id="ee391-124">intégration de hello tooconfigure de CompetencyIQ dans Azure AD, vous devez tooadd CompetencyIQ à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ee391-124">tooconfigure hello integration of CompetencyIQ into Azure AD, you need tooadd CompetencyIQ from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee391-125">**tooadd CompetencyIQ à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ee391-125">**tooadd CompetencyIQ from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee391-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ee391-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee391-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ee391-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee391-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ee391-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ee391-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ee391-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ee391-133">Dans la zone de recherche de hello, tapez **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="ee391-133">In hello search box, type **CompetencyIQ**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="ee391-135">Dans le volet de résultats hello, sélectionnez **CompetencyIQ**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ee391-135">In hello results panel, select **CompetencyIQ**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee391-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee391-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec CompetencyIQ avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ee391-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee391-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans CompetencyIQ est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee391-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CompetencyIQ is tooa user in Azure AD.</span></span> <span data-ttu-id="ee391-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans CompetencyIQ doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ee391-140">In other words, a link relationship between an Azure AD user and hello related user in CompetencyIQ needs toobe established.</span></span>

<span data-ttu-id="ee391-141">Dans CompetencyIQ, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ee391-141">In CompetencyIQ, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ee391-142">tooconfigure et test Azure AD l’authentification unique avec CompetencyIQ, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ee391-142">tooconfigure and test Azure AD single sign-on with CompetencyIQ, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee391-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ee391-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee391-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee391-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee391-145">**[Création d’un utilisateur de test CompetencyIQ](#creating-a-competencyiq-test-user)**  -toohave un équivalent de Britta Simon dans CompetencyIQ est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ee391-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - toohave a counterpart of Britta Simon in CompetencyIQ that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee391-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ee391-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee391-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ee391-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee391-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee391-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="ee391-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="ee391-150">**tooconfigure Azure AD single sign-on avec CompetencyIQ, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ee391-150">**tooconfigure Azure AD single sign-on with CompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee391-151">Bonjour portail Azure, sur hello **CompetencyIQ** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ee391-151">In hello Azure portal, on hello **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ee391-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ee391-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="ee391-155">Sur hello **CompetencyIQ domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee391-155">On hello **CompetencyIQ Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="ee391-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee391-157">a.</span></span> <span data-ttu-id="ee391-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="ee391-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="ee391-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee391-159">b.</span></span> <span data-ttu-id="ee391-160">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="ee391-160">In hello **Identifier** textbox, type hello URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee391-161">valeur de l’URL Hello Sign-on n'est pas réel donc mettre à jour ce avec l’URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="ee391-161">hello Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="ee391-162">Contact [équipe de support Client de CompetencyIQ](https://www.competencyiq.com/) tooget cela.</span><span class="sxs-lookup"><span data-stu-id="ee391-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) tooget this.</span></span> 
 
4. <span data-ttu-id="ee391-163">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ee391-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="ee391-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ee391-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee391-167">Sur hello **CompetencyIQ Configuration** , cliquez sur **CompetencyIQ de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ee391-167">On hello **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee391-168">Hello de copie **ID d’entité SAML**, et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ee391-168">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="ee391-170">tooconfigure l’authentification unique sur **CompetencyIQ** côté, vous devez hello toosend téléchargé **Metadata XML**, **ID d’entité SAML** et **SAML Single Sign-On URL du service** trop[équipe de support CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="ee391-170">tooconfigure single sign-on on **CompetencyIQ** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="ee391-171">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="ee391-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ee391-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ee391-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee391-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ee391-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee391-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee391-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee391-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee391-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ee391-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ee391-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ee391-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee391-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ee391-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee391-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ee391-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee391-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ee391-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee391-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee391-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee391-187">a.</span><span class="sxs-lookup"><span data-stu-id="ee391-187">a.</span></span> <span data-ttu-id="ee391-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee391-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee391-189">b.</span><span class="sxs-lookup"><span data-stu-id="ee391-189">b.</span></span> <span data-ttu-id="ee391-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee391-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee391-191">c.</span><span class="sxs-lookup"><span data-stu-id="ee391-191">c.</span></span> <span data-ttu-id="ee391-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ee391-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee391-193">d.</span><span class="sxs-lookup"><span data-stu-id="ee391-193">d.</span></span> <span data-ttu-id="ee391-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ee391-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="ee391-195">Création d’un utilisateur de test CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ee391-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="ee391-196">tooenable Azure AD les utilisateurs toolog dans tooCompetencyIQ, vous devez les configurer dans CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="ee391-196">tooenable Azure AD users toolog in tooCompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="ee391-197">Contact [équipe de support CompetencyIQ](https://www.competencyiq.com/) toocreate des utilisateurs dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ee391-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) toocreate users in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee391-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee391-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee391-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="ee391-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCompetencyIQ.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ee391-201">**tooassign Britta Simon tooCompetencyIQ, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ee391-201">**tooassign Britta Simon tooCompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee391-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ee391-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ee391-204">Dans la liste des applications hello, sélectionnez **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="ee391-204">In hello applications list, select **CompetencyIQ**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="ee391-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ee391-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ee391-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ee391-208">Click **Add** button.</span></span> <span data-ttu-id="ee391-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ee391-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ee391-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ee391-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee391-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ee391-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee391-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ee391-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee391-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ee391-214">Testing single sign-on</span></span>

<span data-ttu-id="ee391-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ee391-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee391-216">Lorsque vous cliquez sur mosaïque CompetencyIQ hello hello volet d’accès, vous devriez obtenir automatiquement connecté dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="ee391-216">When you click hello CompetencyIQ tile in hello Access Panel, you should get automatically logged into hello application.</span></span>
<span data-ttu-id="ee391-217">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee391-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee391-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ee391-218">Additional resources</span></span>

* [<span data-ttu-id="ee391-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee391-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee391-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ee391-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

