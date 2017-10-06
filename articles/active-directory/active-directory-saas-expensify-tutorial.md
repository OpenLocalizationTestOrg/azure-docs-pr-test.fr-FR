---
title: "Didacticiel : Intégration d’Azure Active Directory avec Expensify | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="c6192-103">Didacticiel : Intégration d’Azure Active Directory avec Expensify</span><span class="sxs-lookup"><span data-stu-id="c6192-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="c6192-104">Dans ce didacticiel, vous apprendrez comment toointegrate Expensify avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6192-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6192-105">Intégration Expensify à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c6192-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c6192-106">Vous pouvez contrôler dans Azure AD qui a accès tooExpensify</span><span class="sxs-lookup"><span data-stu-id="c6192-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="c6192-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooExpensify (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6192-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c6192-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c6192-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6192-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6192-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c6192-110">Prerequisites</span></span>

<span data-ttu-id="c6192-111">tooconfigure intégration d’Azure AD avec Expensify, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c6192-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="c6192-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6192-113">Un abonnement Expensify pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c6192-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6192-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c6192-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6192-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c6192-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6192-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c6192-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6192-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6192-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6192-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c6192-118">Scenario description</span></span>
<span data-ttu-id="c6192-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c6192-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6192-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c6192-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6192-121">Ajout de Expensify à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c6192-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="c6192-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="c6192-123">Ajout de Expensify à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c6192-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="c6192-124">intégration de hello tooconfigure de Expensify dans Azure AD, vous devez tooadd Expensify à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c6192-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c6192-125">**tooadd Expensify à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c6192-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6192-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c6192-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6192-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c6192-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c6192-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c6192-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c6192-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c6192-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c6192-133">Dans la zone de recherche de hello, tapez **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="c6192-133">In hello search box, type **Expensify**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="c6192-135">Dans le volet de résultats hello, sélectionnez **Expensify**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c6192-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6192-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6192-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Expensify avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c6192-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6192-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Expensify est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6192-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="c6192-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Expensify doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c6192-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="c6192-141">Dans Expensify, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c6192-142">tooconfigure et test Azure AD l’authentification unique avec Expensify, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c6192-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c6192-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c6192-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c6192-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c6192-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6192-145">**[Création d’un utilisateur de test Expensify](#creating-an-expensify-test-user)**  -toohave un équivalent de Britta Simon dans Expensify est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c6192-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6192-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c6192-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6192-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c6192-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6192-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6192-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Expensify.</span><span class="sxs-lookup"><span data-stu-id="c6192-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="c6192-150">**tooconfigure Azure AD single sign-on avec Expensify, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c6192-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6192-151">Bonjour portail Azure, sur hello **Expensify** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c6192-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c6192-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c6192-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="c6192-155">Sur hello **Expensify de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6192-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="c6192-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6192-157">a.</span></span> <span data-ttu-id="c6192-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="c6192-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="c6192-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6192-159">b.</span></span> <span data-ttu-id="c6192-160">Bonjour **URL d’identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="c6192-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="c6192-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c6192-161">These values are not real.</span></span> <span data-ttu-id="c6192-162">Mettre à jour ces valeurs avec l’URL réelle de l’authentification sur l’URL et l’identificateur hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="c6192-163">Contact [équipe de support Client de Expensify](mailto:help@expensify.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c6192-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c6192-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c6192-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="c6192-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c6192-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6192-168">tooenable SSO dans Expensify, vous devez tout d’abord tooenable **domaine contrôle** dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="c6192-169">Vous pouvez activer le contrôle de domaine dans l’application hello à travers les étapes de hello répertoriés [ici](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="c6192-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="c6192-170">Pour une assistance supplémentaire, travaillez avec [l’équipe de support technique Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="c6192-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="c6192-171">Une fois que le contrôle de domaine est activé, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c6192-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="c6192-173">a.</span><span class="sxs-lookup"><span data-stu-id="c6192-173">a.</span></span> <span data-ttu-id="c6192-174">Ouverture de session tooyour Expensify application.</span><span class="sxs-lookup"><span data-stu-id="c6192-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="c6192-175">b.</span><span class="sxs-lookup"><span data-stu-id="c6192-175">b.</span></span> <span data-ttu-id="c6192-176">Dans la barre d’outils de hello en haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c6192-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="c6192-177">c.</span><span class="sxs-lookup"><span data-stu-id="c6192-177">c.</span></span> <span data-ttu-id="c6192-178">Dans le volet gauche de hello, cliquez sur **domaine**.</span><span class="sxs-lookup"><span data-stu-id="c6192-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="c6192-179">d.</span><span class="sxs-lookup"><span data-stu-id="c6192-179">d.</span></span> <span data-ttu-id="c6192-180">Cliquez sur le nom de votre domaine vérifié.</span><span class="sxs-lookup"><span data-stu-id="c6192-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="c6192-181">e.</span><span class="sxs-lookup"><span data-stu-id="c6192-181">e.</span></span> <span data-ttu-id="c6192-182">Dans le volet gauche de hello, cliquez sur **SAML**, puis sélectionnez **activé**.</span><span class="sxs-lookup"><span data-stu-id="c6192-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="c6192-183">f.</span><span class="sxs-lookup"><span data-stu-id="c6192-183">f.</span></span> <span data-ttu-id="c6192-184">Ouvrez hello téléchargé des métadonnées de fédération à partir d’Azure AD dans le bloc-notes, hello copie le contenu et le coller ensuite dans hello **métadonnées du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c6192-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="c6192-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c6192-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c6192-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c6192-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6192-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6192-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6192-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c6192-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c6192-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c6192-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6192-192">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c6192-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6192-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c6192-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6192-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6192-198">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6192-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6192-200">a.</span><span class="sxs-lookup"><span data-stu-id="c6192-200">a.</span></span> <span data-ttu-id="c6192-201">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6192-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6192-202">b.</span><span class="sxs-lookup"><span data-stu-id="c6192-202">b.</span></span> <span data-ttu-id="c6192-203">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6192-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6192-204">c.</span><span class="sxs-lookup"><span data-stu-id="c6192-204">c.</span></span> <span data-ttu-id="c6192-205">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c6192-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c6192-206">d.</span><span class="sxs-lookup"><span data-stu-id="c6192-206">d.</span></span> <span data-ttu-id="c6192-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c6192-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="c6192-208">Création d’un utilisateur test Expensify</span><span class="sxs-lookup"><span data-stu-id="c6192-208">Creating an Expensify test user</span></span>

<span data-ttu-id="c6192-209">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Expensify.</span><span class="sxs-lookup"><span data-stu-id="c6192-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="c6192-210">Travailler avec [équipe de support Client de Expensify](mailto:help@expensify.com) tooadd les utilisateurs de hello dans la plateforme de Expensify hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c6192-211">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6192-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c6192-212">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooExpensify.</span><span class="sxs-lookup"><span data-stu-id="c6192-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c6192-214">**tooassign Britta Simon tooExpensify, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c6192-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6192-215">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c6192-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c6192-217">Dans la liste des applications hello, sélectionnez **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="c6192-217">In hello applications list, select **Expensify**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="c6192-219">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c6192-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c6192-221">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c6192-221">Click **Add** button.</span></span> <span data-ttu-id="c6192-222">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c6192-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c6192-224">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c6192-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c6192-225">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c6192-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6192-226">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c6192-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6192-227">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c6192-227">Testing single sign-on</span></span>

<span data-ttu-id="c6192-228">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c6192-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c6192-229">Lorsque vous cliquez sur mosaïque Expensify hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Expensify application.</span><span class="sxs-lookup"><span data-stu-id="c6192-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6192-230">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c6192-230">Additional resources</span></span>

* [<span data-ttu-id="c6192-231">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6192-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6192-232">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c6192-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

