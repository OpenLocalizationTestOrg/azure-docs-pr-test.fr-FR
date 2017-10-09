---
title: "Didacticiel : Intégration d’Azure Active Directory à Yonyx Interactive Guides | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et des Guides de Yonyx Interactive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="7fe47-103">Didacticiel : Intégration d’Azure Active Directory à Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="7fe47-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="7fe47-104">Dans ce didacticiel, vous apprendrez comment toointegrate Yonyx Interactive Guide avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7fe47-104">In this tutorial, you learn how toointegrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fe47-105">Intégration Yonyx les manuels interactifs à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7fe47-105">Integrating Yonyx Interactive Guides with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7fe47-106">Vous pouvez contrôler dans Azure AD qui a accès tooYonyx manuels interactifs</span><span class="sxs-lookup"><span data-stu-id="7fe47-106">You can control in Azure AD who has access tooYonyx Interactive Guides</span></span>
- <span data-ttu-id="7fe47-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooYonyx manuels interactifs (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-107">You can enable your users tooautomatically get signed-on tooYonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fe47-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fe47-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7fe47-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fe47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fe47-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7fe47-110">Prerequisites</span></span>

<span data-ttu-id="7fe47-111">tooconfigure intégration d’Azure AD avec les repères de Yonyx interactif, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7fe47-111">tooconfigure Azure AD integration with Yonyx Interactive Guides, you need hello following items:</span></span>

- <span data-ttu-id="7fe47-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fe47-113">Un abonnement Yonyx Interactive Guides pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7fe47-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fe47-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7fe47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fe47-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7fe47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fe47-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7fe47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fe47-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fe47-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fe47-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7fe47-118">Scenario description</span></span>
<span data-ttu-id="7fe47-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7fe47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fe47-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7fe47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fe47-121">Ajout de repères de Yonyx Interactive à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7fe47-121">Adding Yonyx Interactive Guides from hello gallery</span></span>
2. <span data-ttu-id="7fe47-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a><span data-ttu-id="7fe47-123">Ajout de repères de Yonyx Interactive à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7fe47-123">Adding Yonyx Interactive Guides from hello gallery</span></span>
<span data-ttu-id="7fe47-124">tooconfigure hello intégration des repères de Yonyx Interactive dans Azure AD, vous devez tooadd Yonyx les Guides Interactive à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7fe47-124">tooconfigure hello integration of Yonyx Interactive Guides into Azure AD, you need tooadd Yonyx Interactive Guides from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7fe47-125">**tooadd Yonyx les Guides Interactive à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7fe47-125">**tooadd Yonyx Interactive Guides from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe47-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7fe47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="7fe47-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7fe47-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="7fe47-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7fe47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="7fe47-133">Dans la zone de recherche de hello, tapez **Yonyx les manuels interactifs**, sélectionnez **Yonyx les manuels interactifs** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7fe47-133">In hello search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Repères de Yonyx Interactive dans la liste des résultats hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7fe47-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7fe47-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Yonyx Interactive Guides, sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7fe47-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7fe47-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les Guides de Yonyx Interactive est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fe47-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yonyx Interactive Guides is tooa user in Azure AD.</span></span> <span data-ttu-id="7fe47-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les Guides de Yonyx Interactive hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7fe47-138">In other words, a link relationship between an Azure AD user and hello related user in Yonyx Interactive Guides needs toobe established.</span></span>

