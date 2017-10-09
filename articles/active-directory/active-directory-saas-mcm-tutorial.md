---
title: "Didacticiel : Intégration d’Azure Active Directory à MCM | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et MCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 6fbb3c641725bed1e7c73ee78129efb86979839e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="3e98d-103">Didacticiel : Intégration d’Azure Active Directory à MCM</span><span class="sxs-lookup"><span data-stu-id="3e98d-103">Tutorial: Azure Active Directory integration with MCM</span></span>

<span data-ttu-id="3e98d-104">Dans ce didacticiel, vous apprendrez comment toointegrate MCM avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e98d-104">In this tutorial, you learn how toointegrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e98d-105">Intégration MCM à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3e98d-105">Integrating MCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e98d-106">Vous pouvez contrôler dans Azure AD qui a accès tooMCM</span><span class="sxs-lookup"><span data-stu-id="3e98d-106">You can control in Azure AD who has access tooMCM</span></span>
- <span data-ttu-id="3e98d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMCM (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-107">You can enable your users tooautomatically get signed-on tooMCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e98d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3e98d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3e98d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e98d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e98d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3e98d-110">Prerequisites</span></span>

<span data-ttu-id="3e98d-111">tooconfigure intégration d’Azure AD avec MCM, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3e98d-111">tooconfigure Azure AD integration with MCM, you need hello following items:</span></span>

- <span data-ttu-id="3e98d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e98d-113">Un abonnement MCM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3e98d-113">A MCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e98d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3e98d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e98d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="3e98d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e98d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3e98d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e98d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e98d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e98d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3e98d-118">Scenario description</span></span>
<span data-ttu-id="3e98d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3e98d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e98d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="3e98d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e98d-121">Ajout de MCM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3e98d-121">Adding MCM from hello gallery</span></span>
2. <span data-ttu-id="3e98d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-hello-gallery"></a><span data-ttu-id="3e98d-123">Ajout de MCM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3e98d-123">Adding MCM from hello gallery</span></span>
<span data-ttu-id="3e98d-124">tooconfigure hello intégration de MCM dans Azure AD, vous devez tooadd MCM à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3e98d-124">tooconfigure hello integration of MCM into Azure AD, you need tooadd MCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e98d-125">**tooadd MCM à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3e98d-125">**tooadd MCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e98d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3e98d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e98d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e98d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3e98d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3e98d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3e98d-133">Dans la zone de recherche de hello, tapez **MCM**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-133">In hello search box, type **MCM**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_search.png)

5. <span data-ttu-id="3e98d-135">Dans le volet de résultats hello, sélectionnez **MCM**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e98d-135">In hello results panel, select **MCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e98d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e98d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MCM, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3e98d-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e98d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello MCM est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e98d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MCM is tooa user in Azure AD.</span></span> <span data-ttu-id="3e98d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans MCM doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="3e98d-140">In other words, a link relationship between an Azure AD user and hello related user in MCM needs toobe established.</span></span>

<span data-ttu-id="3e98d-141">Dans MCM, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="3e98d-141">In MCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3e98d-142">tooconfigure et test Azure AD l’authentification unique avec MCM, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="3e98d-142">tooconfigure and test Azure AD single sign-on with MCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e98d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3e98d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e98d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e98d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e98d-145">**[Création d’un MCM utilisateur de test](#creating-a-mcm-test-user)**  -toohave un équivalent de Britta Simon dans MCM est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3e98d-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - toohave a counterpart of Britta Simon in MCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e98d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3e98d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e98d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="3e98d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e98d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e98d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application MCM.</span><span class="sxs-lookup"><span data-stu-id="3e98d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="3e98d-150">**tooconfigure Azure AD single sign-on avec MCM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3e98d-150">**tooconfigure Azure AD single sign-on with MCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e98d-151">Bonjour portail Azure, sur hello **MCM** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-151">In hello Azure portal, on hello **MCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3e98d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3e98d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_samlbase.png)

3. <span data-ttu-id="3e98d-155">Sur hello **MCM domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e98d-155">On hello **MCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_url.png)

    <span data-ttu-id="3e98d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e98d-157">a.</span></span> <span data-ttu-id="3e98d-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://myaba.co.uk/client-access/<companyname>/saml.php`</span><span class="sxs-lookup"><span data-stu-id="3e98d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span></span>

    <span data-ttu-id="3e98d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e98d-159">b.</span></span> <span data-ttu-id="3e98d-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://myaba.co.uk/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3e98d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://myaba.co.uk/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e98d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3e98d-161">These values are not real.</span></span> <span data-ttu-id="3e98d-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="3e98d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3e98d-163">Contact [équipe de support MCM Client](http://mcmtechnology.com/support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3e98d-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="3e98d-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3e98d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_certificate.png) 

