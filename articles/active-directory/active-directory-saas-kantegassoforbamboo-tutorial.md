---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour Bamboo | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Kantega SSO pour Bamboo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="e58f4-103">Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour Bamboo</span><span class="sxs-lookup"><span data-stu-id="e58f4-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="e58f4-104">Dans ce didacticiel, vous apprendrez comment toointegrate Kantega SSO pour Bamboo avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e58f4-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e58f4-105">Intégration Kantega SSO pour Bamboo avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e58f4-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e58f4-106">Vous pouvez contrôler dans Azure AD qui a accès tooKantega SSO pour Bamboo</span><span class="sxs-lookup"><span data-stu-id="e58f4-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="e58f4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKantega SSO pour Bamboo (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e58f4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e58f4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e58f4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e58f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e58f4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e58f4-110">Prerequisites</span></span>

<span data-ttu-id="e58f4-111">tooconfigure intégration d’Azure AD avec Kantega SSO pour Bamboo, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e58f4-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="e58f4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e58f4-113">Un abonnement Kantega SSO pour Bamboo pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e58f4-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e58f4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e58f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e58f4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e58f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e58f4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e58f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e58f4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e58f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e58f4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e58f4-118">Scenario description</span></span>
<span data-ttu-id="e58f4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e58f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e58f4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e58f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e58f4-121">Ajout de Kantega SSO pour Bamboo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e58f4-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="e58f4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="e58f4-123">Ajout de Kantega SSO pour Bamboo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e58f4-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="e58f4-124">intégration de hello tooconfigure de Kantega SSO pour Bamboo dans Azure AD, vous devez tooadd Kantega SSO pour Bamboo à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e58f4-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e58f4-125">**tooadd Kantega SSO pour Bamboo à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58f4-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58f4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e58f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e58f4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e58f4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e58f4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e58f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e58f4-133">Dans la zone de recherche de hello, tapez **Kantega SSO pour Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="e58f4-135">Dans le volet de résultats hello, sélectionnez **Kantega SSO pour Bamboo**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e58f4-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e58f4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e58f4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kantega SSO pour Bamboo sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e58f4-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e58f4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Kantega SSO pour Bamboo est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e58f4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="e58f4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Kantega SSO pour Bamboo doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e58f4-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="e58f4-141">Dans Kantega SSO pour Bamboo, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e58f4-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e58f4-142">tooconfigure et test Azure AD l’authentification unique avec Kantega SSO pour Bamboo, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e58f4-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e58f4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e58f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e58f4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e58f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e58f4-145">**[Création d’un Kantega SSO pour tester un utilisateur Bamboo](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave un équivalent de Britta Simon dans Kantega SSO pour Bamboo est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e58f4-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e58f4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e58f4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e58f4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e58f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e58f4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e58f4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Kantega SSO pour les applications Bamboo.</span><span class="sxs-lookup"><span data-stu-id="e58f4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="e58f4-150">**tooconfigure Azure AD l’authentification unique avec Kantega SSO pour Bamboo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58f4-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58f4-151">Bonjour portail Azure, sur hello **Kantega SSO pour Bamboo** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e58f4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e58f4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="e58f4-155">Dans **IDP** initiée par le mode, hello **Kantega SSO pour Bamboo domaine et les URL** section effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="e58f4-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="e58f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-157">a.</span></span> <span data-ttu-id="e58f4-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e58f4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="e58f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-159">b.</span></span> <span data-ttu-id="e58f4-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e58f4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="e58f4-161">Dans **SP** mode initié, cocher **afficher les paramètres d’URL avancés** et effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="e58f4-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="e58f4-163">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e58f4-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e58f4-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e58f4-164">These values are not real.</span></span> <span data-ttu-id="e58f4-165">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="e58f4-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e58f4-166">Ces valeurs sont reçues lors de la configuration de hello du plug-in Bamboo qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="e58f4-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="e58f4-167">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e58f4-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="e58f4-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e58f4-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="e58f4-171">Dans une fenêtre de navigateur web, connectez-vous tooyour Bamboo sur le serveur local en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e58f4-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="e58f4-172">Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="e58f4-174">Sous l’onglet Modules complémentaires, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="e58f4-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="e58f4-175">Recherche **Kantega SSO pour Bamboo (SAML & Kerberos)** et cliquez sur **installer** bouton tooinstall hello nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="e58f4-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="e58f4-177">installation du plug-in Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="e58f4-177">hello plugin installation will start.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="e58f4-179">Une fois l’installation de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="e58f4-179">Once hello installation is complete.</span></span> <span data-ttu-id="e58f4-180">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-180">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="e58f4-182">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-182">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="e58f4-184">Cliquez sur **configurer** tooconfigure hello nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="e58f4-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="e58f4-186">Bonjour **SAML** section.</span><span class="sxs-lookup"><span data-stu-id="e58f4-186">In hello **SAML** section.</span></span> <span data-ttu-id="e58f4-187">Sélectionnez **Azure Active Directory (Azure AD)** de hello **ajouter le fournisseur d’identité** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="e58f4-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="e58f4-189">Sélectionnez le niveau d’abonnement **De base**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-189">Select subscription level as **Basic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="e58f4-191">Sur hello **propriétés de l’application** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58f4-191">On hello **App properties** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="e58f4-193">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-193">a.</span></span> <span data-ttu-id="e58f4-194">Hello de copie **URI ID d’application** valeur et l’utiliser en tant que **identificateur, les URL de réponse et les URL de connexion** sur hello **Kantega SSO pour Bamboo domaine et les URL** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e58f4-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="e58f4-195">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-195">b.</span></span> <span data-ttu-id="e58f4-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-196">Click **Next**.</span></span>

17. <span data-ttu-id="e58f4-197">Sur hello **importation de métadonnées** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58f4-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="e58f4-199">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-199">a.</span></span> <span data-ttu-id="e58f4-200">Sélectionnez **Metadata file on my computer** (Fichier de métadonnées sur mon ordinateur), puis chargez le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e58f4-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="e58f4-201">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-201">b.</span></span> <span data-ttu-id="e58f4-202">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-202">Click **Next**.</span></span>

18. <span data-ttu-id="e58f4-203">Sur hello **nom et l’authentification unique emplacement** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58f4-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="e58f4-205">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-205">a.</span></span> <span data-ttu-id="e58f4-206">Ajoutez le nom du fournisseur d’identité de hello dans **nom de fournisseur d’identité** zone de texte (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e58f4-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="e58f4-207">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-207">b.</span></span> <span data-ttu-id="e58f4-208">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-208">Click **Next**.</span></span>

19. <span data-ttu-id="e58f4-209">Vérifier le certificat de signature hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="e58f4-211">Sur hello **des comptes d’utilisateur Bamboo** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58f4-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="e58f4-213">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-213">a.</span></span> <span data-ttu-id="e58f4-214">Sélectionnez **créer des utilisateurs dans l’annuaire interne de Bamboo si nécessaire** et entrez le nom de hello approprié du groupe de hello pour les utilisateurs (peut être non plusieurs.</span><span class="sxs-lookup"><span data-stu-id="e58f4-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="e58f4-215">groupes séparés par des virgules).</span><span class="sxs-lookup"><span data-stu-id="e58f4-215">of groups separated by comma).</span></span>

    <span data-ttu-id="e58f4-216">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-216">b.</span></span> <span data-ttu-id="e58f4-217">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-217">Click **Next**.</span></span>

