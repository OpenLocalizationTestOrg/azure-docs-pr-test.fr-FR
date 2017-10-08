---
title: "Didacticiel : Intégration d’Azure Active Directory à SpringCM | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="488db-103">Didacticiel : Intégration d’Azure Active Directory à SpringCM</span><span class="sxs-lookup"><span data-stu-id="488db-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="488db-104">Dans ce didacticiel, vous apprendrez comment toointegrate SpringCM avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="488db-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="488db-105">Intégration de SpringCM avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="488db-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="488db-106">Vous pouvez contrôler dans Azure AD qui a accès tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="488db-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="488db-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSpringCM (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="488db-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="488db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="488db-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="488db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="488db-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="488db-110">Prerequisites</span></span>

<span data-ttu-id="488db-111">tooconfigure intégration d’Azure AD avec SpringCM, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="488db-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="488db-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="488db-113">Un abonnement SpringCM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="488db-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="488db-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="488db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="488db-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="488db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="488db-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="488db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="488db-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="488db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="488db-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="488db-118">Scenario description</span></span>
<span data-ttu-id="488db-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="488db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="488db-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="488db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="488db-121">Ajout de SpringCM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="488db-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="488db-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="488db-123">Ajout de SpringCM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="488db-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="488db-124">intégration de hello tooconfigure de SpringCM dans Azure AD, vous devez tooadd SpringCM à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="488db-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="488db-125">**tooadd SpringCM à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="488db-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="488db-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="488db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="488db-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="488db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="488db-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="488db-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="488db-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="488db-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="488db-133">Dans la zone de recherche de hello, tapez **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="488db-133">In hello search box, type **SpringCM**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="488db-135">Dans le volet de résultats hello, sélectionnez **SpringCM**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="488db-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="488db-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="488db-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SpringCM avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="488db-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="488db-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SpringCM est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="488db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="488db-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans SpringCM hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="488db-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="488db-141">Dans SpringCM, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="488db-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="488db-142">tooconfigure et test Azure AD l’authentification unique avec SpringCM, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="488db-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="488db-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="488db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="488db-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="488db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="488db-145">**[Création d’un utilisateur de test de SpringCM](#creating-a-springcm-test-user)**  -toohave un équivalent de Britta Simon dans SpringCM est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="488db-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="488db-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="488db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="488db-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="488db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="488db-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="488db-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SpringCM.</span><span class="sxs-lookup"><span data-stu-id="488db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="488db-150">**tooconfigure Azure AD single sign-on avec SpringCM, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="488db-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="488db-151">Bonjour portail Azure, sur hello **SpringCM** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="488db-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="488db-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="488db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="488db-155">Sur hello **SpringCM domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="488db-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="488db-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="488db-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="488db-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="488db-158">This value is not real.</span></span> <span data-ttu-id="488db-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="488db-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="488db-160">Contact [équipe de support Client de SpringCM](https://knowledge.springcm.com/support) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="488db-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="488db-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="488db-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="488db-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="488db-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="488db-165">Sur hello **SpringCM Configuration** , cliquez sur **configurer de SpringCM** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="488db-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="488db-166">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="488db-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="488db-168">Dans une fenêtre de navigateur web, connectez-vous tooyour **SpringCM** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="488db-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="488db-169">Dans le menu hello haut de hello, cliquez sur **atteindre**, cliquez sur **préférences**, puis, dans hello **préférences du compte** , cliquez sur **SSO SAML**.</span><span class="sxs-lookup"><span data-stu-id="488db-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="488db-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="488db-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="488db-171">Dans la section de Configuration du fournisseur d’identité de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="488db-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="488db-172">![Configuration du fournisseur d’identité](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configuration du fournisseur d’identité")</span><span class="sxs-lookup"><span data-stu-id="488db-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="488db-173">a.</span><span class="sxs-lookup"><span data-stu-id="488db-173">a.</span></span> <span data-ttu-id="488db-174">tooupload votre certificat Azure Active Directory, cliquez sur **sélectionner le certificat émetteur** ou **modifier le certificat émetteur**.</span><span class="sxs-lookup"><span data-stu-id="488db-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="488db-175">b.</span><span class="sxs-lookup"><span data-stu-id="488db-175">b.</span></span> <span data-ttu-id="488db-176">Coller **ID d’entité SAML** valeur, qui vous avez copié à partir du portail Azure en hello **émetteur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="488db-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="488db-177">c.</span><span class="sxs-lookup"><span data-stu-id="488db-177">c.</span></span> <span data-ttu-id="488db-178">Coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **Service Provider (SP) initiée par le point de terminaison** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="488db-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="488db-179">d.</span><span class="sxs-lookup"><span data-stu-id="488db-179">d.</span></span> <span data-ttu-id="488db-180">Sélectionnez **Enable** pour **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="488db-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="488db-181">e.</span><span class="sxs-lookup"><span data-stu-id="488db-181">e.</span></span> <span data-ttu-id="488db-182">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="488db-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="488db-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="488db-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="488db-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="488db-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="488db-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="488db-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="488db-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="488db-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="488db-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="488db-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="488db-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="488db-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="488db-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="488db-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="488db-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="488db-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="488db-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="488db-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="488db-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="488db-198">a.</span><span class="sxs-lookup"><span data-stu-id="488db-198">a.</span></span> <span data-ttu-id="488db-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="488db-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="488db-200">b.</span><span class="sxs-lookup"><span data-stu-id="488db-200">b.</span></span> <span data-ttu-id="488db-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="488db-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="488db-202">c.</span><span class="sxs-lookup"><span data-stu-id="488db-202">c.</span></span> <span data-ttu-id="488db-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="488db-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="488db-204">d.</span><span class="sxs-lookup"><span data-stu-id="488db-204">d.</span></span> <span data-ttu-id="488db-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="488db-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="488db-206">Création d’un utilisateur de test SpringCM</span><span class="sxs-lookup"><span data-stu-id="488db-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="488db-207">tooenable Azure Active Directory utilisateurs toolog dans tooSpringCM, vous devez les configurer dans SpringCM.</span><span class="sxs-lookup"><span data-stu-id="488db-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="488db-208">Dans les cas de hello de SpringCM, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="488db-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="488db-209">Pour plus d’informations, consultez [Créer et modifier un utilisateur SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="488db-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="488db-210">**tooprovision un tooSpringCM de compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="488db-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="488db-211">Connectez-vous à tooyour **SpringCM** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="488db-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="488db-212">Cliquez sur **GOTO** puis sur **ADDRESS BOOK**.</span><span class="sxs-lookup"><span data-stu-id="488db-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="488db-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="488db-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="488db-214">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="488db-214">Click **Create User**.</span></span>

4. <span data-ttu-id="488db-215">Sélectionnez un rôle d’utilisateur dans **User Role**.</span><span class="sxs-lookup"><span data-stu-id="488db-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="488db-216">Sélectionnez **Send Activation Email**.</span><span class="sxs-lookup"><span data-stu-id="488db-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="488db-217">Type hello prénom, nom et adresse de messagerie d’un compte d’utilisateur Azure Active Directory valid que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="488db-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="488db-218">Ajouter hello utilisateur tooa **groupe de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="488db-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="488db-219">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="488db-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="488db-220">Vous pouvez utiliser n’importe quel autre SpringCM utilisateur compte outil de création ou API fournie par SpringCM tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="488db-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="488db-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="488db-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="488db-222">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSpringCM.</span><span class="sxs-lookup"><span data-stu-id="488db-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="488db-224">**tooassign Britta Simon tooSpringCM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="488db-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="488db-225">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="488db-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="488db-227">Dans la liste des applications hello, sélectionnez **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="488db-227">In hello applications list, select **SpringCM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="488db-229">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="488db-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="488db-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="488db-231">Click **Add** button.</span></span> <span data-ttu-id="488db-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="488db-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="488db-234">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="488db-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="488db-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="488db-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="488db-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="488db-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="488db-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="488db-237">Testing single sign-on</span></span>

<span data-ttu-id="488db-238">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="488db-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="488db-239">Lorsque vous cliquez sur mosaïque SpringCM hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour SpringCM application.</span><span class="sxs-lookup"><span data-stu-id="488db-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="488db-240">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="488db-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="488db-241">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="488db-241">Additional resources</span></span>

* [<span data-ttu-id="488db-242">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="488db-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="488db-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="488db-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