5. <span data-ttu-id="3e98d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3e98d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mcm-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="3e98d-168">tooconfigure l’authentification unique sur **MCM** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique MCM](http://mcmtechnology.com/support/).</span><span class="sxs-lookup"><span data-stu-id="3e98d-168">tooconfigure single sign-on on **MCM** side, you need toosend hello downloaded **Metadata XML** too[MCM support team](http://mcmtechnology.com/support/).</span></span> <span data-ttu-id="3e98d-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="3e98d-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3e98d-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="3e98d-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e98d-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="3e98d-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e98d-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e98d-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e98d-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e98d-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="3e98d-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3e98d-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3e98d-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e98d-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3e98d-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e98d-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e98d-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="3e98d-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e98d-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e98d-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e98d-185">a.</span><span class="sxs-lookup"><span data-stu-id="3e98d-185">a.</span></span> <span data-ttu-id="3e98d-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e98d-187">b.</span><span class="sxs-lookup"><span data-stu-id="3e98d-187">b.</span></span> <span data-ttu-id="3e98d-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e98d-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e98d-189">c.</span><span class="sxs-lookup"><span data-stu-id="3e98d-189">c.</span></span> <span data-ttu-id="3e98d-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e98d-191">d.</span><span class="sxs-lookup"><span data-stu-id="3e98d-191">d.</span></span> <span data-ttu-id="3e98d-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-192">Click **Create**.</span></span>
 
### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="3e98d-193">Création d’un utilisateur de test MCM</span><span class="sxs-lookup"><span data-stu-id="3e98d-193">Creating a MCM test user</span></span>

<span data-ttu-id="3e98d-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans MCM.</span><span class="sxs-lookup"><span data-stu-id="3e98d-194">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="3e98d-195">Travailler avec [équipe de support technique MCM](http://mcmtechnology.com/support/) tooadd les utilisateurs de hello dans la plateforme MCM hello.</span><span class="sxs-lookup"><span data-stu-id="3e98d-195">Work with [MCM support team](http://mcmtechnology.com/support/) tooadd hello users in hello MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="3e98d-196">Vous pouvez utiliser n’importe quel autre MCM utilisateur compte outil de création ou API fournie par MCM tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="3e98d-196">You can use any other MCM user account creation tools or APIs provided by MCM tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e98d-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e98d-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e98d-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMCM.</span><span class="sxs-lookup"><span data-stu-id="3e98d-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMCM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3e98d-200">**tooassign Britta Simon tooMCM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3e98d-200">**tooassign Britta Simon tooMCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e98d-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3e98d-203">Dans la liste des applications hello, sélectionnez **MCM**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-203">In hello applications list, select **MCM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_app.png) 

3. <span data-ttu-id="3e98d-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3e98d-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-207">Click **Add** button.</span></span> <span data-ttu-id="3e98d-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3e98d-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="3e98d-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e98d-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e98d-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3e98d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e98d-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3e98d-213">Testing single sign-on</span></span>

<span data-ttu-id="3e98d-214">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="3e98d-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e98d-215">Lorsque vous cliquez sur hello MCM vignette Bonjour volet d’accès, vous devez obtenir l’application de MCM tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="3e98d-215">When you click hello MCM tile in hello Access Panel, you should get automatically signed-on tooyour MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e98d-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3e98d-216">Additional resources</span></span>

* [<span data-ttu-id="3e98d-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e98d-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e98d-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3e98d-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_203.png

