---
title: "Didacticiel : Intégration d’Azure Active Directory à TiViTz | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et TiViTz."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: e915c31d317c4713720a4db07b23764d91f26a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="4fe03-103">Didacticiel : Intégration d’Azure AD avec TiViTz</span><span class="sxs-lookup"><span data-stu-id="4fe03-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="4fe03-104">Dans ce didacticiel, vous apprendrez comment toointegrate TiViTz avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fe03-104">In this tutorial, you learn how toointegrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fe03-105">Intégration TiViTz à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4fe03-105">Integrating TiViTz with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fe03-106">Vous pouvez contrôler dans Azure AD qui a accès tooTiViTz</span><span class="sxs-lookup"><span data-stu-id="4fe03-106">You can control in Azure AD who has access tooTiViTz</span></span>
- <span data-ttu-id="4fe03-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTiViTz (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-107">You can enable your users tooautomatically get signed-on tooTiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fe03-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4fe03-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4fe03-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fe03-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe03-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4fe03-110">Prerequisites</span></span>

<span data-ttu-id="4fe03-111">tooconfigure intégration d’Azure AD avec TiViTz, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4fe03-111">tooconfigure Azure AD integration with TiViTz, you need hello following items:</span></span>

- <span data-ttu-id="4fe03-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fe03-113">Un abonnement TiViTz pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4fe03-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fe03-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4fe03-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fe03-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4fe03-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fe03-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4fe03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fe03-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fe03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fe03-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4fe03-118">Scenario description</span></span>
<span data-ttu-id="4fe03-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4fe03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fe03-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4fe03-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fe03-121">Ajout de TiViTz à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4fe03-121">Adding TiViTz from hello gallery</span></span>
2. <span data-ttu-id="4fe03-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-hello-gallery"></a><span data-ttu-id="4fe03-123">Ajout de TiViTz à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4fe03-123">Adding TiViTz from hello gallery</span></span>
<span data-ttu-id="4fe03-124">intégration de hello tooconfigure de TiViTz dans Azure AD, vous devez tooadd TiViTz à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4fe03-124">tooconfigure hello integration of TiViTz into Azure AD, you need tooadd TiViTz from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fe03-125">**tooadd TiViTz à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4fe03-125">**tooadd TiViTz from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fe03-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4fe03-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fe03-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fe03-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4fe03-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4fe03-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4fe03-133">Dans la zone de recherche de hello, tapez **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-133">In hello search box, type **TiViTz**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_search.png)

5. <span data-ttu-id="4fe03-135">Dans le volet de résultats hello, sélectionnez **TiViTz**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4fe03-135">In hello results panel, select **TiViTz**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fe03-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fe03-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TiViTz avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4fe03-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4fe03-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TiViTz est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fe03-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TiViTz is tooa user in Azure AD.</span></span> <span data-ttu-id="4fe03-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TiViTz doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4fe03-140">In other words, a link relationship between an Azure AD user and hello related user in TiViTz needs toobe established.</span></span>

