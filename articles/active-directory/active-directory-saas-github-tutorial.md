---
title: "Didacticiel : Intégration d’Azure Active Directory à GitHub | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="06bc6-103">Didacticiel : Intégration d’Azure Active Directory à GitHub</span><span class="sxs-lookup"><span data-stu-id="06bc6-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="06bc6-104">Dans ce didacticiel, vous apprendrez comment toointegrate GitHub avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06bc6-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06bc6-105">Intégration de GitHub à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="06bc6-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06bc6-106">Vous pouvez contrôler dans Azure AD qui a accès tooGitHub</span><span class="sxs-lookup"><span data-stu-id="06bc6-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="06bc6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooGitHub (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06bc6-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="06bc6-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="06bc6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06bc6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06bc6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="06bc6-110">Prerequisites</span></span>

<span data-ttu-id="06bc6-111">tooconfigure intégration d’Azure AD à GitHub, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="06bc6-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="06bc6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06bc6-113">Un abonnement GitHub pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="06bc6-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="06bc6-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="06bc6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="06bc6-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="06bc6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06bc6-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06bc6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="06bc6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06bc6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="06bc6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="06bc6-118">Scenario description</span></span>
<span data-ttu-id="06bc6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="06bc6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06bc6-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="06bc6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06bc6-121">Ajout de GitHub à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="06bc6-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="06bc6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="06bc6-123">Ajout de GitHub à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="06bc6-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="06bc6-124">tooconfigure hello intégration de GitHub dans Azure AD, vous devez tooadd GitHub à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="06bc6-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06bc6-125">**tooadd GitHub à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06bc6-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc6-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="06bc6-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06bc6-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06bc6-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="06bc6-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="06bc6-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="06bc6-133">Dans la zone de recherche de hello, tapez **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-133">In hello search box, type **GitHub.com**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="06bc6-135">Dans le volet de résultats hello, sélectionnez **GitHub**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="06bc6-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06bc6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06bc6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec GitHub, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="06bc6-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="06bc6-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans GitHub est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06bc6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="06bc6-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans GitHub doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="06bc6-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="06bc6-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="06bc6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="06bc6-142">tooconfigure et test Azure AD l’authentification unique avec GitHub, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="06bc6-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06bc6-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="06bc6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06bc6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06bc6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06bc6-145">**[Création d’un utilisateur de test GitHub](#creating-a-GitHub-test-user)**  -toohave de Britta Simon dans GitHub qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="06bc6-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="06bc6-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="06bc6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06bc6-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="06bc6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06bc6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06bc6-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application de GitHub.</span><span class="sxs-lookup"><span data-stu-id="06bc6-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="06bc6-150">**tooconfigure Azure AD single sign-on avec GitHub, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06bc6-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc6-151">Dans le portail de gestion Azure hello, sur hello **GitHub** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="06bc6-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="06bc6-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="06bc6-155">Sur hello **GitHub domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="06bc6-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="06bc6-157">a.</span><span class="sxs-lookup"><span data-stu-id="06bc6-157">a.</span></span> <span data-ttu-id="06bc6-158">Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="06bc6-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="06bc6-159">b.</span><span class="sxs-lookup"><span data-stu-id="06bc6-159">b.</span></span> <span data-ttu-id="06bc6-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="06bc6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06bc6-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="06bc6-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="06bc6-162">Vous avez tooupdate ces valeurs avec hello réel chanter sur URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="06bc6-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="06bc6-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="06bc6-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="06bc6-164">Accédez à tooGitHub Admin section tooretrieve ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="06bc6-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="06bc6-165">Sur hello **attributs utilisateur** section, sélectionnez **identificateur de l’utilisateur** comme user.mail.</span><span class="sxs-lookup"><span data-stu-id="06bc6-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="06bc6-167">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="06bc6-169">Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="06bc6-170">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-170">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="06bc6-172">Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="06bc6-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="06bc6-174">Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="06bc6-176">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="06bc6-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="06bc6-178">Sur hello **GitHub Configuration** , cliquez sur **configurer GitHub** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="06bc6-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="06bc6-181">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise GitHub en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="06bc6-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="06bc6-182">Accédez trop**paramètres** et cliquez sur **sécurité**</span><span class="sxs-lookup"><span data-stu-id="06bc6-182">Navigate too**Settings** and click **Security**</span></span>

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="06bc6-184">Vérifiez hello **activer l’authentification SAML** zone, révélant hello Single Sign-on configuration les champs.</span><span class="sxs-lookup"><span data-stu-id="06bc6-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="06bc6-185">Ensuite, utilisez hello unique authentification URL valeur tooupdate hello unique URL de connexion sur la configuration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06bc6-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="06bc6-187">Configurer hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="06bc6-187">Configure hello following fields:</span></span>

    <span data-ttu-id="06bc6-188">a.</span><span class="sxs-lookup"><span data-stu-id="06bc6-188">a.</span></span> <span data-ttu-id="06bc6-189">**URL de connexion**: entrez **SAML SSO Service URL** de hello **configurer GitHub** section sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="06bc6-190">b.</span><span class="sxs-lookup"><span data-stu-id="06bc6-190">b.</span></span> <span data-ttu-id="06bc6-191">**Émetteur**: entrez **ID d’entité SAML** de hello **configurer GitHub** section sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="06bc6-192">c.</span><span class="sxs-lookup"><span data-stu-id="06bc6-192">c.</span></span> <span data-ttu-id="06bc6-193">**Certificat public**: hello ouvrir téléchargé le certificat à partir d’Azure AD dans un contenu hello bloc-notes, puis copiez notamment « BEGIN CERTIFICATE » et « END CERTIFICATE »</span><span class="sxs-lookup"><span data-stu-id="06bc6-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="06bc6-195">Cliquez sur **configuration SAML du Test** tooconfirm qui aucune des échecs de validation ou des erreurs lors de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="06bc6-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="06bc6-197">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06bc6-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="06bc6-199">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06bc6-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="06bc6-201">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06bc6-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc6-202">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="06bc6-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06bc6-204">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="06bc6-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06bc6-206">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="06bc6-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06bc6-208">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="06bc6-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06bc6-210">a.</span><span class="sxs-lookup"><span data-stu-id="06bc6-210">a.</span></span> <span data-ttu-id="06bc6-211">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06bc6-212">b.</span><span class="sxs-lookup"><span data-stu-id="06bc6-212">b.</span></span> <span data-ttu-id="06bc6-213">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="06bc6-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06bc6-214">c.</span><span class="sxs-lookup"><span data-stu-id="06bc6-214">c.</span></span> <span data-ttu-id="06bc6-215">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="06bc6-216">d.</span><span class="sxs-lookup"><span data-stu-id="06bc6-216">d.</span></span> <span data-ttu-id="06bc6-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="06bc6-218">Création d’un utilisateur de test GitHub</span><span class="sxs-lookup"><span data-stu-id="06bc6-218">Creating a GitHub test user</span></span>

