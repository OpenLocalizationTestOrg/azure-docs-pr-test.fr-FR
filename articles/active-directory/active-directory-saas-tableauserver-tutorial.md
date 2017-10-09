---
title: "Didacticiel : intégration d’Azure Active Directory à Tableau Server | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le serveur du Tableau."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="c29e8-103">Didacticiel : Intégration d’Azure Active Directory à Tableau Server</span><span class="sxs-lookup"><span data-stu-id="c29e8-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="c29e8-104">Dans ce didacticiel, vous apprendrez comment toointegrate Server Tableau avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c29e8-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c29e8-105">Intégration du serveur du Tableau à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c29e8-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c29e8-106">Vous pouvez contrôler dans Azure AD qui a accès tooTableau Server</span><span class="sxs-lookup"><span data-stu-id="c29e8-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="c29e8-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTableau Server (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c29e8-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c29e8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c29e8-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c29e8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c29e8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c29e8-110">Prerequisites</span></span>

<span data-ttu-id="c29e8-111">tooconfigure intégration d’Azure AD avec le serveur du Tableau, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c29e8-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="c29e8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c29e8-113">Un abonnement Tableau Server pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c29e8-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c29e8-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c29e8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c29e8-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c29e8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c29e8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c29e8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c29e8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c29e8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c29e8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c29e8-118">Scenario description</span></span>
<span data-ttu-id="c29e8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c29e8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c29e8-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c29e8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c29e8-121">Ajout du serveur de Tableau à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c29e8-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="c29e8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="c29e8-123">Ajout du serveur de Tableau à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c29e8-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="c29e8-124">tooconfigure hello intégration du serveur du Tableau dans Azure AD, vous devez tooadd serveur du Tableau à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c29e8-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c29e8-125">**tooadd serveur du Tableau à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c29e8-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c29e8-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c29e8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c29e8-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c29e8-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c29e8-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c29e8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c29e8-133">Dans la zone de recherche de hello, tapez **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-133">In hello search box, type **Tableau Server**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="c29e8-135">Dans le volet de résultats hello, sélectionnez **Tableau Server**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e8-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c29e8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c29e8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tableau Server grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c29e8-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c29e8-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le serveur du Tableau est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c29e8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="c29e8-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Tableau serveur hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c29e8-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="c29e8-141">Dans le serveur du Tableau, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c29e8-142">tooconfigure et test Azure AD l’authentification unique avec le serveur du Tableau, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c29e8-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c29e8-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c29e8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c29e8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c29e8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c29e8-145">**[Création d’un utilisateur de test du serveur du Tableau](#creating-a-tableau-server-test-user)**  -toohave un équivalent de Britta Simon dans le serveur de Tableau qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c29e8-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c29e8-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c29e8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c29e8-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c29e8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c29e8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c29e8-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de serveur du Tableau.</span><span class="sxs-lookup"><span data-stu-id="c29e8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="c29e8-150">**tooconfigure Azure AD-authentification avec le serveur du Tableau, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c29e8-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="c29e8-151">Bonjour portail Azure, sur hello **Tableau Server** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c29e8-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c29e8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="c29e8-155">Sur hello **URL et le domaine du serveur Tableau** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c29e8-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="c29e8-157">a.</span><span class="sxs-lookup"><span data-stu-id="c29e8-157">a.</span></span> <span data-ttu-id="c29e8-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="c29e8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="c29e8-159">b.</span><span class="sxs-lookup"><span data-stu-id="c29e8-159">b.</span></span> <span data-ttu-id="c29e8-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="c29e8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="c29e8-161">c.</span><span class="sxs-lookup"><span data-stu-id="c29e8-161">c.</span></span> <span data-ttu-id="c29e8-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="c29e8-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c29e8-163">Hello valeurs précédentes ne sont pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c29e8-163">hello preceding values are not real values.</span></span> <span data-ttu-id="c29e8-164">Une version ultérieure, mise à jour les valeurs hello avec URL réelle de hello et l’identificateur de la page de configuration du serveur du Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="c29e8-165">Application de serveur de tableau attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="c29e8-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c29e8-166">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c29e8-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="c29e8-167">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Attributs utilisateur »** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="c29e8-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="c29e8-168">Hello capture d’écran suivante montre un exemple de hello même.</span><span class="sxs-lookup"><span data-stu-id="c29e8-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="c29e8-170">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c29e8-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c29e8-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="c29e8-171">Attribute Name</span></span> | <span data-ttu-id="c29e8-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="c29e8-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="c29e8-173">username</span><span class="sxs-lookup"><span data-stu-id="c29e8-173">username</span></span> | <span data-ttu-id="c29e8-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="c29e8-174">*user.displayname*</span></span> |

    <span data-ttu-id="c29e8-175">a.</span><span class="sxs-lookup"><span data-stu-id="c29e8-175">a.</span></span> <span data-ttu-id="c29e8-176">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c29e8-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="c29e8-179">b.</span><span class="sxs-lookup"><span data-stu-id="c29e8-179">b.</span></span> <span data-ttu-id="c29e8-180">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c29e8-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c29e8-181">c.</span><span class="sxs-lookup"><span data-stu-id="c29e8-181">c.</span></span> <span data-ttu-id="c29e8-182">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c29e8-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c29e8-183">d.</span><span class="sxs-lookup"><span data-stu-id="c29e8-183">d.</span></span> <span data-ttu-id="c29e8-184">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-184">Click **Ok**</span></span>


