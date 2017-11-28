---
title: "Tutoriel : Intégration d’Azure Active Directory à ASC Contracts | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les contrats ASC."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 8320af8acfda3e3d37e589c9887cd697d5ab651c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="d9216-103">Tutoriel : Intégration d’Azure Active Directory à ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="d9216-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="d9216-104">Dans ce didacticiel, vous apprendrez comment toointegrate ASC contrats avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9216-104">In this tutorial, you learn how toointegrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9216-105">Intégration des contrats ASC à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d9216-105">Integrating ASC Contracts with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9216-106">Vous pouvez contrôler dans Azure AD qui a accès tooASC contrats</span><span class="sxs-lookup"><span data-stu-id="d9216-106">You can control in Azure AD who has access tooASC Contracts</span></span>
- <span data-ttu-id="d9216-107">Vous pouvez activer votre tooautomatically utilisateurs obtenir tooASC signés sur les contrats (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-107">You can enable your users tooautomatically get signed-on tooASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9216-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9216-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9216-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9216-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9216-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9216-110">Prerequisites</span></span>

<span data-ttu-id="d9216-111">tooconfigure intégration d’Azure AD avec des contrats de ASC, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d9216-111">tooconfigure Azure AD integration with ASC Contracts, you need hello following items:</span></span>

- <span data-ttu-id="d9216-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9216-113">Un abonnement ASC Contracts pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d9216-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9216-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d9216-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9216-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d9216-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9216-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d9216-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9216-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9216-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9216-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d9216-118">Scenario description</span></span>
<span data-ttu-id="d9216-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d9216-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9216-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d9216-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9216-121">Ajout de contrats de ASC à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d9216-121">Adding ASC Contracts from hello gallery</span></span>
2. <span data-ttu-id="d9216-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-hello-gallery"></a><span data-ttu-id="d9216-123">Ajout de contrats de ASC à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d9216-123">Adding ASC Contracts from hello gallery</span></span>
<span data-ttu-id="d9216-124">tooconfigure hello intégration des contrats de ASC dans Azure AD, vous devez tooadd ASC contrats à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d9216-124">tooconfigure hello integration of ASC Contracts into Azure AD, you need tooadd ASC Contracts from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9216-125">**tooadd contrats ASC à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9216-125">**tooadd ASC Contracts from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9216-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d9216-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9216-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d9216-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9216-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d9216-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d9216-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d9216-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d9216-133">Dans la zone de recherche de hello, tapez **ASC contrats**.</span><span class="sxs-lookup"><span data-stu-id="d9216-133">In hello search box, type **ASC Contracts**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="d9216-135">Dans le volet de résultats hello, sélectionnez **ASC contrats**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d9216-135">In hello results panel, select **ASC Contracts**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9216-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9216-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ASC Contracts, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d9216-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9216-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les contrats ASC est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9216-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ASC Contracts is tooa user in Azure AD.</span></span> <span data-ttu-id="d9216-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les contrats ASC hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d9216-140">In other words, a link relationship between an Azure AD user and hello related user in ASC Contracts needs toobe established.</span></span>

<span data-ttu-id="d9216-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans les contrats ASC.</span><span class="sxs-lookup"><span data-stu-id="d9216-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ASC Contracts.</span></span>

<span data-ttu-id="d9216-142">tooconfigure et test Azure AD l’authentification unique avec les contrats ASC, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d9216-142">tooconfigure and test Azure AD single sign-on with ASC Contracts, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9216-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d9216-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9216-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9216-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9216-145">**[Création d’un utilisateur de test ASC contrats](#creating-an-asc-contracts-test-user)**  -toohave un équivalent de Britta Simon dans les contrats ASC est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9216-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - toohave a counterpart of Britta Simon in ASC Contracts that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9216-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d9216-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9216-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d9216-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9216-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9216-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ASC contrats.</span><span class="sxs-lookup"><span data-stu-id="d9216-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="d9216-150">**tooconfigure Azure AD authentification unique avec les contrats ASC, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9216-150">**tooconfigure Azure AD single sign-on with ASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9216-151">Bonjour portail Azure, sur hello **ASC contrats** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d9216-151">In hello Azure portal, on hello **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d9216-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d9216-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="d9216-155">Sur hello **ASC contrats de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9216-155">On hello **ASC Contracts Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="d9216-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9216-157">a.</span></span> <span data-ttu-id="d9216-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="d9216-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="d9216-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9216-159">b.</span></span> <span data-ttu-id="d9216-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="d9216-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9216-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d9216-161">These values are not real.</span></span> <span data-ttu-id="d9216-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="d9216-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d9216-163">Contactez l’équipe ASC réseaux Inc. (ASC) **613.599.6178** tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d9216-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** tooget these values.</span></span>

4. <span data-ttu-id="d9216-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d9216-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="d9216-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d9216-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9216-168">tooconfigure l’authentification unique sur **ASC contrats** côté, appelez le support ASC réseaux Inc. (ASC) à **613.599.6178** et fournissez-leur hello téléchargé **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="d9216-168">tooconfigure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with hello downloaded **Metadata XML**.</span></span> <span data-ttu-id="d9216-169">Ils définir cette application toohave hello connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="d9216-169">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d9216-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d9216-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9216-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d9216-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9216-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9216-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9216-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9216-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d9216-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d9216-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9216-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9216-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d9216-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9216-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d9216-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9216-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d9216-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9216-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9216-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9216-185">a.</span><span class="sxs-lookup"><span data-stu-id="d9216-185">a.</span></span> <span data-ttu-id="d9216-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9216-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9216-187">b.</span><span class="sxs-lookup"><span data-stu-id="d9216-187">b.</span></span> <span data-ttu-id="d9216-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9216-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9216-189">c.</span><span class="sxs-lookup"><span data-stu-id="d9216-189">c.</span></span> <span data-ttu-id="d9216-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d9216-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9216-191">d.</span><span class="sxs-lookup"><span data-stu-id="d9216-191">d.</span></span> <span data-ttu-id="d9216-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9216-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="d9216-193">Création d’un utilisateur de test ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="d9216-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="d9216-194">Travailler avec l’équipe de support ASC réseaux Inc. (ASC) **613.599.6178** tooget hello les utilisateurs dans la plateforme de contrats de ASC hello.</span><span class="sxs-lookup"><span data-stu-id="d9216-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** tooget hello users added in hello ASC Contracts platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9216-195">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9216-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9216-196">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooASC contrats.</span><span class="sxs-lookup"><span data-stu-id="d9216-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooASC Contracts.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d9216-198">**tooassign Britta Simon tooASC contrats, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d9216-198">**tooassign Britta Simon tooASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9216-199">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d9216-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d9216-201">Dans la liste des applications hello, sélectionnez **ASC contrats**.</span><span class="sxs-lookup"><span data-stu-id="d9216-201">In hello applications list, select **ASC Contracts**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="d9216-203">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d9216-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d9216-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d9216-205">Click **Add** button.</span></span> <span data-ttu-id="d9216-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d9216-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d9216-208">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d9216-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9216-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d9216-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9216-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d9216-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9216-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d9216-211">Testing single sign-on</span></span>

<span data-ttu-id="d9216-212">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d9216-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9216-213">Lorsque vous cliquez sur hello ASC contrats vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application des contrats de ASC.</span><span class="sxs-lookup"><span data-stu-id="d9216-213">When you click hello ASC Contracts tile in hello Access Panel, you should get automatically signed-on tooyour ASC Contracts application.</span></span> <span data-ttu-id="d9216-214">Pour plus d’informations sur le volet d’accès, consultez</span><span class="sxs-lookup"><span data-stu-id="d9216-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="d9216-215">[Présentation du volet d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d9216-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9216-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d9216-216">Additional resources</span></span>

* [<span data-ttu-id="d9216-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9216-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9216-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d9216-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

