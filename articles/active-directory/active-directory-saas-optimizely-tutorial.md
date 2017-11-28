---
title: "Didacticiel : Intégration d’Azure Active Directory à Optimizely |Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="5c50b-103">Didacticiel : Intégration d’Azure Active Directory avec Optimizely</span><span class="sxs-lookup"><span data-stu-id="5c50b-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="5c50b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Optimizely avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c50b-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c50b-105">Intégration Optimizely à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5c50b-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c50b-106">Vous pouvez contrôler dans Azure AD qui a accès tooOptimizely</span><span class="sxs-lookup"><span data-stu-id="5c50b-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="5c50b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOptimizely (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c50b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5c50b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c50b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c50b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c50b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5c50b-110">Prerequisites</span></span>

<span data-ttu-id="5c50b-111">tooconfigure intégration d’Azure AD avec Optimizely, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5c50b-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="5c50b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c50b-113">Un abonnement Optimizely pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5c50b-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c50b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5c50b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c50b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5c50b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c50b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5c50b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c50b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c50b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c50b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5c50b-118">Scenario description</span></span>
<span data-ttu-id="5c50b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5c50b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c50b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5c50b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c50b-121">Ajout de Optimizely à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5c50b-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="5c50b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="5c50b-123">Ajout de Optimizely à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5c50b-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="5c50b-124">intégration de hello tooconfigure de Optimizely dans Azure AD, vous devez tooadd Optimizely à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5c50b-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c50b-125">**tooadd Optimizely à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c50b-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c50b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5c50b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c50b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c50b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5c50b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5c50b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5c50b-133">Dans la zone de recherche de hello, tapez **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-133">In hello search box, type **Optimizely**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="5c50b-135">Dans le volet de résultats hello, sélectionnez **Optimizely**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5c50b-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c50b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c50b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Optimizely avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5c50b-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c50b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Optimizely est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c50b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="5c50b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Optimizely doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5c50b-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="5c50b-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Optimizely.</span><span class="sxs-lookup"><span data-stu-id="5c50b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="5c50b-142">tooconfigure et test Azure AD l’authentification unique avec Optimizely, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5c50b-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c50b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5c50b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c50b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c50b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c50b-145">**[Création d’un utilisateur de test Optimizely](#creating-an-optimizely-test-user)**  -toohave un équivalent de Britta Simon dans Optimizely est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5c50b-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c50b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c50b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c50b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5c50b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c50b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c50b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Optimizely.</span><span class="sxs-lookup"><span data-stu-id="5c50b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="5c50b-150">**tooconfigure Azure AD single sign-on avec Optimizely, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c50b-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c50b-151">Bonjour portail Azure, sur hello **Optimizely** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5c50b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c50b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="5c50b-155">Sur hello **Optimizely domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c50b-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="5c50b-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c50b-157">a.</span></span> <span data-ttu-id="5c50b-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="5c50b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="5c50b-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c50b-159">b.</span></span> <span data-ttu-id="5c50b-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="5c50b-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c50b-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="5c50b-161">These values are not hello real.</span></span> <span data-ttu-id="5c50b-162">Vous mettrez à jour la valeur de hello avec l’URL de connexion réel hello et identificateur, qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="5c50b-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="5c50b-163">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5c50b-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="5c50b-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5c50b-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c50b-167">Sur hello **Optimizely Configuration** , cliquez sur **Optimizely de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5c50b-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5c50b-168">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5c50b-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="5c50b-170">tooconfigure l’authentification unique sur **Optimizely** côté, contactez votre responsable de compte Optimizely et fournissez hello téléchargé **certificat (Base64)**, et **SAML Sign-On URL du Service unique** .</span><span class="sxs-lookup"><span data-stu-id="5c50b-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="5c50b-171">Par courrier électronique de réponse tooyour, Optimizely vous offre hello URL de connexion (l’authentification unique initiée par le Service Pack) et hello des valeurs d’identificateur (ID d’entité fournisseur de Service).</span><span class="sxs-lookup"><span data-stu-id="5c50b-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="5c50b-172">a.</span><span class="sxs-lookup"><span data-stu-id="5c50b-172">a.</span></span> <span data-ttu-id="5c50b-173">Hello de copie **URL d’authentification unique initiée par SP** fourni par Optimizely, puis coller dans hello **URL de connexion** zone de texte dans **Optimizely domaine et les URL** section sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5c50b-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="5c50b-174">b.</span><span class="sxs-lookup"><span data-stu-id="5c50b-174">b.</span></span> <span data-ttu-id="5c50b-175">Hello de copie **ID d’entité de fournisseur de Service** fourni par Optimizely, puis coller dans hello **identificateur** zone de texte dans **Optimizely domaine et les URL** section sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5c50b-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="5c50b-176">Dans une autre fenêtre de navigateur, l’authentification tooyour Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="5c50b-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="5c50b-177">Cliquez sur vous nom du compte dans la partie supérieure de hello coin supérieur droit, puis **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Authentification unique Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="5c50b-179">Dans l’onglet compte hello hello case **activez SSO** sous Single Sign On Bonjour **vue d’ensemble** section.</span><span class="sxs-lookup"><span data-stu-id="5c50b-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Authentification unique Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="5c50b-181">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="5c50b-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5c50b-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c50b-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5c50b-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c50b-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c50b-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c50b-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c50b-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5c50b-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5c50b-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c50b-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c50b-189">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5c50b-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c50b-191">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c50b-193">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5c50b-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c50b-195">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c50b-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c50b-197">a.</span><span class="sxs-lookup"><span data-stu-id="5c50b-197">a.</span></span> <span data-ttu-id="5c50b-198">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c50b-199">b.</span><span class="sxs-lookup"><span data-stu-id="5c50b-199">b.</span></span> <span data-ttu-id="5c50b-200">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c50b-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="5c50b-201">c.</span><span class="sxs-lookup"><span data-stu-id="5c50b-201">c.</span></span> <span data-ttu-id="5c50b-202">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c50b-203">d.</span><span class="sxs-lookup"><span data-stu-id="5c50b-203">d.</span></span> <span data-ttu-id="5c50b-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="5c50b-205">Création d’un utilisateur de test Optimizely</span><span class="sxs-lookup"><span data-stu-id="5c50b-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="5c50b-206">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Optimizely.</span><span class="sxs-lookup"><span data-stu-id="5c50b-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="5c50b-207">Sur la page d’accueil hello, sélectionnez **collaborateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="5c50b-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="5c50b-208">tooadd collaborateur toohello projet, cliquez sur **nouveau collaborateur**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="5c50b-210">Adresse de messagerie hello et attribuez-leur un rôle.</span><span class="sxs-lookup"><span data-stu-id="5c50b-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="5c50b-211">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-211">Click **Invite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="5c50b-213">Il reçoit une invitation par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="5c50b-213">They receive an email invite.</span></span> <span data-ttu-id="5c50b-214">À l’aide d’adresse de messagerie hello, ils ont toolog dans tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="5c50b-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c50b-215">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c50b-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c50b-216">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="5c50b-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5c50b-218">**tooassign Britta Simon tooOptimizely, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c50b-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c50b-219">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5c50b-221">Dans la liste des applications hello, sélectionnez **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-221">In hello applications list, select **Optimizely**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="5c50b-223">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5c50b-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-225">Click **Add** button.</span></span> <span data-ttu-id="5c50b-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5c50b-228">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5c50b-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c50b-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c50b-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c50b-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c50b-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5c50b-231">Testing single sign-on</span></span>

<span data-ttu-id="5c50b-232">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5c50b-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c50b-233">Lorsque vous cliquez sur mosaïque Optimizely hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="5c50b-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c50b-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5c50b-234">Additional resources</span></span>

* [<span data-ttu-id="5c50b-235">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c50b-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c50b-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5c50b-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

