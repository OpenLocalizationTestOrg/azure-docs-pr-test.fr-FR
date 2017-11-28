---
title: "Didacticiel : Intégration d’Azure Active Directory à FM:Systems | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et FM : Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="28260-103">Didacticiel : Intégration d’Azure Active Directory à FM:Systems</span><span class="sxs-lookup"><span data-stu-id="28260-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="28260-104">Dans ce didacticiel, vous apprendrez comment toointegrate FM : Systems avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28260-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28260-105">Intégration FM : Systems à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="28260-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28260-106">Vous pouvez contrôler dans Azure AD qui a accès tooFM:Systems</span><span class="sxs-lookup"><span data-stu-id="28260-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="28260-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFM:Systems (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28260-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="28260-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28260-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28260-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28260-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="28260-110">Prerequisites</span></span>

<span data-ttu-id="28260-111">tooconfigure intégration d’Azure AD avec FM : Systems, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="28260-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="28260-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28260-113">Un abonnement FM:Systems pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="28260-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28260-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="28260-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28260-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="28260-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28260-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="28260-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28260-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28260-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28260-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="28260-118">Scenario description</span></span>
<span data-ttu-id="28260-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="28260-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28260-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="28260-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28260-121">Ajout de FM : Systems à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="28260-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="28260-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="28260-123">Ajout de FM : Systems à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="28260-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="28260-124">tooconfigure hello intégration de FM : Systems dans Azure AD, vous devez tooadd FM : Systems à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="28260-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28260-125">**tooadd FM : Systems à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28260-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28260-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="28260-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28260-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="28260-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28260-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="28260-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="28260-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="28260-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="28260-133">Dans la zone de recherche de hello, tapez **FM : Systems**.</span><span class="sxs-lookup"><span data-stu-id="28260-133">In hello search box, type **FM:Systems**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="28260-135">Dans le volet de résultats hello, sélectionnez **FM : Systems**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="28260-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28260-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28260-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FM:Systems, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="28260-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28260-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FM : Systems est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28260-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="28260-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FM : Systems doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="28260-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="28260-141">Dans FM : Systems, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="28260-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="28260-142">tooconfigure et test Azure AD l’authentification unique avec FM : Systems, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="28260-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28260-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="28260-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28260-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28260-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28260-145">**[Création d’un utilisateur de test FM : Systems](#creating-an-fmsystems-test-user)**  -toohave un homologue de Britta Simon dans FM : Systems qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="28260-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28260-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28260-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28260-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="28260-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28260-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28260-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application FM : Systems.</span><span class="sxs-lookup"><span data-stu-id="28260-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="28260-150">**tooconfigure Azure AD single sign-on avec FM : Systems, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28260-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="28260-151">Bonjour portail Azure, sur hello **FM : Systems** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="28260-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="28260-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28260-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="28260-155">Sur hello **FM : Systems domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28260-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="28260-157">Bonjour **URL de réponse** zone de texte, tapez votre FM : Systems **URL de réponse**, tapez l’URL hello hello suivant le modèle à l’aide de :`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="28260-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28260-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="28260-158">This value is not real.</span></span> <span data-ttu-id="28260-159">Mettre à jour cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="28260-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="28260-160">Contact [équipe de support FM : Systems](https://fmsystems.com/ask-us/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="28260-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="28260-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="28260-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="28260-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="28260-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="28260-165">tooconfigure l’authentification unique sur **FM : Systems** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support FM : Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="28260-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="28260-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="28260-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="28260-167">Vous recevrez une notification dès que l’authentification unique aura été activée pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="28260-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="28260-168">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="28260-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28260-169">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="28260-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28260-170">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28260-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28260-171">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="28260-172">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="28260-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="28260-174">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28260-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28260-175">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="28260-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28260-177">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="28260-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28260-179">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="28260-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28260-181">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28260-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28260-183">a.</span><span class="sxs-lookup"><span data-stu-id="28260-183">a.</span></span> <span data-ttu-id="28260-184">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28260-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28260-185">b.</span><span class="sxs-lookup"><span data-stu-id="28260-185">b.</span></span> <span data-ttu-id="28260-186">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28260-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28260-187">c.</span><span class="sxs-lookup"><span data-stu-id="28260-187">c.</span></span> <span data-ttu-id="28260-188">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="28260-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28260-189">d.</span><span class="sxs-lookup"><span data-stu-id="28260-189">d.</span></span> <span data-ttu-id="28260-190">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="28260-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="28260-191">Création d’un utilisateur de test FM:Systems</span><span class="sxs-lookup"><span data-stu-id="28260-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="28260-192">Dans une fenêtre de navigateur web, connectez-vous à votre site d’entreprise FM:Systems en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="28260-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="28260-193">Accédez trop**Administration système \> gérer la sécurité \> utilisateurs \> liste des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="28260-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="28260-194">![Administration système](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Administration système")</span><span class="sxs-lookup"><span data-stu-id="28260-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="28260-195">Cliquez sur **Create new user**.</span><span class="sxs-lookup"><span data-stu-id="28260-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="28260-196">![Créer un nouvel utilisateur](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Créer un nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="28260-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="28260-197">Bonjour **Create User** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28260-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="28260-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="28260-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="28260-199">a.</span><span class="sxs-lookup"><span data-stu-id="28260-199">a.</span></span> <span data-ttu-id="28260-200">Hello de type **nom d’utilisateur**, hello **mot de passe**, **confirmer le mot de passe**, **messagerie** et hello **ID d’employé**d’un Azure valide compte Active Directory que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="28260-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="28260-201">b.</span><span class="sxs-lookup"><span data-stu-id="28260-201">b.</span></span> <span data-ttu-id="28260-202">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="28260-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="28260-203">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28260-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="28260-204">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooFM:Systems.</span><span class="sxs-lookup"><span data-stu-id="28260-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="28260-206">**tooassign Britta Simon tooFM:Systems, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28260-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="28260-207">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="28260-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="28260-209">Dans la liste des applications hello, sélectionnez **FM : Systems**.</span><span class="sxs-lookup"><span data-stu-id="28260-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="28260-211">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="28260-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="28260-213">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="28260-213">Click **Add** button.</span></span> <span data-ttu-id="28260-214">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="28260-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="28260-216">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="28260-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28260-217">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="28260-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28260-218">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="28260-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28260-219">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="28260-219">Testing single sign-on</span></span>

<span data-ttu-id="28260-220">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="28260-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="28260-221">Lorsque vous cliquez sur mosaïque FM : Systems hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour FM : Systems application.</span><span class="sxs-lookup"><span data-stu-id="28260-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="28260-222">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28260-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28260-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="28260-223">Additional resources</span></span>

* [<span data-ttu-id="28260-224">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28260-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28260-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="28260-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