<span data-ttu-id="06bc6-219">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans GitHub, ils doivent être configurés dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="06bc6-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="06bc6-220">Dans les cas de hello de GitHub, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="06bc6-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="06bc6-221">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06bc6-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc6-222">Ouvrez une session dans tooyour GitHub site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="06bc6-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="06bc6-223">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-223">Click **People**.</span></span>

    <span data-ttu-id="06bc6-224">![Personnes](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="06bc6-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="06bc6-225">Cliquez sur **Invite member**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-225">Click **Invite member**.</span></span>

    <span data-ttu-id="06bc6-226">![Inviter des utilisateurs](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "inviter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="06bc6-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="06bc6-227">Sur hello **invitation membre** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="06bc6-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="06bc6-228">a.</span><span class="sxs-lookup"><span data-stu-id="06bc6-228">a.</span></span> <span data-ttu-id="06bc6-229">Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06bc6-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="06bc6-230">![Inviter des personnes](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "inviter des personnes")</span><span class="sxs-lookup"><span data-stu-id="06bc6-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="06bc6-231">b.</span><span class="sxs-lookup"><span data-stu-id="06bc6-231">b.</span></span> <span data-ttu-id="06bc6-232">Cliquez sur **Send Invitation**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="06bc6-233">![Inviter des personnes](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "inviter des personnes")</span><span class="sxs-lookup"><span data-stu-id="06bc6-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="06bc6-234">titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="06bc6-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="06bc6-235">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc6-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="06bc6-236">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooGitHub de son accès.</span><span class="sxs-lookup"><span data-stu-id="06bc6-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="06bc6-238">**tooassign Britta Simon tooGitHub, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06bc6-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc6-239">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="06bc6-241">Dans la liste des applications hello, sélectionnez **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="06bc6-243">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="06bc6-245">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-245">Click **Add** button.</span></span> <span data-ttu-id="06bc6-246">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="06bc6-248">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="06bc6-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06bc6-249">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06bc6-250">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="06bc6-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="06bc6-251">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="06bc6-251">Testing single sign-on</span></span>

<span data-ttu-id="06bc6-252">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="06bc6-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="06bc6-253">Lorsque vous cliquez sur mosaïque GitHub hello hello volet d’accès, vous devez obtenir tooyour connecté GitHub application.</span><span class="sxs-lookup"><span data-stu-id="06bc6-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="06bc6-254">Vous allez être journalisation comme un compte d’organisation mais puis besoin toolog avec votre compte personnel.</span><span class="sxs-lookup"><span data-stu-id="06bc6-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="06bc6-255">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="06bc6-255">Additional resources</span></span>

* [<span data-ttu-id="06bc6-256">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06bc6-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06bc6-257">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="06bc6-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
