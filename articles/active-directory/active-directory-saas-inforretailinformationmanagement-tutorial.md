---
title: "Didacticiel : Intégration d’Azure Active Directory avec Infor Retail – Information Management | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les informations de vente au détail – gestion des informations."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="c3baf-103">Didacticiel : Intégration d’Azure Active Directory avec Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="c3baf-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="c3baf-104">Dans ce didacticiel, vous apprendrez comment toointegrate commerce de détail les informations de gestion des informations avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3baf-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3baf-105">Intégrer les informations de vente au détail – gestion des informations auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c3baf-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3baf-106">Vous pouvez contrôler dans Azure AD qui a accès tooInfor vente au détail – gestion des informations.</span><span class="sxs-lookup"><span data-stu-id="c3baf-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="c3baf-107">Vous pouvez activer vos utilisateurs tooautomatically get signé sur tooInfor Retail – gestion des informations (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3baf-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c3baf-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c3baf-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c3baf-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3baf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3baf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c3baf-110">Prerequisites</span></span>

<span data-ttu-id="c3baf-111">tooconfigure intégration d’Azure AD avec les informations de vente au détail – gestion des informations, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c3baf-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="c3baf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3baf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3baf-113">Un abonnement autorisant l’authentification unique à Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="c3baf-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3baf-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c3baf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3baf-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c3baf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3baf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c3baf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3baf-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3baf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3baf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c3baf-118">Scenario description</span></span>
<span data-ttu-id="c3baf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c3baf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3baf-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c3baf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3baf-121">Ajout de commerce de détail les informations de gestion des informations à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c3baf-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="c3baf-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3baf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="c3baf-123">Ajout de commerce de détail les informations de gestion des informations à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c3baf-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="c3baf-124">intégration de hello tooconfigure des informations de vente au détail – gestion des informations dans Azure AD, vous devez tooadd les informations de vente au détail – gestion des informations à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c3baf-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3baf-125">**tooadd commerce de détail les informations de gestion des informations à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3baf-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3baf-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c3baf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="c3baf-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3baf-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="c3baf-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c3baf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="c3baf-133">Dans la zone de recherche de hello, tapez **les informations de vente au détail – gestion des informations**, sélectionnez **les informations de vente au détail – gestion des informations** à partir du volet de résultats, puis sur **ajouter** hello tooadd de bouton application.</span><span class="sxs-lookup"><span data-stu-id="c3baf-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Les informations de vente au détail – gestion des informations dans la liste des résultats hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c3baf-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3baf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c3baf-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Infor Retail – Information Management et un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c3baf-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3baf-137">Pour les toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les informations de détail : gestion des informations est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3baf-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="c3baf-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les informations de vente au détail – gestion des informations hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c3baf-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="c3baf-139">Dans les informations de vente au détail – gestion des informations, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c3baf-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3baf-140">tooconfigure et test Azure AD l’authentification unique avec les informations de vente au détail – gestion des informations, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c3baf-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3baf-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c3baf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3baf-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3baf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3baf-143">**[Créer un informations de vente au détail – utilisateur de test de gestion des informations](#create-an-infor-retail--information-management-test-user)**  - toohave de Britta Simon dans les informations de détail contrepartie – gestion des informations qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c3baf-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3baf-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c3baf-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3baf-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c3baf-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c3baf-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3baf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c3baf-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre les informations de vente au détail – application de gestion des informations.</span><span class="sxs-lookup"><span data-stu-id="c3baf-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="c3baf-148">**tooconfigure Azure AD l’authentification unique avec les informations de vente au détail – gestion des informations, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3baf-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3baf-149">Bonjour portail Azure, sur hello **les informations de vente au détail – gestion des informations** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c3baf-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c3baf-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="c3baf-153">Sur hello **les informations de vente au détail – informations de gestion de domaine et les URL** section, effectuer hello comme suit si vous le souhaitez en mode initié par l’application hello tooconfigure IDP :</span><span class="sxs-lookup"><span data-stu-id="c3baf-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informations d’authentification unique dans Infor Retail – Information Management Domain and URLs (Domaine et URL Infor Retail – Information Management) - Fournisseur d’identité](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="c3baf-155">a.</span><span class="sxs-lookup"><span data-stu-id="c3baf-155">a.</span></span> <span data-ttu-id="c3baf-156">Bonjour **identificateur** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c3baf-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="c3baf-157">b.</span><span class="sxs-lookup"><span data-stu-id="c3baf-157">b.</span></span> <span data-ttu-id="c3baf-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="c3baf-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="c3baf-159">Vérifiez **afficher les paramètres d’URL avancés** et effectuer hello suivant l’étape si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="c3baf-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Infor Retail – Information Management Domain and URLs (Domaine et URL Infor Retail – Information Management) - Fournisseur de service](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="c3baf-161">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="c3baf-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c3baf-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c3baf-162">These values are not real.</span></span> <span data-ttu-id="c3baf-163">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="c3baf-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c3baf-164">Contact [les informations de vente au détail – équipe de support Client de gestion des informations](mailto:innovate@infor.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c3baf-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="c3baf-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c3baf-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="c3baf-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c3baf-167">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c3baf-169">tooconfigure l’authentification unique sur **les informations de vente au détail – gestion des informations** côté, vous devez hello toosend téléchargé **Metadata XML** trop[les informations de vente au détail – équipe de support technique de gestion des informations ](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="c3baf-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="c3baf-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="c3baf-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c3baf-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c3baf-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3baf-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c3baf-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3baf-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3baf-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c3baf-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3baf-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c3baf-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c3baf-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c3baf-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3baf-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3baf-178">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="c3baf-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c3baf-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c3baf-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c3baf-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c3baf-184">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3baf-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c3baf-186">a.</span><span class="sxs-lookup"><span data-stu-id="c3baf-186">a.</span></span> <span data-ttu-id="c3baf-187">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3baf-188">b.</span><span class="sxs-lookup"><span data-stu-id="c3baf-188">b.</span></span> <span data-ttu-id="c3baf-189">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3baf-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c3baf-190">c.</span><span class="sxs-lookup"><span data-stu-id="c3baf-190">c.</span></span> <span data-ttu-id="c3baf-191">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="c3baf-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c3baf-192">d.</span><span class="sxs-lookup"><span data-stu-id="c3baf-192">d.</span></span> <span data-ttu-id="c3baf-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="c3baf-194">Créer un utilisateur de test Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="c3baf-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="c3baf-195">Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="c3baf-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="c3baf-196">Collaborez avec [les informations de vente au détail – équipe de support technique de gestion des informations](mailto:innovate@infor.com) utilisateurs hello tooadd hello les informations de vente au détail : plateforme de gestion des informations.</span><span class="sxs-lookup"><span data-stu-id="c3baf-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c3baf-197">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3baf-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c3baf-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooInfor vente au détail – gestion des informations.</span><span class="sxs-lookup"><span data-stu-id="c3baf-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="c3baf-200">**tooassign Britta Simon tooInfor vente au détail – gestion des informations, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3baf-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3baf-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c3baf-203">Dans la liste des applications hello, sélectionnez **les informations de vente au détail – gestion des informations**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![Hello les informations de vente au détail – gestion des informations de liaison dans la liste des Applications hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="c3baf-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="c3baf-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-207">Click **Add** button.</span></span> <span data-ttu-id="c3baf-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="c3baf-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c3baf-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3baf-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3baf-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c3baf-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c3baf-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c3baf-213">Test single sign-on</span></span>

<span data-ttu-id="c3baf-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c3baf-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c3baf-215">Lorsque vous cliquez sur hello les informations de vente au détail – vignette de gestion des informations dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour les informations de détail – application de gestion des informations.</span><span class="sxs-lookup"><span data-stu-id="c3baf-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="c3baf-216">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3baf-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c3baf-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c3baf-217">Additional resources</span></span>

* [<span data-ttu-id="c3baf-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3baf-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3baf-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c3baf-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