<span data-ttu-id="7fe47-139">Dans les Guides de Yonyx Interactive, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="7fe47-139">In Yonyx Interactive Guides, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7fe47-140">tooconfigure et test Azure AD l’authentification unique avec les repères de Yonyx interactif, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7fe47-140">tooconfigure and test Azure AD single sign-on with Yonyx Interactive Guides, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7fe47-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7fe47-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7fe47-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7fe47-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fe47-143">**[Créer un utilisateur de test manuels interactifs de Yonyx](#create-a-yonyx-interactive-guides-test-user)**  -toohave un équivalent de Britta Simon Yonyx guides interactif est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7fe47-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - toohave a counterpart of Britta Simon in Yonyx Interactive Guides that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fe47-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7fe47-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fe47-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7fe47-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7fe47-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7fe47-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Yonyx les manuels interactifs.</span><span class="sxs-lookup"><span data-stu-id="7fe47-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="7fe47-148">**tooconfigure Azure AD l’authentification unique avec les repères de Yonyx Interactive, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7fe47-148">**tooconfigure Azure AD single sign-on with Yonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe47-149">Bonjour portail Azure, sur hello **Yonyx les manuels interactifs** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-149">In hello Azure portal, on hello **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="7fe47-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7fe47-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="7fe47-153">Sur hello **Yonyx Interactive Guides de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fe47-153">On hello **Yonyx Interactive Guides Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="7fe47-155">a.</span><span class="sxs-lookup"><span data-stu-id="7fe47-155">a.</span></span> <span data-ttu-id="7fe47-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="7fe47-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="7fe47-157">b.</span><span class="sxs-lookup"><span data-stu-id="7fe47-157">b.</span></span> <span data-ttu-id="7fe47-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="7fe47-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7fe47-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7fe47-159">These values are not real.</span></span> <span data-ttu-id="7fe47-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="7fe47-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7fe47-161">Contact [équipe de support Client de Guides interactif Yonyx](mailto:support@yonyx.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="7fe47-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="7fe47-162">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7fe47-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="7fe47-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7fe47-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7fe47-166">Sur hello **Yonyx Interactive Guides de Configuration** , cliquez sur **configurer les manuels interactifs Yonyx** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7fe47-166">On hello **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7fe47-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7fe47-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="7fe47-169">tooconfigure l’authentification unique sur **Yonyx les manuels interactifs** côté, vous devez hello toosend téléchargé **Certificate(Base64)**, **URL de déconnexion**, **SAML Single Sign-On URL du Service** **ID d’entité SAML** trop[Yonyx les manuels interactifs l’équipe de support](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="7fe47-169">tooconfigure single sign-on on **Yonyx Interactive Guides** side, you need toosend hello downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** too[Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="7fe47-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="7fe47-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7fe47-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="7fe47-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7fe47-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="7fe47-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7fe47-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fe47-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7fe47-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-174">Create an Azure AD test user</span></span>

<span data-ttu-id="7fe47-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="7fe47-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

  ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="7fe47-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7fe47-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe47-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7fe47-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fe47-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fe47-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="7fe47-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fe47-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fe47-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fe47-186">a.</span><span class="sxs-lookup"><span data-stu-id="7fe47-186">a.</span></span> <span data-ttu-id="7fe47-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fe47-188">b.</span><span class="sxs-lookup"><span data-stu-id="7fe47-188">b.</span></span> <span data-ttu-id="7fe47-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7fe47-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fe47-190">c.</span><span class="sxs-lookup"><span data-stu-id="7fe47-190">c.</span></span> <span data-ttu-id="7fe47-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7fe47-192">d.</span><span class="sxs-lookup"><span data-stu-id="7fe47-192">d.</span></span> <span data-ttu-id="7fe47-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="7fe47-194">Créer un utilisateur de test Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="7fe47-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="7fe47-195">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans les Guides de Yonyx Interactive.</span><span class="sxs-lookup"><span data-stu-id="7fe47-195">hello objective of this section is toocreate a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="7fe47-196">Yonyx Interactive Guides prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="7fe47-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7fe47-197">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="7fe47-197">There is no action item for you in this section.</span></span> <span data-ttu-id="7fe47-198">Un nouvel utilisateur est créé pendant un tooaccess tentative Yonyx les Guides interactif s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="7fe47-198">A new user is created during an attempt tooaccess Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7fe47-199">Si vous devez manuellement toocreate un utilisateur, vous devez hello toocontact Yonyx les manuels interactifs prennent en charge l’équipe via < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="7fe47-199">If you need toocreate a user manually, you need toocontact hello Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7fe47-200">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fe47-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7fe47-201">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooYonyx manuels interactifs.</span><span class="sxs-lookup"><span data-stu-id="7fe47-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYonyx Interactive Guides.</span></span>

![Attribuer le rôle d’utilisateur hello][200]

<span data-ttu-id="7fe47-203">**tooassign Britta Simon tooYonyx les repères Interactive, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7fe47-203">**tooassign Britta Simon tooYonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe47-204">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7fe47-206">Dans la liste des applications hello, sélectionnez **Yonyx les manuels interactifs**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-206">In hello applications list, select **Yonyx Interactive Guides**.</span></span>

    ![lien de Guides interactif de Yonyx Hello dans la liste des Applications hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="7fe47-208">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="7fe47-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-210">Click **Add** button.</span></span> <span data-ttu-id="7fe47-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="7fe47-213">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7fe47-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7fe47-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fe47-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7fe47-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7fe47-216">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7fe47-216">Test single sign-on</span></span>

<span data-ttu-id="7fe47-217">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7fe47-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7fe47-218">Lorsque vous cliquez sur hello Guides interactif de Yonyx vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de Yonyx les manuels interactifs.</span><span class="sxs-lookup"><span data-stu-id="7fe47-218">When you click hello Yonyx Interactive Guides tile in hello Access Panel, you should get automatically signed-on tooyour Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="7fe47-219">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fe47-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fe47-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7fe47-220">Additional resources</span></span>

* [<span data-ttu-id="7fe47-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fe47-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fe47-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7fe47-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

