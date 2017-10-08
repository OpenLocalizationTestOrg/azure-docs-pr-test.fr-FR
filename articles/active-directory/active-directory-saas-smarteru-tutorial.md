---
title: "Didacticiel : Intégration d’Azure Active Directory à SmarterU | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="6e21d-103">Didacticiel : Intégration d’Azure Active Directory à SmarterU</span><span class="sxs-lookup"><span data-stu-id="6e21d-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="6e21d-104">Dans ce didacticiel, vous apprendrez comment toointegrate SmarterU avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e21d-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e21d-105">Intégration de SmarterU à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6e21d-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e21d-106">Vous pouvez contrôler dans Azure AD qui a accès tooSmarterU</span><span class="sxs-lookup"><span data-stu-id="6e21d-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="6e21d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSmarterU (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e21d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="6e21d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6e21d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e21d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e21d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6e21d-110">Prerequisites</span></span>

<span data-ttu-id="6e21d-111">tooconfigure intégration d’Azure AD à SmarterU, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6e21d-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="6e21d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e21d-113">Un abonnement SmarterU pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6e21d-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e21d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6e21d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e21d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="6e21d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e21d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6e21d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e21d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e21d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e21d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6e21d-118">Scenario description</span></span>
<span data-ttu-id="6e21d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6e21d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e21d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="6e21d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e21d-121">Ajout de SmarterU à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6e21d-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="6e21d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="6e21d-123">Ajout de SmarterU à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6e21d-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="6e21d-124">intégration de hello tooconfigure de SmarterU dans Azure AD, vous devez tooadd SmarterU à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6e21d-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e21d-125">**tooadd SmarterU à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6e21d-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e21d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="6e21d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e21d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e21d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6e21d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6e21d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6e21d-133">Dans la zone de recherche de hello, tapez **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-133">In hello search box, type **SmarterU**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="6e21d-135">Dans le volet de résultats hello, sélectionnez **SmarterU**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6e21d-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e21d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e21d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SmarterU, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6e21d-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e21d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SmarterU est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e21d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="6e21d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SmarterU doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="6e21d-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="6e21d-141">Dans SmarterU, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="6e21d-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6e21d-142">tooconfigure et test Azure AD l’authentification unique à SmarterU, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="6e21d-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e21d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6e21d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e21d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e21d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e21d-145">**[Création d’un utilisateur de test de SmarterU](#creating-a-smarteru-test-user)**  -toohave un équivalent de Britta Simon dans SmarterU est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6e21d-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e21d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6e21d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e21d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="6e21d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e21d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e21d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de SmarterU.</span><span class="sxs-lookup"><span data-stu-id="6e21d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="6e21d-150">**tooconfigure Azure AD single sign-on avec SmarterU, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6e21d-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e21d-151">Bonjour portail Azure, sur hello **SmarterU** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6e21d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6e21d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="6e21d-155">Sur hello **SmarterU domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e21d-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="6e21d-157">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="6e21d-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="6e21d-158">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6e21d-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="6e21d-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6e21d-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e21d-162">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour SmarterU en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6e21d-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="6e21d-163">Dans la barre d’outils de hello en haut de hello, cliquez sur **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6e21d-164">![Paramètres de compte](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="6e21d-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="6e21d-165">Sur la page de configuration de compte hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e21d-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6e21d-166">![Autorisation externe](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorisation externe")</span><span class="sxs-lookup"><span data-stu-id="6e21d-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="6e21d-167">a.</span><span class="sxs-lookup"><span data-stu-id="6e21d-167">a.</span></span> <span data-ttu-id="6e21d-168">Sélectionnez **Enable External Authorization**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="6e21d-169">b.</span><span class="sxs-lookup"><span data-stu-id="6e21d-169">b.</span></span> <span data-ttu-id="6e21d-170">Bonjour **contrôle de connexion principale** section, sélectionnez hello **SmarterU** onglet.</span><span class="sxs-lookup"><span data-stu-id="6e21d-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="6e21d-171">c.</span><span class="sxs-lookup"><span data-stu-id="6e21d-171">c.</span></span> <span data-ttu-id="6e21d-172">Bonjour **connexion par défaut de l’utilisateur** section, sélectionnez hello **SmarterU** onglet.</span><span class="sxs-lookup"><span data-stu-id="6e21d-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="6e21d-173">d.</span><span class="sxs-lookup"><span data-stu-id="6e21d-173">d.</span></span> <span data-ttu-id="6e21d-174">Sélectionnez **Enable Okta**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="6e21d-175">e.</span><span class="sxs-lookup"><span data-stu-id="6e21d-175">e.</span></span> <span data-ttu-id="6e21d-176">Copier le contenu du fichier de métadonnées téléchargé hello hello et collez-le à hello **Okta Metadata** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6e21d-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="6e21d-177">f.</span><span class="sxs-lookup"><span data-stu-id="6e21d-177">f.</span></span> <span data-ttu-id="6e21d-178">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6e21d-179">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="6e21d-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6e21d-180">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="6e21d-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6e21d-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e21d-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e21d-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e21d-183">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="6e21d-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6e21d-185">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6e21d-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e21d-186">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="6e21d-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e21d-188">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e21d-190">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="6e21d-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e21d-192">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e21d-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e21d-194">a.</span><span class="sxs-lookup"><span data-stu-id="6e21d-194">a.</span></span> <span data-ttu-id="6e21d-195">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e21d-196">b.</span><span class="sxs-lookup"><span data-stu-id="6e21d-196">b.</span></span> <span data-ttu-id="6e21d-197">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e21d-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e21d-198">c.</span><span class="sxs-lookup"><span data-stu-id="6e21d-198">c.</span></span> <span data-ttu-id="6e21d-199">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e21d-200">d.</span><span class="sxs-lookup"><span data-stu-id="6e21d-200">d.</span></span> <span data-ttu-id="6e21d-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="6e21d-202">Création d’un utilisateur de test SmarterU</span><span class="sxs-lookup"><span data-stu-id="6e21d-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="6e21d-203">tooenable Azure AD les utilisateurs toolog dans tooSmarterU, ils doivent être configurés dans SmarterU.</span><span class="sxs-lookup"><span data-stu-id="6e21d-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="6e21d-204">Pour SmarterU, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="6e21d-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="6e21d-205">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6e21d-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e21d-206">Connectez-vous à tooyour **SmarterU** client.</span><span class="sxs-lookup"><span data-stu-id="6e21d-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="6e21d-207">Accédez trop**utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-207">Go too**Users**.</span></span>

3. <span data-ttu-id="6e21d-208">Dans la section de l’utilisateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e21d-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6e21d-209">![Nouvel utilisateur](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="6e21d-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="6e21d-210">a.</span><span class="sxs-lookup"><span data-stu-id="6e21d-210">a.</span></span> <span data-ttu-id="6e21d-211">Cliquez sur **+User**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-211">Click **+User**.</span></span>
    
    <span data-ttu-id="6e21d-212">b.</span><span class="sxs-lookup"><span data-stu-id="6e21d-212">b.</span></span> <span data-ttu-id="6e21d-213">Hello de type relatives des valeurs d’attribut de compte d’utilisateur hello Azure AD dans hello suivant des zones de texte : **adresse de messagerie principale**, **ID d’employé**, **mot de passe**,  **Vérifiez le mot de passe**, **prénom**, **Surname**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="6e21d-214">c.</span><span class="sxs-lookup"><span data-stu-id="6e21d-214">c.</span></span> <span data-ttu-id="6e21d-215">Cliquez sur **Active**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="6e21d-216">d.</span><span class="sxs-lookup"><span data-stu-id="6e21d-216">d.</span></span> <span data-ttu-id="6e21d-217">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="6e21d-218">Vous pouvez utiliser n’importe quel autre SmarterU utilisateur compte outil de création ou API fournie par SmarterU tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="6e21d-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6e21d-219">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e21d-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6e21d-220">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSmarterU.</span><span class="sxs-lookup"><span data-stu-id="6e21d-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6e21d-222">**tooassign Britta Simon tooSmarterU, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6e21d-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e21d-223">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6e21d-225">Dans la liste des applications hello, sélectionnez **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-225">In hello applications list, select **SmarterU**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="6e21d-227">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6e21d-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-229">Click **Add** button.</span></span> <span data-ttu-id="6e21d-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6e21d-232">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="6e21d-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e21d-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e21d-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6e21d-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e21d-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6e21d-235">Testing single sign-on</span></span>

<span data-ttu-id="6e21d-236">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="6e21d-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="6e21d-237">Lorsque vous cliquez sur mosaïque SmarterU hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour SmarterU application.</span><span class="sxs-lookup"><span data-stu-id="6e21d-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="6e21d-238">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e21d-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="6e21d-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6e21d-239">Additional resources</span></span>

* [<span data-ttu-id="6e21d-240">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e21d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e21d-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6e21d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

