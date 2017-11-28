---
title: "Didacticiel : Intégration d’Azure Active Directory à Degreed | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Degreed."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eda2d1c-b5e2-4c53-ad46-bbeb91cd119a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: decb553a6c5fa253ddf16b0f03336ab9366a8b4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-degreed"></a><span data-ttu-id="20e7d-103">Didacticiel : Intégration d’Azure AD à Degreed</span><span class="sxs-lookup"><span data-stu-id="20e7d-103">Tutorial: Azure Active Directory integration with Degreed</span></span>

<span data-ttu-id="20e7d-104">Dans ce didacticiel, vous apprendrez comment toointegrate Degreed avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20e7d-104">In this tutorial, you learn how toointegrate Degreed with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20e7d-105">Intégration Degreed à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="20e7d-105">Integrating Degreed with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="20e7d-106">Vous pouvez contrôler dans Azure AD qui a accès tooDegreed</span><span class="sxs-lookup"><span data-stu-id="20e7d-106">You can control in Azure AD who has access tooDegreed</span></span>
- <span data-ttu-id="20e7d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDegreed (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-107">You can enable your users tooautomatically get signed-on tooDegreed (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20e7d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="20e7d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="20e7d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20e7d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20e7d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="20e7d-110">Prerequisites</span></span>

<span data-ttu-id="20e7d-111">tooconfigure intégration d’Azure AD avec Degreed, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="20e7d-111">tooconfigure Azure AD integration with Degreed, you need hello following items:</span></span>

- <span data-ttu-id="20e7d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20e7d-113">Un abonnement Degreed pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="20e7d-113">A Degreed single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20e7d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="20e7d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20e7d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="20e7d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20e7d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="20e7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20e7d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20e7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20e7d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="20e7d-118">Scenario description</span></span>
<span data-ttu-id="20e7d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="20e7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20e7d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="20e7d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20e7d-121">Ajout de Degreed à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="20e7d-121">Adding Degreed from hello gallery</span></span>
2. <span data-ttu-id="20e7d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-degreed-from-hello-gallery"></a><span data-ttu-id="20e7d-123">Ajout de Degreed à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="20e7d-123">Adding Degreed from hello gallery</span></span>
<span data-ttu-id="20e7d-124">intégration de hello tooconfigure de Degreed dans Azure AD, vous devez tooadd Degreed à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="20e7d-124">tooconfigure hello integration of Degreed into Azure AD, you need tooadd Degreed from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="20e7d-125">**tooadd Degreed à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20e7d-125">**tooadd Degreed from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e7d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="20e7d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="20e7d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="20e7d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="20e7d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="20e7d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="20e7d-133">Dans la zone de recherche de hello, tapez **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-133">In hello search box, type **Degreed**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_search.png)

5. <span data-ttu-id="20e7d-135">Dans le volet de résultats hello, sélectionnez **Degreed**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="20e7d-135">In hello results panel, select **Degreed**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20e7d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20e7d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Degreed, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="20e7d-138">In this section, you configure and test Azure AD single sign-on with Degreed based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="20e7d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Degreed est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20e7d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Degreed is tooa user in Azure AD.</span></span> <span data-ttu-id="20e7d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Degreed doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="20e7d-140">In other words, a link relationship between an Azure AD user and hello related user in Degreed needs toobe established.</span></span>

<span data-ttu-id="20e7d-141">Dans Degreed, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="20e7d-141">In Degreed, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="20e7d-142">tooconfigure et test Azure AD l’authentification unique avec Degreed, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="20e7d-142">tooconfigure and test Azure AD single sign-on with Degreed, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="20e7d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="20e7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="20e7d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="20e7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20e7d-145">**[Création d’un utilisateur test Degreed](#creating-a-degreed-test-user)**  -toohave un équivalent de Britta Simon dans Degreed est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20e7d-145">**[Creating a Degreed test user](#creating-a-degreed-test-user)** - toohave a counterpart of Britta Simon in Degreed that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="20e7d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="20e7d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20e7d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="20e7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20e7d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20e7d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Degreed.</span><span class="sxs-lookup"><span data-stu-id="20e7d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Degreed application.</span></span>

<span data-ttu-id="20e7d-150">**tooconfigure Azure AD single sign-on avec Degreed, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20e7d-150">**tooconfigure Azure AD single sign-on with Degreed, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e7d-151">Bonjour portail Azure, sur hello **Degreed** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-151">In hello Azure portal, on hello **Degreed** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="20e7d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="20e7d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_samlbase.png)

3. <span data-ttu-id="20e7d-155">Sur hello **Degreed de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="20e7d-155">On hello **Degreed Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_url.png)

    <span data-ttu-id="20e7d-157">a.</span><span class="sxs-lookup"><span data-stu-id="20e7d-157">a.</span></span> <span data-ttu-id="20e7d-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://degreed.com/?orgsso=<company code>`</span><span class="sxs-lookup"><span data-stu-id="20e7d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://degreed.com/?orgsso=<company code>`</span></span>

    <span data-ttu-id="20e7d-159">b.</span><span class="sxs-lookup"><span data-stu-id="20e7d-159">b.</span></span> <span data-ttu-id="20e7d-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://degreed.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="20e7d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://degreed.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20e7d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="20e7d-161">These values are not real.</span></span> <span data-ttu-id="20e7d-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="20e7d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="20e7d-163">Contact [équipe de support Client Degreed](mailTo:admin@degreed.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="20e7d-163">Contact [Degreed Client support team](mailTo:admin@degreed.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="20e7d-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="20e7d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_certificate.png) 

5. <span data-ttu-id="20e7d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="20e7d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20e7d-168">tooconfigure l’authentification unique sur **Degreed** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="20e7d-168">tooconfigure single sign-on on **Degreed** side, you need toosend hello downloaded **Metadata XML** too[Degreed support team](mailTo:admin@degreed.com).</span></span> <span data-ttu-id="20e7d-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="20e7d-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="20e7d-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="20e7d-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="20e7d-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="20e7d-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="20e7d-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20e7d-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20e7d-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="20e7d-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="20e7d-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="20e7d-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20e7d-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e7d-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="20e7d-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20e7d-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20e7d-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="20e7d-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20e7d-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="20e7d-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20e7d-185">a.</span><span class="sxs-lookup"><span data-stu-id="20e7d-185">a.</span></span> <span data-ttu-id="20e7d-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20e7d-187">b.</span><span class="sxs-lookup"><span data-stu-id="20e7d-187">b.</span></span> <span data-ttu-id="20e7d-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="20e7d-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20e7d-189">c.</span><span class="sxs-lookup"><span data-stu-id="20e7d-189">c.</span></span> <span data-ttu-id="20e7d-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="20e7d-191">d.</span><span class="sxs-lookup"><span data-stu-id="20e7d-191">d.</span></span> <span data-ttu-id="20e7d-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-192">Click **Create**.</span></span>
 
### <a name="creating-a-degreed-test-user"></a><span data-ttu-id="20e7d-193">Création d’un utilisateur de test Degreed</span><span class="sxs-lookup"><span data-stu-id="20e7d-193">Creating a Degreed test user</span></span>

<span data-ttu-id="20e7d-194">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Degreed.</span><span class="sxs-lookup"><span data-stu-id="20e7d-194">hello objective of this section is toocreate a user called Britta Simon in Degreed.</span></span> <span data-ttu-id="20e7d-195">Degreed prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="20e7d-195">Degreed supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="20e7d-196">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="20e7d-196">There is no action item for you in this section.</span></span> <span data-ttu-id="20e7d-197">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Degreed s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="20e7d-197">A new user is created during an attempt tooaccess Degreed if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="20e7d-198">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="20e7d-198">If you need toocreate a user manually, you need toocontact hello [Degreed support team](mailTo:admin@degreed.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="20e7d-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e7d-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="20e7d-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDegreed.</span><span class="sxs-lookup"><span data-stu-id="20e7d-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDegreed.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="20e7d-202">**tooassign Britta Simon tooDegreed, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20e7d-202">**tooassign Britta Simon tooDegreed, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e7d-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="20e7d-205">Dans la liste des applications hello, sélectionnez **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-205">In hello applications list, select **Degreed**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_app.png) 

3. <span data-ttu-id="20e7d-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="20e7d-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-209">Click **Add** button.</span></span> <span data-ttu-id="20e7d-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="20e7d-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="20e7d-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="20e7d-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20e7d-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="20e7d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20e7d-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="20e7d-215">Testing single sign-on</span></span>

<span data-ttu-id="20e7d-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="20e7d-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="20e7d-217">Lorsque vous cliquez sur la vignette de Degreed hello dans hello volet d’accès, vous devez obtenir les applications Degreed tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="20e7d-217">When you click hello Degreed tile in hello Access Panel, you should get automatically signed-on tooyour Degreed application.</span></span>
<span data-ttu-id="20e7d-218">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="20e7d-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="20e7d-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="20e7d-219">Additional resources</span></span>

* [<span data-ttu-id="20e7d-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20e7d-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20e7d-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="20e7d-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_203.png
