---
title: "Didacticiel : Intégration d’Azure Active Directory avec Lucidchart | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="a9bfa-103">Didacticiel : Intégration d’Azure Active Directory à Lucidchart</span><span class="sxs-lookup"><span data-stu-id="a9bfa-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="a9bfa-104">Dans ce didacticiel, vous apprendrez comment toointegrate Lucidchart avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9bfa-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9bfa-105">Intégration de Lucidchart à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a9bfa-106">Vous pouvez contrôler dans Azure AD qui a accès tooLucidchart</span><span class="sxs-lookup"><span data-stu-id="a9bfa-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="a9bfa-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLucidchart (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9bfa-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a9bfa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a9bfa-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9bfa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9bfa-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a9bfa-110">Prerequisites</span></span>

<span data-ttu-id="a9bfa-111">tooconfigure intégration d’Azure AD à Lucidchart, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="a9bfa-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9bfa-113">Un abonnement Lucidchart pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a9bfa-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9bfa-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9bfa-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9bfa-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9bfa-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9bfa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9bfa-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a9bfa-118">Scenario description</span></span>
<span data-ttu-id="a9bfa-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9bfa-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9bfa-121">Ajout de Lucidchart à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a9bfa-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="a9bfa-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="a9bfa-123">Ajout de Lucidchart à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a9bfa-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="a9bfa-124">intégration de hello tooconfigure de Lucidchart dans Azure AD, vous devez tooadd Lucidchart à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a9bfa-125">**tooadd Lucidchart à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9bfa-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9bfa-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9bfa-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a9bfa-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a9bfa-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a9bfa-133">Dans la zone de recherche de hello, tapez **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-133">In hello search box, type **Lucidchart**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="a9bfa-135">Dans le volet de résultats hello, sélectionnez **Lucidchart**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9bfa-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9bfa-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lucidchart à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a9bfa-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9bfa-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Lucidchart est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="a9bfa-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Lucidchart doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="a9bfa-141">Dans Lucidchart, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a9bfa-142">tooconfigure et test Azure AD l’authentification unique avec Lucidchart, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a9bfa-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a9bfa-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9bfa-145">**[Création d’un utilisateur de test de Lucidchart](#creating-a-lucidchart-test-user)**  -toohave un équivalent de Britta Simon dans Lucidchart est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9bfa-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9bfa-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9bfa-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9bfa-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="a9bfa-150">**tooconfigure Azure AD single sign-on avec Lucidchart, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9bfa-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9bfa-151">Bonjour portail Azure, sur hello **Lucidchart** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a9bfa-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="a9bfa-155">Sur hello **Lucidchart domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="a9bfa-157">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="a9bfa-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="a9bfa-158">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="a9bfa-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a9bfa-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a9bfa-162">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Lucidchart en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="a9bfa-163">Dans le menu hello haut de hello, cliquez sur **Team**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="a9bfa-164">![Équipe](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Équipe")</span><span class="sxs-lookup"><span data-stu-id="a9bfa-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="a9bfa-165">Cliquez sur **Applications \> Gérer SAML**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="a9bfa-166">![Gérer SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Gérer SAML")</span><span class="sxs-lookup"><span data-stu-id="a9bfa-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="a9bfa-167">Sur hello **paramètres d’authentification SAML** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9bfa-168">a.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-168">a.</span></span> <span data-ttu-id="a9bfa-169">Sélectionnez **Enable SAML Authentication**, puis cliquez sur **Optional**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="a9bfa-170">![Paramètres d’authentification SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Paramètres d’authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="a9bfa-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="a9bfa-171">b.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-171">b.</span></span> <span data-ttu-id="a9bfa-172">Bonjour **domaine** zone de texte, tapez votre domaine, puis cliquez sur **modifier le certificat**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="a9bfa-173">![Modifier le certificat](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Modifier le certificat")</span><span class="sxs-lookup"><span data-stu-id="a9bfa-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="a9bfa-174">c.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-174">c.</span></span> <span data-ttu-id="a9bfa-175">Ouvrez votre fichier de métadonnées téléchargé, les hello copie contenu, puis collez-le dans hello **télécharger les métadonnées** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="a9bfa-176">![Charger les métadonnées](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Charger les métadonnées")</span><span class="sxs-lookup"><span data-stu-id="a9bfa-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="a9bfa-177">d.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-177">d.</span></span> <span data-ttu-id="a9bfa-178">Sélectionnez **ajouter automatiquement une nouvelle équipe de toohello utilisateurs**, puis cliquez sur **enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="a9bfa-179">![Enregistrer les modifications](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Enregistrer les modifications")</span><span class="sxs-lookup"><span data-stu-id="a9bfa-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="a9bfa-180">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a9bfa-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a9bfa-181">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a9bfa-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9bfa-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9bfa-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9bfa-184">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a9bfa-186">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9bfa-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9bfa-187">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9bfa-189">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9bfa-191">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9bfa-193">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9bfa-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9bfa-195">a.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-195">a.</span></span> <span data-ttu-id="a9bfa-196">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9bfa-197">b.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-197">b.</span></span> <span data-ttu-id="a9bfa-198">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9bfa-199">c.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-199">c.</span></span> <span data-ttu-id="a9bfa-200">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a9bfa-201">d.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-201">d.</span></span> <span data-ttu-id="a9bfa-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="a9bfa-203">Création d’un utilisateur de test Lucidchart</span><span class="sxs-lookup"><span data-stu-id="a9bfa-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="a9bfa-204">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="a9bfa-205">Quand un utilisateur affecté tente de toolog à Lucidchart à l’aide du volet d’accès hello, Lucidchart vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="a9bfa-206">Si aucun compte d’utilisateur n’est disponible, Lucidchart le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a9bfa-207">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9bfa-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a9bfa-208">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a9bfa-210">**tooassign Britta Simon tooLucidchart, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9bfa-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9bfa-211">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a9bfa-213">Dans la liste des applications hello, sélectionnez **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="a9bfa-215">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a9bfa-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-217">Click **Add** button.</span></span> <span data-ttu-id="a9bfa-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a9bfa-220">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a9bfa-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9bfa-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9bfa-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a9bfa-223">Testing single sign-on</span></span>

<span data-ttu-id="a9bfa-224">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a9bfa-225">Lorsque vous cliquez sur mosaïque Lucidchart hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Lucidchart application.</span><span class="sxs-lookup"><span data-stu-id="a9bfa-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="a9bfa-226">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9bfa-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9bfa-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a9bfa-227">Additional resources</span></span>

* [<span data-ttu-id="a9bfa-228">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9bfa-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9bfa-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a9bfa-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

