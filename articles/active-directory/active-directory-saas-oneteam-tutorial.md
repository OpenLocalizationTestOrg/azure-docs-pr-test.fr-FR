---
title: "Didacticiel : Intégration d’Azure Active Directory à Oneteam | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 7964aaaf9b9570d460f28d86de34b5e87693ba93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="34f3f-103">Didacticiel : Intégration d’Azure Active Directory à Oneteam</span><span class="sxs-lookup"><span data-stu-id="34f3f-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="34f3f-104">Dans ce didacticiel, vous apprendrez comment toointegrate Oneteam avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34f3f-104">In this tutorial, you learn how toointegrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34f3f-105">Intégration Oneteam à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="34f3f-105">Integrating Oneteam with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34f3f-106">Vous pouvez contrôler dans Azure AD qui a accès tooOneteam</span><span class="sxs-lookup"><span data-stu-id="34f3f-106">You can control in Azure AD who has access tooOneteam</span></span>
- <span data-ttu-id="34f3f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOneteam (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-107">You can enable your users tooautomatically get signed-on tooOneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34f3f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="34f3f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34f3f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34f3f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34f3f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="34f3f-110">Prerequisites</span></span>

<span data-ttu-id="34f3f-111">tooconfigure intégration d’Azure AD avec Oneteam, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="34f3f-111">tooconfigure Azure AD integration with Oneteam, you need hello following items:</span></span>

- <span data-ttu-id="34f3f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34f3f-113">Un abonnement Oneteam pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="34f3f-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34f3f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="34f3f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34f3f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="34f3f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34f3f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="34f3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34f3f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34f3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34f3f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="34f3f-118">Scenario description</span></span>
<span data-ttu-id="34f3f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="34f3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34f3f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="34f3f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34f3f-121">Ajout de Oneteam à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="34f3f-121">Adding Oneteam from hello gallery</span></span>
2. <span data-ttu-id="34f3f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-hello-gallery"></a><span data-ttu-id="34f3f-123">Ajout de Oneteam à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="34f3f-123">Adding Oneteam from hello gallery</span></span>
<span data-ttu-id="34f3f-124">intégration de hello tooconfigure de Oneteam dans Azure AD, vous devez tooadd Oneteam à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="34f3f-124">tooconfigure hello integration of Oneteam into Azure AD, you need tooadd Oneteam from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34f3f-125">**tooadd Oneteam à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34f3f-125">**tooadd Oneteam from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f3f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="34f3f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34f3f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34f3f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="34f3f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="34f3f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="34f3f-133">Dans la zone de recherche de hello, tapez **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-133">In hello search box, type **Oneteam**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="34f3f-135">Dans le volet de résultats hello, sélectionnez **Oneteam**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="34f3f-135">In hello results panel, select **Oneteam**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34f3f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34f3f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Oneteam avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="34f3f-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34f3f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Oneteam est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34f3f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Oneteam is tooa user in Azure AD.</span></span> <span data-ttu-id="34f3f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Oneteam doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="34f3f-140">In other words, a link relationship between an Azure AD user and hello related user in Oneteam needs toobe established.</span></span>

<span data-ttu-id="34f3f-141">Dans Oneteam, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="34f3f-141">In Oneteam, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34f3f-142">tooconfigure et test Azure AD l’authentification unique avec Oneteam, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="34f3f-142">tooconfigure and test Azure AD single sign-on with Oneteam, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34f3f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="34f3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34f3f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34f3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34f3f-145">**[Création d’un utilisateur de test Oneteam](#creating-a-oneteam-test-user)**  -toohave un équivalent de Britta Simon dans Oneteam est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34f3f-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - toohave a counterpart of Britta Simon in Oneteam that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34f3f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="34f3f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34f3f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="34f3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34f3f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34f3f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Oneteam.</span><span class="sxs-lookup"><span data-stu-id="34f3f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="34f3f-150">**tooconfigure Azure AD single sign-on avec Oneteam, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34f3f-150">**tooconfigure Azure AD single sign-on with Oneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f3f-151">Bonjour portail Azure, sur hello **Oneteam** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-151">In hello Azure portal, on hello **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="34f3f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="34f3f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="34f3f-155">Sur hello **Oneteam domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="34f3f-155">On hello **Oneteam Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="34f3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="34f3f-157">a.</span></span> <span data-ttu-id="34f3f-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="34f3f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="34f3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="34f3f-159">b.</span></span> <span data-ttu-id="34f3f-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="34f3f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="34f3f-161">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="34f3f-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="34f3f-163">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="34f3f-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="34f3f-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="34f3f-164">These values are not real.</span></span> <span data-ttu-id="34f3f-165">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="34f3f-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="34f3f-166">Contact [équipe de support Client de Oneteam](https://support.one-team.com/hc/requests/new) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="34f3f-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) tooget these values.</span></span> 



