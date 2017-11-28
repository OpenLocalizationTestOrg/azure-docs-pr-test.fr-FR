---
title: "Didacticiel : Intégration d’Azure Active Directory à YouEarnedIt | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="39323-103">Didacticiel : Intégration d’Azure Active Directory à YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="39323-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="39323-104">Dans ce didacticiel, vous apprendrez comment toointegrate YouEarnedIt avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39323-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39323-105">Intégration YouEarnedIt à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="39323-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39323-106">Vous pouvez contrôler dans Azure AD qui a accès tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="39323-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="39323-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooYouEarnedIt (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39323-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="39323-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="39323-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="39323-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39323-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39323-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="39323-110">Prerequisites</span></span>

<span data-ttu-id="39323-111">tooconfigure intégration d’Azure AD avec YouEarnedIt, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="39323-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="39323-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="39323-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39323-113">Un abonnement YouEarnedIt pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="39323-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39323-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="39323-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39323-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="39323-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39323-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="39323-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39323-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39323-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39323-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="39323-118">Scenario description</span></span>
<span data-ttu-id="39323-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="39323-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39323-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="39323-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39323-121">Ajout de YouEarnedIt à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="39323-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="39323-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="39323-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="39323-123">Ajout de YouEarnedIt à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="39323-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="39323-124">intégration de hello tooconfigure de YouEarnedIt dans Azure AD, vous devez tooadd YouEarnedIt à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="39323-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39323-125">**tooadd YouEarnedIt à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39323-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39323-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="39323-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="39323-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="39323-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39323-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="39323-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="39323-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="39323-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="39323-133">Dans la zone de recherche de hello, tapez **YouEarnedt**, sélectionnez **YouEarnedt** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="39323-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![YouEarnedIt dans la liste des résultats hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="39323-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="39323-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="39323-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec YouEarnedIt avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="39323-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39323-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans YouEarnedIt est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39323-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="39323-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans YouEarnedIt doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="39323-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="39323-139">Dans YouEarnedIt, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="39323-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39323-140">tooconfigure et test Azure AD l’authentification unique avec YouEarnedIt, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="39323-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39323-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="39323-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39323-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39323-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39323-143">**[Créer un utilisateur de test YouEarnedIt](#create-a-youearnedit-test-user)**  -toohave un équivalent de Britta Simon dans YouEarnedIt est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="39323-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39323-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="39323-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39323-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="39323-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="39323-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="39323-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="39323-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="39323-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="39323-148">**tooconfigure Azure AD single sign-on avec YouEarnedIt, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39323-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="39323-149">Bonjour portail Azure, sur hello **YouEarnedIt** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="39323-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="39323-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="39323-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="39323-153">Sur hello **YouEarnedIt domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="39323-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="39323-155">a.</span><span class="sxs-lookup"><span data-stu-id="39323-155">a.</span></span> <span data-ttu-id="39323-156">Bonjour **URL de connexion** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="39323-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="39323-157">Environnement</span><span class="sxs-lookup"><span data-stu-id="39323-157">Environment</span></span>  | <span data-ttu-id="39323-158">Modèle</span><span class="sxs-lookup"><span data-stu-id="39323-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="39323-159">Production</span><span class="sxs-lookup"><span data-stu-id="39323-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="39323-160">Bac à sable</span><span class="sxs-lookup"><span data-stu-id="39323-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="39323-161">b.</span><span class="sxs-lookup"><span data-stu-id="39323-161">b.</span></span> <span data-ttu-id="39323-162">Bonjour **identificateur** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="39323-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="39323-163">Environnement</span><span class="sxs-lookup"><span data-stu-id="39323-163">Environment</span></span>  | <span data-ttu-id="39323-164">Modèle</span><span class="sxs-lookup"><span data-stu-id="39323-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="39323-165">Production</span><span class="sxs-lookup"><span data-stu-id="39323-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="39323-166">Bac à sable</span><span class="sxs-lookup"><span data-stu-id="39323-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="39323-167">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="39323-167">These values are not real.</span></span> <span data-ttu-id="39323-168">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="39323-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="39323-169">Contact [équipe de support Client de YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="39323-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="39323-170">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="39323-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="39323-172">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="39323-172">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="39323-174">Sur hello **YouEarnedIt Configuration** , cliquez sur **YouEarnedIt de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="39323-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="39323-175">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="39323-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="39323-177">tooconfigure l’authentification unique sur **YouEarnedIt** côté, vous devez hello toosend téléchargé **Certificate(Base64)** et **SAML Sign-On URL du Service unique** trop[Équipe de support YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="39323-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="39323-178">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="39323-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="39323-179">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="39323-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39323-180">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="39323-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39323-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39323-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="39323-182">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="39323-182">Create an Azure AD test user</span></span>

<span data-ttu-id="39323-183">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="39323-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="39323-185">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39323-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39323-186">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="39323-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="39323-188">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="39323-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="39323-190">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="39323-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="39323-192">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="39323-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="39323-194">a.</span><span class="sxs-lookup"><span data-stu-id="39323-194">a.</span></span> <span data-ttu-id="39323-195">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39323-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39323-196">b.</span><span class="sxs-lookup"><span data-stu-id="39323-196">b.</span></span> <span data-ttu-id="39323-197">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39323-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="39323-198">c.</span><span class="sxs-lookup"><span data-stu-id="39323-198">c.</span></span> <span data-ttu-id="39323-199">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="39323-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="39323-200">d.</span><span class="sxs-lookup"><span data-stu-id="39323-200">d.</span></span> <span data-ttu-id="39323-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="39323-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="39323-202">Créer un utilisateur de test YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="39323-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="39323-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="39323-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="39323-204">Collaborez avec les utilisateurs YouEarnedIt prise en charge team tooadd hello dans la plateforme de YouEarnedIt hello.</span><span class="sxs-lookup"><span data-stu-id="39323-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="39323-205">YouEarnedIt attendre hello fournisseur d’identité toosupply un EmailAddress ou le nom d’utilisateur dans l’attribut de NameID hello.</span><span class="sxs-lookup"><span data-stu-id="39323-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="39323-206">L’authentification échoue si un nom d’utilisateur correspondant EmailAddress n’est trouvé dans la base de données hello ou ne correspond pas exactement.</span><span class="sxs-lookup"><span data-stu-id="39323-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="39323-207">Cette opération nécessite que les comptes d’être importé dans YouEarnedIt hello avant l’intégration de l’authentification unique hello (en général, soit via l’importation des API ou CSV).</span><span class="sxs-lookup"><span data-stu-id="39323-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="39323-208">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="39323-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="39323-209">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="39323-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="39323-211">**tooassign Britta Simon tooYouEarnedIt, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39323-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="39323-212">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="39323-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="39323-214">Dans la liste des applications hello, sélectionnez **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="39323-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![lien de YouEarnedIt Hello dans la liste des Applications hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="39323-216">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="39323-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="39323-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="39323-218">Click **Add** button.</span></span> <span data-ttu-id="39323-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="39323-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="39323-221">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="39323-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39323-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="39323-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39323-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="39323-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="39323-224">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="39323-224">Test single sign-on</span></span>

<span data-ttu-id="39323-225">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="39323-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="39323-226">Lorsque vous cliquez sur mosaïque YouEarnedIt hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour YouEarnedIt application.</span><span class="sxs-lookup"><span data-stu-id="39323-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="39323-227">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39323-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="39323-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="39323-228">Additional resources</span></span>

* [<span data-ttu-id="39323-229">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39323-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39323-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="39323-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

