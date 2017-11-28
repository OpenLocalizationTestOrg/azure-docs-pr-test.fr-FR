---
title: "Didacticiel : Intégration d’Azure Active Directory à Convercent | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="d9b39-103">Didacticiel : Intégration d’Azure Active Directory à Convercent</span><span class="sxs-lookup"><span data-stu-id="d9b39-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="d9b39-104">Dans ce didacticiel, vous apprendrez comment toointegrate Convercent avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9b39-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9b39-105">Intégration Convercent à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d9b39-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9b39-106">Vous pouvez contrôler dans Azure AD qui a accès tooConvercent</span><span class="sxs-lookup"><span data-stu-id="d9b39-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="d9b39-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooConvercent (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9b39-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9b39-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9b39-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9b39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9b39-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9b39-110">Prerequisites</span></span>

<span data-ttu-id="d9b39-111">tooconfigure intégration d’Azure AD avec Convercent, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d9b39-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="d9b39-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9b39-113">Un abonnement Convercent pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d9b39-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9b39-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d9b39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9b39-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d9b39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9b39-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d9b39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9b39-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9b39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9b39-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d9b39-118">Scenario description</span></span>
<span data-ttu-id="d9b39-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d9b39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9b39-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d9b39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9b39-121">Ajout de Convercent à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d9b39-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="d9b39-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="d9b39-123">Ajout de Convercent à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d9b39-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="d9b39-124">intégration de hello tooconfigure de Convercent dans Azure AD, vous devez tooadd Convercent à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d9b39-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9b39-125">**tooadd Convercent à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9b39-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b39-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d9b39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9b39-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9b39-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d9b39-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d9b39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d9b39-133">Dans la zone de recherche de hello, tapez **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-133">In hello search box, type **Convercent**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="d9b39-135">Dans le volet de résultats hello, sélectionnez **Convercent**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d9b39-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9b39-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9b39-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Convercent avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d9b39-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9b39-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Convercent est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b39-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="d9b39-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Convercent doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d9b39-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="d9b39-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Convercent.</span><span class="sxs-lookup"><span data-stu-id="d9b39-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="d9b39-142">tooconfigure et test Azure AD l’authentification unique avec Convercent, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d9b39-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9b39-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d9b39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9b39-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9b39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9b39-145">**[Création d’un utilisateur de test Convercent](#creating-a-convercent-test-user)**  -toohave un équivalent de Britta Simon dans Convercent est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9b39-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9b39-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d9b39-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9b39-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d9b39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9b39-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9b39-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Convercent.</span><span class="sxs-lookup"><span data-stu-id="d9b39-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="d9b39-150">**tooconfigure Azure AD single sign-on avec Convercent, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9b39-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b39-151">Bonjour portail Azure, sur hello **Convercent** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d9b39-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d9b39-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="d9b39-155">Sur hello **Convercent domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="d9b39-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="d9b39-157">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="d9b39-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="d9b39-158">Si vous le souhaitez application hello tooconfigure **mode initiée par SP**, sur hello **Convercent domaine et les URL** section effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9b39-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="d9b39-160">a.</span><span class="sxs-lookup"><span data-stu-id="d9b39-160">a.</span></span> <span data-ttu-id="d9b39-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="d9b39-162">b.</span><span class="sxs-lookup"><span data-stu-id="d9b39-162">b.</span></span> <span data-ttu-id="d9b39-163">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="d9b39-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="d9b39-164">c.</span><span class="sxs-lookup"><span data-stu-id="d9b39-164">c.</span></span> <span data-ttu-id="d9b39-165">Bonjour **relais état** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="d9b39-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9b39-166">Ces valeurs ne sont pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="d9b39-166">These values are not hello real values.</span></span> <span data-ttu-id="d9b39-167">Mettre à jour les valeurs de hello réel identificateur, URL de connexion et l’état de relais.</span><span class="sxs-lookup"><span data-stu-id="d9b39-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="d9b39-168">Contact [équipe de support Client de Convercent](http://support.convercent.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d9b39-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="d9b39-169">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d9b39-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="d9b39-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d9b39-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d9b39-173">tooget l’authentification unique configurée pour votre application, contactez [équipe de support Convercent](mailto:support@convercent.com) et fournissez-leur hello téléchargé **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="d9b39-174">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d9b39-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9b39-175">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d9b39-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9b39-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9b39-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9b39-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9b39-178">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d9b39-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d9b39-180">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9b39-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b39-181">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d9b39-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9b39-183">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9b39-185">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d9b39-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9b39-187">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9b39-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9b39-189">a.</span><span class="sxs-lookup"><span data-stu-id="d9b39-189">a.</span></span> <span data-ttu-id="d9b39-190">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9b39-191">b.</span><span class="sxs-lookup"><span data-stu-id="d9b39-191">b.</span></span> <span data-ttu-id="d9b39-192">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9b39-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9b39-193">c.</span><span class="sxs-lookup"><span data-stu-id="d9b39-193">c.</span></span> <span data-ttu-id="d9b39-194">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9b39-195">d.</span><span class="sxs-lookup"><span data-stu-id="d9b39-195">d.</span></span> <span data-ttu-id="d9b39-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="d9b39-197">Création d’un utilisateur de test Convercent</span><span class="sxs-lookup"><span data-stu-id="d9b39-197">Creating a Convercent test user</span></span>

<span data-ttu-id="d9b39-198">Travailler avec [équipe de support Convercent](mailto:support@convercent.com) tooadd les utilisateurs de hello dans la plateforme de Convercent hello.</span><span class="sxs-lookup"><span data-stu-id="d9b39-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9b39-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b39-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9b39-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooConvercent.</span><span class="sxs-lookup"><span data-stu-id="d9b39-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d9b39-202">**tooassign Britta Simon tooConvercent, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9b39-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b39-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d9b39-205">Dans la liste des applications hello, sélectionnez **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-205">In hello applications list, select **Convercent**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="d9b39-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d9b39-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-209">Click **Add** button.</span></span> <span data-ttu-id="d9b39-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d9b39-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d9b39-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9b39-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9b39-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d9b39-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9b39-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d9b39-215">Testing single sign-on</span></span>

<span data-ttu-id="d9b39-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d9b39-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9b39-217">Lorsque vous cliquez sur mosaïque Convercent hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Convercent application.</span><span class="sxs-lookup"><span data-stu-id="d9b39-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="d9b39-218">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9b39-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9b39-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d9b39-219">Additional resources</span></span>

* [<span data-ttu-id="d9b39-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9b39-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9b39-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d9b39-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

