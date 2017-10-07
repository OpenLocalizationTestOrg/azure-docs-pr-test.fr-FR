---
title: "Didacticiel : Intégration d’Azure Active Directory à Birst Agile Business Analytics | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Birst Agile Business Analytique."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f007edcec0fb8ece215ab69f7ec7ca59ca34bddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="383e6-103">Didacticiel : Intégration d’Azure Active Directory à Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="383e6-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="383e6-104">Dans ce didacticiel, vous apprendrez comment toointegrate Birst Agile Business Analytique avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="383e6-104">In this tutorial, you learn how toointegrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="383e6-105">Intégration Birst Agile Business Analytique à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="383e6-105">Integrating Birst Agile Business Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="383e6-106">Vous pouvez contrôler dans Azure AD qui a accès tooBirst Agile Business Analytique</span><span class="sxs-lookup"><span data-stu-id="383e6-106">You can control in Azure AD who has access tooBirst Agile Business Analytics</span></span>
- <span data-ttu-id="383e6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBirst Agile Analytique d’entreprise (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-107">You can enable your users tooautomatically get signed-on tooBirst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="383e6-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="383e6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="383e6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="383e6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="383e6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="383e6-110">Prerequisites</span></span>

<span data-ttu-id="383e6-111">tooconfigure intégration d’Azure AD avec Birst Agile Business Analytique, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="383e6-111">tooconfigure Azure AD integration with Birst Agile Business Analytics, you need hello following items:</span></span>

- <span data-ttu-id="383e6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="383e6-113">Un abonnement Birst Agile Business Analytics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="383e6-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="383e6-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="383e6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="383e6-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="383e6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="383e6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="383e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="383e6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="383e6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="383e6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="383e6-118">Scenario description</span></span>
<span data-ttu-id="383e6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="383e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="383e6-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="383e6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="383e6-121">Ajout de Birst Agile Business Analytique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="383e6-121">Adding Birst Agile Business Analytics from hello gallery</span></span>
2. <span data-ttu-id="383e6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-hello-gallery"></a><span data-ttu-id="383e6-123">Ajout de Birst Agile Business Analytique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="383e6-123">Adding Birst Agile Business Analytics from hello gallery</span></span>
<span data-ttu-id="383e6-124">intégration de hello tooconfigure de Birst Agile Business Analytique dans Azure AD, vous devez tooadd Birst Agile Business Analytique à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="383e6-124">tooconfigure hello integration of Birst Agile Business Analytics into Azure AD, you need tooadd Birst Agile Business Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="383e6-125">**tooadd Birst Agile Business Analytique à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="383e6-125">**tooadd Birst Agile Business Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="383e6-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="383e6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="383e6-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="383e6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="383e6-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="383e6-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="383e6-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="383e6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="383e6-133">Dans la zone de recherche de hello, tapez **Birst Agile Business Analytique**.</span><span class="sxs-lookup"><span data-stu-id="383e6-133">In hello search box, type **Birst Agile Business Analytics**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="383e6-135">Dans le volet de résultats hello, sélectionnez **Birst Agile Business Analytique**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="383e6-135">In hello results panel, select **Birst Agile Business Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="383e6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="383e6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Birst Agile Business Analytics, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="383e6-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="383e6-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Birst Agile Business Analytique est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="383e6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Birst Agile Business Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="383e6-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Birst Agile Business Analytique doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="383e6-140">In other words, a link relationship between an Azure AD user and hello related user in Birst Agile Business Analytics needs toobe established.</span></span>

