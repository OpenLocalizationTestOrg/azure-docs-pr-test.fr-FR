---
title: "Didacticiel : Intégration d’Azure Active Directory à Heroku | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="441ac-103">Didacticiel : Intégration d’Azure Active Directory à Heroku</span><span class="sxs-lookup"><span data-stu-id="441ac-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="441ac-104">Dans ce didacticiel, vous apprendrez comment toointegrate Heroku avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="441ac-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="441ac-105">Intégration Heroku à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="441ac-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="441ac-106">Vous pouvez contrôler dans Azure AD qui a accès tooHeroku</span><span class="sxs-lookup"><span data-stu-id="441ac-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="441ac-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHeroku (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="441ac-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="441ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="441ac-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="441ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="441ac-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="441ac-110">Prerequisites</span></span>

<span data-ttu-id="441ac-111">tooconfigure intégration d’Azure AD avec Heroku, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="441ac-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="441ac-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="441ac-113">Un abonnement Heroku pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="441ac-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="441ac-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="441ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="441ac-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="441ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="441ac-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="441ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="441ac-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="441ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="441ac-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="441ac-118">Scenario description</span></span>
<span data-ttu-id="441ac-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="441ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="441ac-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="441ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="441ac-121">Ajout de Heroku à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="441ac-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="441ac-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="441ac-123">Ajout de Heroku à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="441ac-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="441ac-124">intégration de hello tooconfigure de Heroku dans Azure AD, vous devez tooadd Heroku à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="441ac-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="441ac-125">**tooadd Heroku à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="441ac-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="441ac-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="441ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="441ac-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="441ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="441ac-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="441ac-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="441ac-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="441ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="441ac-133">Dans la zone de recherche de hello, tapez **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="441ac-133">In hello search box, type **Heroku**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="441ac-135">Dans le volet de résultats hello, sélectionnez **Heroku**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="441ac-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="441ac-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="441ac-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Heroku avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="441ac-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="441ac-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Heroku est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="441ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="441ac-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Heroku doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="441ac-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="441ac-141">Dans Heroku, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="441ac-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="441ac-142">tooconfigure et test Azure AD l’authentification unique avec Heroku, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="441ac-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="441ac-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="441ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="441ac-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="441ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="441ac-145">**[Création d’un utilisateur de test Heroku](#creating-a-heroku-test-user)**  -toohave un équivalent de Britta Simon dans Heroku est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="441ac-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="441ac-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="441ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="441ac-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="441ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="441ac-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="441ac-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Heroku.</span><span class="sxs-lookup"><span data-stu-id="441ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="441ac-150">**tooconfigure Azure AD single sign-on avec Heroku, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="441ac-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="441ac-151">Bonjour portail Azure, sur hello **Heroku** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="441ac-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="441ac-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="441ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="441ac-155">Sur hello **Heroku domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="441ac-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="441ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="441ac-157">a.</span></span> <span data-ttu-id="441ac-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="441ac-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="441ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="441ac-159">b.</span></span> <span data-ttu-id="441ac-160">Bonjour **URL d’identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="441ac-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="441ac-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="441ac-161">These values are not real.</span></span> <span data-ttu-id="441ac-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="441ac-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="441ac-163">C’est l’équipe Heroku qui vous fournit ces valeurs (comme décrit dans les sections suivantes de cet article).</span><span class="sxs-lookup"><span data-stu-id="441ac-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="441ac-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="441ac-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="441ac-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="441ac-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="441ac-168">tooenable SSO dans Heroku, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="441ac-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="441ac-169">a.</span><span class="sxs-lookup"><span data-stu-id="441ac-169">a.</span></span> <span data-ttu-id="441ac-170">Ouvrez une session dans toohello Heroku compte en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="441ac-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="441ac-171">b.</span><span class="sxs-lookup"><span data-stu-id="441ac-171">b.</span></span> <span data-ttu-id="441ac-172">Cliquez sur hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="441ac-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="441ac-173">c.</span><span class="sxs-lookup"><span data-stu-id="441ac-173">c.</span></span> <span data-ttu-id="441ac-174">Sur hello **l’authentification unique sur la Page**, cliquez sur **télécharger les métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="441ac-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="441ac-175">d.</span><span class="sxs-lookup"><span data-stu-id="441ac-175">d.</span></span> <span data-ttu-id="441ac-176">Téléchargez le fichier de métadonnées hello, qui vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="441ac-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="441ac-177">e.</span><span class="sxs-lookup"><span data-stu-id="441ac-177">e.</span></span> <span data-ttu-id="441ac-178">Lorsque le programme d’installation hello est réussie, les administrateurs voient une boîte de dialogue de confirmation et URL hello Hello connexion de l’authentification unique pour les utilisateurs finaux s’affiche.</span><span class="sxs-lookup"><span data-stu-id="441ac-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="441ac-179">f.</span><span class="sxs-lookup"><span data-stu-id="441ac-179">f.</span></span> <span data-ttu-id="441ac-180">Hello de copie **URL de connexion Heroku** et **ID d’entité Heroku** valeurs et que vous y revenez trop**Heroku domaine et les URL** section dans le portail Azure et coller ces valeurs hello **Url de connexion** et **identificateur** zones de texte respectivement.</span><span class="sxs-lookup"><span data-stu-id="441ac-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="441ac-182">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="441ac-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="441ac-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="441ac-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="441ac-184">Après l’ajout de cette application à partir de hello **des Applications d’entreprise Active Directory** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="441ac-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="441ac-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="441ac-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="441ac-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="441ac-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="441ac-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="441ac-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="441ac-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="441ac-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="441ac-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="441ac-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="441ac-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="441ac-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="441ac-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="441ac-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="441ac-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="441ac-198">a.</span><span class="sxs-lookup"><span data-stu-id="441ac-198">a.</span></span> <span data-ttu-id="441ac-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="441ac-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="441ac-200">b.</span><span class="sxs-lookup"><span data-stu-id="441ac-200">b.</span></span> <span data-ttu-id="441ac-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="441ac-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="441ac-202">c.</span><span class="sxs-lookup"><span data-stu-id="441ac-202">c.</span></span> <span data-ttu-id="441ac-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="441ac-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="441ac-204">d.</span><span class="sxs-lookup"><span data-stu-id="441ac-204">d.</span></span> <span data-ttu-id="441ac-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="441ac-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="441ac-206">Création d’un utilisateur de test Heroku</span><span class="sxs-lookup"><span data-stu-id="441ac-206">Creating a Heroku test user</span></span>

<span data-ttu-id="441ac-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Heroku.</span><span class="sxs-lookup"><span data-stu-id="441ac-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="441ac-208">Heroku prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="441ac-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="441ac-209">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="441ac-209">There is no action item for you in this section.</span></span> <span data-ttu-id="441ac-210">Un nouvel utilisateur est créé lors de l’accès Heroku si l’utilisateur de hello n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="441ac-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="441ac-211">Une fois que le compte hello est configuré, hello utilisateur reçoit un message électronique de vérification et doit lier des accusés de réception tooclick hello.</span><span class="sxs-lookup"><span data-stu-id="441ac-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="441ac-212">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Client de Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="441ac-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="441ac-213">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="441ac-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="441ac-214">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHeroku.</span><span class="sxs-lookup"><span data-stu-id="441ac-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="441ac-216">**tooassign Britta Simon tooHeroku, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="441ac-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="441ac-217">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="441ac-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="441ac-219">Dans la liste des applications hello, sélectionnez **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="441ac-219">In hello applications list, select **Heroku**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="441ac-221">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="441ac-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="441ac-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="441ac-223">Click **Add** button.</span></span> <span data-ttu-id="441ac-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="441ac-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="441ac-226">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="441ac-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="441ac-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="441ac-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="441ac-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="441ac-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="441ac-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="441ac-229">Testing single sign-on</span></span>

<span data-ttu-id="441ac-230">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="441ac-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="441ac-231">Lorsque vous cliquez sur mosaïque Heroku hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Heroku application.</span><span class="sxs-lookup"><span data-stu-id="441ac-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="441ac-232">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="441ac-232">Additional resources</span></span>

* [<span data-ttu-id="441ac-233">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="441ac-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="441ac-234">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="441ac-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