6. <span data-ttu-id="c29e8-185">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c29e8-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="c29e8-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c29e8-187">Click **Save** button.</span></span>

    <span data-ttu-id="c29e8-188">![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="c29e8-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="c29e8-189">tooget SSO configuré pour votre application, vous devez tooyour toosign sur les clients de serveur du Tableau en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c29e8-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="c29e8-190">a.</span><span class="sxs-lookup"><span data-stu-id="c29e8-190">a.</span></span> <span data-ttu-id="c29e8-191">Dans la configuration du serveur du Tableau hello, cliquez sur hello **SAML** onglet.</span><span class="sxs-lookup"><span data-stu-id="c29e8-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="c29e8-193">b.</span><span class="sxs-lookup"><span data-stu-id="c29e8-193">b.</span></span> <span data-ttu-id="c29e8-194">Sélectionnez la case à cocher hello de **SAML d’utilisation pour l’authentification unique sur**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="c29e8-195">c.</span><span class="sxs-lookup"><span data-stu-id="c29e8-195">c.</span></span> <span data-ttu-id="c29e8-196">URL de renvoi du serveur du tableau : hello URL serveur du Tableau utilisateurs accéderont à, telles que http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="c29e8-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="c29e8-197">L’utilisation de l’URL http://localhost n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="c29e8-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="c29e8-198">L’utilisation d’une URL avec une barre oblique finale (par exemple, http://tableau_server/) n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c29e8-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="c29e8-199">Copie **URL de renvoi du serveur du Tableau** et collez-le tooAzure AD **URL de connexion** zone de texte dans **URL et le domaine du serveur Tableau** section.</span><span class="sxs-lookup"><span data-stu-id="c29e8-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="c29e8-200">d.</span><span class="sxs-lookup"><span data-stu-id="c29e8-200">d.</span></span> <span data-ttu-id="c29e8-201">ID d’entité SAML : ID d’entité hello identifie de façon unique votre toohello d’installation de serveur du Tableau IdP.</span><span class="sxs-lookup"><span data-stu-id="c29e8-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="c29e8-202">Vous pouvez entrer l’URL du serveur Tableau à nouveau ici, si vous le souhaitez, mais il n’a pas toobe URL du serveur de votre Tableau.</span><span class="sxs-lookup"><span data-stu-id="c29e8-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="c29e8-203">Copie **ID d’entité SAML** et collez-le tooAzure AD **identificateur** zone de texte dans **URL et le domaine du serveur Tableau** section.</span><span class="sxs-lookup"><span data-stu-id="c29e8-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="c29e8-204">e.</span><span class="sxs-lookup"><span data-stu-id="c29e8-204">e.</span></span> <span data-ttu-id="c29e8-205">Cliquez sur hello **exporter le fichier de métadonnées** et ouvrez-le dans l’application de l’éditeur de texte hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="c29e8-206">Localiser des URL de Service de consommateur Assertion avec Http Post et Index 0 et copier l’URL hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="c29e8-207">Maintenant collez-le tooAzure AD **URL de réponse** zone de texte dans **URL et le domaine du serveur Tableau** section.</span><span class="sxs-lookup"><span data-stu-id="c29e8-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="c29e8-208">f.</span><span class="sxs-lookup"><span data-stu-id="c29e8-208">f.</span></span> <span data-ttu-id="c29e8-209">Rechercher le fichier de métadonnées de fédération téléchargé à partir du portail Azure, puis le télécharger dans hello **fichier de métadonnées de fournisseur d’identité SAML**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="c29e8-210">g.</span><span class="sxs-lookup"><span data-stu-id="c29e8-210">g.</span></span> <span data-ttu-id="c29e8-211">Cliquez sur hello **OK** bouton dans la page de Configuration du serveur Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="c29e8-212">Client ont tooupload n’importe quel certificat dans la configuration de l’authentification unique SAML de Tableau serveur hello et sera obtenir ignoré Bonjour flux d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c29e8-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="c29e8-213">Si vous avez besoin d’aide configuration SAML sur le serveur du Tableau, consultez l’article de toothis [SAML de configurer](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="c29e8-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="c29e8-214">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c29e8-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c29e8-215">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c29e8-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c29e8-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c29e8-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="c29e8-218">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c29e8-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c29e8-220">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c29e8-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c29e8-221">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c29e8-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c29e8-223">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c29e8-225">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c29e8-227">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c29e8-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c29e8-229">a.</span><span class="sxs-lookup"><span data-stu-id="c29e8-229">a.</span></span> <span data-ttu-id="c29e8-230">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c29e8-231">b.</span><span class="sxs-lookup"><span data-stu-id="c29e8-231">b.</span></span> <span data-ttu-id="c29e8-232">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c29e8-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c29e8-233">c.</span><span class="sxs-lookup"><span data-stu-id="c29e8-233">c.</span></span> <span data-ttu-id="c29e8-234">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c29e8-235">d.</span><span class="sxs-lookup"><span data-stu-id="c29e8-235">d.</span></span> <span data-ttu-id="c29e8-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="c29e8-237">Création d’un utilisateur de test Tableau Server</span><span class="sxs-lookup"><span data-stu-id="c29e8-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="c29e8-238">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans le serveur du Tableau.</span><span class="sxs-lookup"><span data-stu-id="c29e8-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="c29e8-239">Vous devez tooprovision tous les utilisateurs de hello du serveur du Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="c29e8-240">Ce nom d’utilisateur de l’utilisateur de hello doit correspondre à valeur hello que vous avez configurée dans l’attribut personnalisé de hello Azure AD de **nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="c29e8-241">Avec hello correct de mappage de l’intégration hello doit fonctionner [configuration Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c29e8-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="c29e8-242">Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’administrateur de serveur du Tableau toocontact hello dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c29e8-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c29e8-243">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c29e8-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c29e8-244">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTableau Server.</span><span class="sxs-lookup"><span data-stu-id="c29e8-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c29e8-246">**tooassign Britta Simon tooTableau Server, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c29e8-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="c29e8-247">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c29e8-249">Dans la liste des applications hello, sélectionnez **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="c29e8-251">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c29e8-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-253">Click **Add** button.</span></span> <span data-ttu-id="c29e8-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c29e8-256">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c29e8-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c29e8-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c29e8-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c29e8-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c29e8-259">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c29e8-259">Testing single sign-on</span></span>

<span data-ttu-id="c29e8-260">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c29e8-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c29e8-261">Lorsque vous cliquez sur vignette de Tableau serveur hello Bonjour volet d’accès, vous devez obtenir l’application de serveur du Tableau tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="c29e8-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="c29e8-262">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c29e8-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c29e8-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c29e8-263">Additional resources</span></span>

* [<span data-ttu-id="c29e8-264">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c29e8-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c29e8-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c29e8-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