5. <span data-ttu-id="34f3f-167">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="34f3f-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="34f3f-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="34f3f-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="34f3f-171">tooget SSO configuré pour votre application, vous pouvez déclencher un ticket de support hello avec [équipe de support Oneteam](https://support.one-team.com/hc/requests/new) et nommez-les hello téléchargé **métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-171">tooget SSO configured for your application, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them hello downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="34f3f-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="34f3f-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34f3f-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="34f3f-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34f3f-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34f3f-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34f3f-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="34f3f-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="34f3f-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="34f3f-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34f3f-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f3f-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="34f3f-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34f3f-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34f3f-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="34f3f-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34f3f-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="34f3f-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34f3f-187">a.</span><span class="sxs-lookup"><span data-stu-id="34f3f-187">a.</span></span> <span data-ttu-id="34f3f-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34f3f-189">b.</span><span class="sxs-lookup"><span data-stu-id="34f3f-189">b.</span></span> <span data-ttu-id="34f3f-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34f3f-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34f3f-191">c.</span><span class="sxs-lookup"><span data-stu-id="34f3f-191">c.</span></span> <span data-ttu-id="34f3f-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34f3f-193">d.</span><span class="sxs-lookup"><span data-stu-id="34f3f-193">d.</span></span> <span data-ttu-id="34f3f-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="34f3f-195">Création d’un utilisateur de test Oneteam</span><span class="sxs-lookup"><span data-stu-id="34f3f-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="34f3f-196">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Oneteam.</span><span class="sxs-lookup"><span data-stu-id="34f3f-196">hello objective of this section is toocreate a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="34f3f-197">Oneteam prend en charge l’approvisionnement de type just-in-time (juste à temps) qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="34f3f-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="34f3f-198">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="34f3f-198">There is no action item for you in this section.</span></span> <span data-ttu-id="34f3f-199">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Oneteam, s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="34f3f-199">A new user will be created during an attempt tooaccess Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="34f3f-200">Si vous devez manuellement toocreate un utilisateur, vous pouvez augmenter le ticket de support hello avec [équipe de support Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="34f3f-200">If you need toocreate an user manually, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34f3f-201">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f3f-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34f3f-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOneteam.</span><span class="sxs-lookup"><span data-stu-id="34f3f-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOneteam.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="34f3f-204">**tooassign Britta Simon tooOneteam, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34f3f-204">**tooassign Britta Simon tooOneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f3f-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="34f3f-207">Dans la liste des applications hello, sélectionnez **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-207">In hello applications list, select **Oneteam**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="34f3f-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="34f3f-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-211">Click **Add** button.</span></span> <span data-ttu-id="34f3f-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="34f3f-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="34f3f-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34f3f-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34f3f-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="34f3f-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34f3f-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="34f3f-217">Testing single sign-on</span></span>

<span data-ttu-id="34f3f-218">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="34f3f-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="34f3f-219">Lorsque vous cliquez sur mosaïque Oneteam hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Oneteam application.</span><span class="sxs-lookup"><span data-stu-id="34f3f-219">When you click hello Oneteam tile in hello Access Panel, you should get automatically signed-on tooyour Oneteam application.</span></span>
<span data-ttu-id="34f3f-220">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34f3f-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="34f3f-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="34f3f-221">Additional resources</span></span>

* [<span data-ttu-id="34f3f-222">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34f3f-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34f3f-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="34f3f-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