<span data-ttu-id="4fe03-141">Dans TiViTz, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4fe03-141">In TiViTz, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4fe03-142">tooconfigure et test Azure AD l’authentification unique avec TiViTz, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4fe03-142">tooconfigure and test Azure AD single sign-on with TiViTz, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fe03-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4fe03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fe03-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fe03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fe03-145">**[Création d’un utilisateur de test TiViTz](#creating-a-tivitz-test-user)**  -toohave un équivalent de Britta Simon dans TiViTz est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4fe03-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - toohave a counterpart of Britta Simon in TiViTz that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fe03-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4fe03-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fe03-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4fe03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fe03-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fe03-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application TiViTz.</span><span class="sxs-lookup"><span data-stu-id="4fe03-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="4fe03-150">**tooconfigure Azure AD single sign-on avec TiViTz, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4fe03-150">**tooconfigure Azure AD single sign-on with TiViTz, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fe03-151">Bonjour portail Azure, sur hello **TiViTz** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-151">In hello Azure portal, on hello **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4fe03-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4fe03-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_samlbase.png)

3. <span data-ttu-id="4fe03-155">Sur hello **TiViTz domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fe03-155">On hello **TiViTz Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="4fe03-157">a.</span><span class="sxs-lookup"><span data-stu-id="4fe03-157">a.</span></span> <span data-ttu-id="4fe03-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="4fe03-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="4fe03-159">b.</span><span class="sxs-lookup"><span data-stu-id="4fe03-159">b.</span></span> <span data-ttu-id="4fe03-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="4fe03-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fe03-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4fe03-161">These values are not real.</span></span> <span data-ttu-id="4fe03-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="4fe03-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4fe03-163">Contact [équipe de support Client de TiViTz](mailto:info@tivitz.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4fe03-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) tooget these values.</span></span> 

4. <span data-ttu-id="4fe03-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4fe03-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_certificate.png) 

5. <span data-ttu-id="4fe03-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4fe03-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4fe03-168">tooconfigure l’authentification unique sur **TiViTz** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="4fe03-168">tooconfigure single sign-on on **TiViTz** side, you need toosend hello downloaded **Metadata XML** too[TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="4fe03-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4fe03-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fe03-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4fe03-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fe03-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fe03-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fe03-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fe03-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4fe03-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4fe03-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4fe03-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fe03-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4fe03-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fe03-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fe03-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4fe03-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fe03-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fe03-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fe03-184">a.</span><span class="sxs-lookup"><span data-stu-id="4fe03-184">a.</span></span> <span data-ttu-id="4fe03-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fe03-186">b.</span><span class="sxs-lookup"><span data-stu-id="4fe03-186">b.</span></span> <span data-ttu-id="4fe03-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4fe03-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fe03-188">c.</span><span class="sxs-lookup"><span data-stu-id="4fe03-188">c.</span></span> <span data-ttu-id="4fe03-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4fe03-190">d.</span><span class="sxs-lookup"><span data-stu-id="4fe03-190">d.</span></span> <span data-ttu-id="4fe03-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="4fe03-192">Création d’un utilisateur de test TiViTz</span><span class="sxs-lookup"><span data-stu-id="4fe03-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="4fe03-193">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans TiViTz.</span><span class="sxs-lookup"><span data-stu-id="4fe03-193">hello objective of this section is toocreate a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="4fe03-194">TiViTz prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="4fe03-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4fe03-195">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4fe03-195">There is no action item for you in this section.</span></span> <span data-ttu-id="4fe03-196">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess TiViTz s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="4fe03-196">A new user is created during an attempt tooaccess TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4fe03-197">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact [équipe de support TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="4fe03-197">If you need toocreate an user manually, you need toocontact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4fe03-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe03-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4fe03-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTiViTz.</span><span class="sxs-lookup"><span data-stu-id="4fe03-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTiViTz.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4fe03-201">**tooassign Britta Simon tooTiViTz, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4fe03-201">**tooassign Britta Simon tooTiViTz, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fe03-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4fe03-204">Dans la liste des applications hello, sélectionnez **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-204">In hello applications list, select **TiViTz**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_app.png) 

3. <span data-ttu-id="4fe03-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4fe03-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-208">Click **Add** button.</span></span> <span data-ttu-id="4fe03-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4fe03-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4fe03-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fe03-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fe03-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4fe03-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fe03-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4fe03-214">Testing single sign-on</span></span>

<span data-ttu-id="4fe03-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4fe03-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4fe03-216">Lorsque vous cliquez sur mosaïque TiViTz hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour TiViTz application.</span><span class="sxs-lookup"><span data-stu-id="4fe03-216">When you click hello TiViTz tile in hello Access Panel, you should get automatically signed-on tooyour TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fe03-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4fe03-217">Additional resources</span></span>

* [<span data-ttu-id="4fe03-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fe03-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fe03-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4fe03-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png