<span data-ttu-id="383e6-141">Dans Agile Analytique d’entreprise Birst, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="383e6-141">In Birst Agile Business Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="383e6-142">tooconfigure et test Azure AD l’authentification unique avec Birst Agile Business Analytique, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="383e6-142">tooconfigure and test Azure AD single sign-on with Birst Agile Business Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="383e6-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="383e6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="383e6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="383e6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="383e6-145">**[Création d’un utilisateur de test Birst Agile Business Analytique](#creating-a-birst-agile-business-analytics-test-user)**  -toohave un équivalent de Britta Simon dans Birst Agile Business Analytique est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="383e6-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - toohave a counterpart of Britta Simon in Birst Agile Business Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="383e6-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="383e6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="383e6-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="383e6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="383e6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="383e6-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Birst Agile Business Analytique.</span><span class="sxs-lookup"><span data-stu-id="383e6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="383e6-150">**tooconfigure Azure AD l’authentification unique avec Analytique d’entreprise Agile Birst, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="383e6-150">**tooconfigure Azure AD single sign-on with Birst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="383e6-151">Bonjour portail Azure, sur hello **Birst Agile Business Analytique** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="383e6-151">In hello Azure portal, on hello **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="383e6-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="383e6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="383e6-155">Sur hello **Birst Agile domaine Analytique et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="383e6-155">On hello **Birst Agile Business Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="383e6-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="383e6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="383e6-158">URL de Hello dépend hello de centre de données que votre compte Birst se trouve :</span><span class="sxs-lookup"><span data-stu-id="383e6-158">hello URL depends on hello datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="383e6-159">Pour une utilisation du centre de données États-Unis hello modèle :`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="383e6-159">For US datacenter use following hello pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="383e6-160">Pour l’Europe centre de données utilisez hello modèle :`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="383e6-160">For Europe datacenter use hello following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="383e6-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="383e6-161">This value is not real.</span></span> <span data-ttu-id="383e6-162">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="383e6-162">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="383e6-163">Contact [équipe de support Birst Agile Business Analytique Client](mailto:info@birst.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="383e6-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="383e6-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="383e6-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="383e6-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="383e6-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="383e6-168">Sur hello **Birst Agile Business Analytique Configuration** , cliquez sur **configurer Birst Agile Business Analytique** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="383e6-168">On hello **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="383e6-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="383e6-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="383e6-171">tooconfigure l’authentification unique sur **Birst Agile Business Analytique** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **URL de déconnexion, ID d’entité SAML et SAML Single Sign-On URL du service** trop[Birst Agile Business Analytique l’équipe de support](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="383e6-171">tooconfigure single sign-on on **Birst Agile Business Analytics** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="383e6-172">Indiquez équipe tooBirst que cette intégration doit algorithme SHA256 (SHA1 pas de support) afin que les développeurs peuvent définir hello SSO sur le serveur approprié de hello, tels que **app2101** etc..</span><span class="sxs-lookup"><span data-stu-id="383e6-172">Mention tooBirst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set hello SSO on hello appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="383e6-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="383e6-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="383e6-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="383e6-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="383e6-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="383e6-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="383e6-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="383e6-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="383e6-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="383e6-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="383e6-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="383e6-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="383e6-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="383e6-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="383e6-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="383e6-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="383e6-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="383e6-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="383e6-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="383e6-188">a.</span><span class="sxs-lookup"><span data-stu-id="383e6-188">a.</span></span> <span data-ttu-id="383e6-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="383e6-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="383e6-190">b.</span><span class="sxs-lookup"><span data-stu-id="383e6-190">b.</span></span> <span data-ttu-id="383e6-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="383e6-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="383e6-192">c.</span><span class="sxs-lookup"><span data-stu-id="383e6-192">c.</span></span> <span data-ttu-id="383e6-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="383e6-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="383e6-194">d.</span><span class="sxs-lookup"><span data-stu-id="383e6-194">d.</span></span> <span data-ttu-id="383e6-195">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="383e6-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="383e6-196">Création d’un utilisateur de test Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="383e6-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="383e6-197">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Birst Agile Business Analytique.</span><span class="sxs-lookup"><span data-stu-id="383e6-197">hello objective of this section is toocreate a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="383e6-198">Travailler avec [Birst Agile Business Analytique l’équipe de support](mailto:info@birst.com) utilisateurs hello tooadd hello Birst compte.</span><span class="sxs-lookup"><span data-stu-id="383e6-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) tooadd hello users in hello Birst account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="383e6-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="383e6-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="383e6-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBirst Agile Business Analytique.</span><span class="sxs-lookup"><span data-stu-id="383e6-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBirst Agile Business Analytics.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="383e6-202">**tooassign Britta Simon tooBirst Analytique d’entreprise Agile, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="383e6-202">**tooassign Britta Simon tooBirst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="383e6-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="383e6-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="383e6-205">Dans la liste des applications hello, sélectionnez **Birst Agile Business Analytique**.</span><span class="sxs-lookup"><span data-stu-id="383e6-205">In hello applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="383e6-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="383e6-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="383e6-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="383e6-209">Click **Add** button.</span></span> <span data-ttu-id="383e6-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="383e6-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="383e6-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="383e6-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="383e6-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="383e6-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="383e6-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="383e6-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="383e6-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="383e6-215">Testing single sign-on</span></span>

<span data-ttu-id="383e6-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="383e6-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="383e6-217">Lorsque vous cliquez sur hello Birst Agile Business Analytique vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de Birst Agile Business Analytique.</span><span class="sxs-lookup"><span data-stu-id="383e6-217">When you click hello Birst Agile Business Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="383e6-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="383e6-218">Additional resources</span></span>

* [<span data-ttu-id="383e6-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="383e6-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="383e6-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="383e6-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