21. <span data-ttu-id="e58f4-218">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-218">Click **Finish**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="e58f4-220">Sur hello **connu des domaines pour Azure AD** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58f4-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="e58f4-222">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-222">a.</span></span> <span data-ttu-id="e58f4-223">Sélectionnez **connu domaines** à partir du Panneau de gauche hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="e58f4-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="e58f4-224">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-224">b.</span></span> <span data-ttu-id="e58f4-225">Entrez le nom de domaine Bonjour **connu domaines** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e58f4-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="e58f4-226">c.</span><span class="sxs-lookup"><span data-stu-id="e58f4-226">c.</span></span> <span data-ttu-id="e58f4-227">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e58f4-228">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e58f4-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e58f4-229">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e58f4-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e58f4-230">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e58f4-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e58f4-231">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="e58f4-232">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e58f4-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e58f4-234">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58f4-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58f4-235">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e58f4-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e58f4-237">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e58f4-239">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e58f4-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e58f4-241">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58f4-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e58f4-243">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-243">a.</span></span> <span data-ttu-id="e58f4-244">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e58f4-245">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-245">b.</span></span> <span data-ttu-id="e58f4-246">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e58f4-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e58f4-247">c.</span><span class="sxs-lookup"><span data-stu-id="e58f4-247">c.</span></span> <span data-ttu-id="e58f4-248">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e58f4-249">d.</span><span class="sxs-lookup"><span data-stu-id="e58f4-249">d.</span></span> <span data-ttu-id="e58f4-250">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="e58f4-251">Création d’un utilisateur de test Kantega SSO pour Bamboo</span><span class="sxs-lookup"><span data-stu-id="e58f4-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="e58f4-252">tooenable Azure AD les utilisateurs toolog dans tooBamboo, vous devez les configurer dans Bamboo.</span><span class="sxs-lookup"><span data-stu-id="e58f4-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="e58f4-253">Dans Kantega SSO pour Bamboo, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e58f4-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="e58f4-254">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58f4-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58f4-255">Ouvrez une session dans tooyour Bamboo sur le serveur local en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e58f4-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="e58f4-256">Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-256">Hover on cog and click hello **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="e58f4-258">Cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-258">Click **Users**.</span></span> <span data-ttu-id="e58f4-259">Sous hello **ajouter un utilisateur** section, effectuez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e58f4-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="e58f4-261">a.</span><span class="sxs-lookup"><span data-stu-id="e58f4-261">a.</span></span> <span data-ttu-id="e58f4-262">Bonjour **nom d’utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e58f4-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="e58f4-263">b.</span><span class="sxs-lookup"><span data-stu-id="e58f4-263">b.</span></span> <span data-ttu-id="e58f4-264">Bonjour **mot de passe** zone de texte, un mot de passe hello type d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e58f4-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="e58f4-265">c.</span><span class="sxs-lookup"><span data-stu-id="e58f4-265">c.</span></span> <span data-ttu-id="e58f4-266">Bonjour **confirmer le mot de passe** zone de texte, entrez à nouveau hello mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e58f4-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="e58f4-267">d.</span><span class="sxs-lookup"><span data-stu-id="e58f4-267">d.</span></span> <span data-ttu-id="e58f4-268">Bonjour **nom complet** zone de texte, nom complet du type d’utilisateur hello comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e58f4-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="e58f4-269">e.</span><span class="sxs-lookup"><span data-stu-id="e58f4-269">e.</span></span> <span data-ttu-id="e58f4-270">Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e58f4-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="e58f4-271">f.</span><span class="sxs-lookup"><span data-stu-id="e58f4-271">f.</span></span> <span data-ttu-id="e58f4-272">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e58f4-273">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58f4-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e58f4-274">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKantega SSO pour Bamboo.</span><span class="sxs-lookup"><span data-stu-id="e58f4-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e58f4-276">**tooassign Britta Simon tooKantega SSO pour Bamboo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58f4-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58f4-277">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e58f4-279">Dans la liste des applications hello, sélectionnez **Kantega SSO pour Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="e58f4-281">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e58f4-283">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-283">Click **Add** button.</span></span> <span data-ttu-id="e58f4-284">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e58f4-286">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e58f4-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e58f4-287">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e58f4-288">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e58f4-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e58f4-289">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e58f4-289">Testing single sign-on</span></span>

<span data-ttu-id="e58f4-290">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e58f4-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e58f4-291">Lorsque vous cliquez sur hello Kantega SSO pour vignette Bamboo Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Kantega SSO pour l’application de Bamboo.</span><span class="sxs-lookup"><span data-stu-id="e58f4-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="e58f4-292">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e58f4-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e58f4-293">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e58f4-293">Additional resources</span></span>

* [<span data-ttu-id="e58f4-294">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e58f4-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e58f4-295">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e58f4-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

