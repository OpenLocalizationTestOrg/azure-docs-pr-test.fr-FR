---
title: "Didacticiel : Intégration d’Azure Active Directory à EverBridge | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="de73b-103">Didacticiel : Intégration d’Azure Active Directory à Everbridge</span><span class="sxs-lookup"><span data-stu-id="de73b-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="de73b-104">Dans ce didacticiel, vous apprendrez comment toointegrate EverBridge avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de73b-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de73b-105">Intégration EverBridge à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="de73b-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de73b-106">Vous pouvez contrôler dans Azure AD qui a accès tooEverBridge</span><span class="sxs-lookup"><span data-stu-id="de73b-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="de73b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEverBridge (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de73b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="de73b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de73b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de73b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de73b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="de73b-110">Prerequisites</span></span>

<span data-ttu-id="de73b-111">tooconfigure intégration d’Azure AD avec EverBridge, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="de73b-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="de73b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de73b-113">Un abonnement EverBridge pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="de73b-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de73b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="de73b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de73b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="de73b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de73b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="de73b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de73b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de73b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de73b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="de73b-118">Scenario description</span></span>
<span data-ttu-id="de73b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="de73b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de73b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="de73b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de73b-121">Ajout de EverBridge à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="de73b-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="de73b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="de73b-123">Ajout de EverBridge à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="de73b-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="de73b-124">intégration de hello tooconfigure de EverBridge dans Azure AD, vous devez tooadd EverBridge à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="de73b-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de73b-125">**tooadd EverBridge à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de73b-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de73b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="de73b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de73b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="de73b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de73b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de73b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="de73b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="de73b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="de73b-133">Dans la zone de recherche de hello, tapez **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="de73b-133">In hello search box, type **EverBridge**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="de73b-135">Dans le volet de résultats hello, sélectionnez **EverBridge**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="de73b-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de73b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de73b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec EverBridge à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="de73b-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de73b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans EverBridge est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de73b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="de73b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans EverBridge doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="de73b-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="de73b-141">Dans EverBridge, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="de73b-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de73b-142">tooconfigure et test Azure AD l’authentification unique avec EverBridge, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="de73b-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de73b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="de73b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de73b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de73b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de73b-145">**[Création d’un utilisateur de test EverBridge](#creating-an-everbridge-test-user)**  -toohave un équivalent de Britta Simon dans EverBridge est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de73b-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de73b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de73b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de73b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="de73b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de73b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de73b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application EverBridge.</span><span class="sxs-lookup"><span data-stu-id="de73b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="de73b-150">**tooconfigure Azure AD single sign-on avec EverBridge, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de73b-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="de73b-151">Bonjour portail Azure, sur hello **EverBridge** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="de73b-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="de73b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de73b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="de73b-155">Sur hello **EverBridge domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="de73b-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="de73b-157">a.</span><span class="sxs-lookup"><span data-stu-id="de73b-157">a.</span></span> <span data-ttu-id="de73b-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="de73b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="de73b-159">b.</span><span class="sxs-lookup"><span data-stu-id="de73b-159">b.</span></span> <span data-ttu-id="de73b-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="de73b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de73b-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="de73b-161">These values are not real.</span></span> <span data-ttu-id="de73b-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="de73b-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="de73b-163">Contact [équipe de support EverBridge](mailto:support@everbridge.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="de73b-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="de73b-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="de73b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="de73b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="de73b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de73b-168">Sur hello **EverBridge Configuration** , cliquez sur **EverBridge de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="de73b-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de73b-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="de73b-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="de73b-171">tooget SSO configuré pour votre application, vous devez locataire de Everbridge toosign sur tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="de73b-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="de73b-172">Dans le menu hello haut de hello, cliquez sur hello **paramètres** onglet et sélectionnez **Single Sign-On** sous **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="de73b-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="de73b-174">a.</span><span class="sxs-lookup"><span data-stu-id="de73b-174">a.</span></span> <span data-ttu-id="de73b-175">Bonjour **nom** zone de texte, nom de fournisseur de l’identificateur hello de type (par exemple : nom de votre société).</span><span class="sxs-lookup"><span data-stu-id="de73b-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="de73b-176">b.</span><span class="sxs-lookup"><span data-stu-id="de73b-176">b.</span></span> <span data-ttu-id="de73b-177">Bonjour **nom de l’API** zone de texte Nom hello du type de l’API.</span><span class="sxs-lookup"><span data-stu-id="de73b-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="de73b-178">c.</span><span class="sxs-lookup"><span data-stu-id="de73b-178">c.</span></span> <span data-ttu-id="de73b-179">Cliquez sur **choisir un fichier** fichier de métadonnées bouton tooupload hello que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de73b-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="de73b-180">d.</span><span class="sxs-lookup"><span data-stu-id="de73b-180">d.</span></span> <span data-ttu-id="de73b-181">Bonjour emplacement d’identité SAML, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="de73b-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="de73b-182">e.</span><span class="sxs-lookup"><span data-stu-id="de73b-182">e.</span></span> <span data-ttu-id="de73b-183">Bonjour **Identity Provider Login URL** zone de texte, valeur de l’URL de l’authentification unique SAML à partir d’Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="de73b-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="de73b-185">f.</span><span class="sxs-lookup"><span data-stu-id="de73b-185">f.</span></span> <span data-ttu-id="de73b-186">Bonjour Service Provider Initiated Request Binding, sélectionnez **redirection HTTP**.</span><span class="sxs-lookup"><span data-stu-id="de73b-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="de73b-187">g.</span><span class="sxs-lookup"><span data-stu-id="de73b-187">g.</span></span> <span data-ttu-id="de73b-188">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="de73b-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="de73b-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="de73b-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de73b-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="de73b-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de73b-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de73b-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de73b-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="de73b-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="de73b-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="de73b-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de73b-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de73b-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="de73b-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de73b-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="de73b-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de73b-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="de73b-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de73b-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="de73b-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de73b-204">a.</span><span class="sxs-lookup"><span data-stu-id="de73b-204">a.</span></span> <span data-ttu-id="de73b-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de73b-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de73b-206">b.</span><span class="sxs-lookup"><span data-stu-id="de73b-206">b.</span></span> <span data-ttu-id="de73b-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="de73b-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de73b-208">c.</span><span class="sxs-lookup"><span data-stu-id="de73b-208">c.</span></span> <span data-ttu-id="de73b-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="de73b-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de73b-210">d.</span><span class="sxs-lookup"><span data-stu-id="de73b-210">d.</span></span> <span data-ttu-id="de73b-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="de73b-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="de73b-212">Création d’un utilisateur de test EverBridge</span><span class="sxs-lookup"><span data-stu-id="de73b-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="de73b-213">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Everbridge.</span><span class="sxs-lookup"><span data-stu-id="de73b-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="de73b-214">Travailler avec [équipe de support EverBridge](mailto:support@everbridge.com) tooadd les utilisateurs de hello dans la plateforme de Everbridge hello.</span><span class="sxs-lookup"><span data-stu-id="de73b-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de73b-215">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="de73b-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de73b-216">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEverBridge.</span><span class="sxs-lookup"><span data-stu-id="de73b-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="de73b-218">**tooassign Britta Simon tooEverBridge, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de73b-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="de73b-219">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de73b-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="de73b-221">Dans la liste des applications hello, sélectionnez **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="de73b-221">In hello applications list, select **EverBridge**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="de73b-223">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="de73b-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="de73b-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de73b-225">Click **Add** button.</span></span> <span data-ttu-id="de73b-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="de73b-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="de73b-228">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="de73b-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de73b-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="de73b-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de73b-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="de73b-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de73b-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="de73b-231">Testing single sign-on</span></span>

<span data-ttu-id="de73b-232">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="de73b-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de73b-233">Lorsque vous cliquez sur mosaïque Everbridge hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Everbridge application.</span><span class="sxs-lookup"><span data-stu-id="de73b-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de73b-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="de73b-234">Additional resources</span></span>

* [<span data-ttu-id="de73b-235">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de73b-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de73b-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="de73b-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

