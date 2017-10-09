---
title: "Didacticiel : Intégration d’Azure Active Directory à Slack | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la marge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="8c27d-103">Didacticiel : Intégration d’Azure AD avec Slack</span><span class="sxs-lookup"><span data-stu-id="8c27d-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="8c27d-104">Dans ce didacticiel, vous apprendrez comment toointegrate marge avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c27d-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c27d-105">Intégration de marge à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8c27d-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c27d-106">Vous pouvez contrôler dans Azure AD qui a accès tooSlack</span><span class="sxs-lookup"><span data-stu-id="8c27d-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="8c27d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSlack (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c27d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8c27d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8c27d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c27d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c27d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8c27d-110">Prerequisites</span></span>

<span data-ttu-id="8c27d-111">intégration d’Azure AD avec une marge de tooconfigure, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8c27d-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="8c27d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c27d-113">Un abonnement Slack pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8c27d-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c27d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8c27d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c27d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8c27d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c27d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8c27d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c27d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c27d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c27d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8c27d-118">Scenario description</span></span>
<span data-ttu-id="8c27d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8c27d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c27d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8c27d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c27d-121">Ajout de la marge à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8c27d-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="8c27d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="8c27d-123">Ajout de la marge à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8c27d-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="8c27d-124">intégration de hello tooconfigure marge dans Azure AD, vous devez tooadd Slack à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8c27d-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c27d-125">**tooadd Slack à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c27d-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c27d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8c27d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c27d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c27d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8c27d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8c27d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8c27d-133">Dans la zone de recherche de hello, tapez **Slack**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-133">In hello search box, type **Slack**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="8c27d-135">Dans le volet de résultats hello, sélectionnez **Slack**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8c27d-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c27d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c27d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Slack avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8c27d-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c27d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Slack est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c27d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="8c27d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la marge hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8c27d-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="8c27d-141">Dans la marge, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8c27d-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8c27d-142">tooconfigure et test Azure AD l’authentification unique avec une marge, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8c27d-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c27d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8c27d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c27d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c27d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c27d-145">**[Création d’un utilisateur test marge](#creating-a-slack-test-user)**  -toohave un équivalent de Britta Simon dans Slack est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c27d-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c27d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8c27d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c27d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8c27d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c27d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c27d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de marge.</span><span class="sxs-lookup"><span data-stu-id="8c27d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="8c27d-150">**tooconfigure Azure AD authentification unique avec une marge, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c27d-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c27d-151">Bonjour portail Azure, sur hello **Slack** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8c27d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8c27d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="8c27d-155">Sur hello **URL et le domaine de la marge** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c27d-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="8c27d-157">a.</span><span class="sxs-lookup"><span data-stu-id="8c27d-157">a.</span></span> <span data-ttu-id="8c27d-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="8c27d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="8c27d-159">b.</span><span class="sxs-lookup"><span data-stu-id="8c27d-159">b.</span></span> <span data-ttu-id="8c27d-160">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="8c27d-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8c27d-161">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="8c27d-161">hello value is not real.</span></span> <span data-ttu-id="8c27d-162">Vous avez tooupdate valeur hello hello réel URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="8c27d-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="8c27d-163">Contact [équipe de support marge](https://slack.com/help/contact) valeur de hello tooget</span><span class="sxs-lookup"><span data-stu-id="8c27d-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="8c27d-164">Marge application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="8c27d-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8c27d-165">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="8c27d-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="8c27d-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="8c27d-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8c27d-167">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="8c27d-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="8c27d-169">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, sélectionnez **user.mail** en tant que **identificateur d’utilisateur** et pour chaque ligne indiqué dans le tableau hello ci-dessous, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c27d-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="8c27d-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="8c27d-170">Attribute Name</span></span> | <span data-ttu-id="8c27d-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="8c27d-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8c27d-172">first_name</span><span class="sxs-lookup"><span data-stu-id="8c27d-172">first_name</span></span> | <span data-ttu-id="8c27d-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8c27d-173">user.givenname</span></span> |
    | <span data-ttu-id="8c27d-174">last_name</span><span class="sxs-lookup"><span data-stu-id="8c27d-174">last_name</span></span> | <span data-ttu-id="8c27d-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="8c27d-175">user.surname</span></span> |
    | <span data-ttu-id="8c27d-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="8c27d-176">User.Email</span></span> | <span data-ttu-id="8c27d-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="8c27d-177">user.mail</span></span> |  
    | <span data-ttu-id="8c27d-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="8c27d-178">User.Username</span></span> | <span data-ttu-id="8c27d-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8c27d-179">user.userprincipalname</span></span> |

    <span data-ttu-id="8c27d-180">a.</span><span class="sxs-lookup"><span data-stu-id="8c27d-180">a.</span></span> <span data-ttu-id="8c27d-181">Cliquez sur **attribut** tooopen **modifier l’attribut** boîte de dialogue zone et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c27d-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="8c27d-183">a.</span><span class="sxs-lookup"><span data-stu-id="8c27d-183">a.</span></span> <span data-ttu-id="8c27d-184">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8c27d-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8c27d-185">b.</span><span class="sxs-lookup"><span data-stu-id="8c27d-185">b.</span></span> <span data-ttu-id="8c27d-186">À partir de hello **valeur** liste, la valeur de l’attribut select hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8c27d-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8c27d-187">c.</span><span class="sxs-lookup"><span data-stu-id="8c27d-187">c.</span></span> <span data-ttu-id="8c27d-188">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="8c27d-188">Click **OK**</span></span>

6. <span data-ttu-id="8c27d-189">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8c27d-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="8c27d-191">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8c27d-191">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8c27d-193">Sur hello **Slack Configuration** , cliquez sur **configurer une marge** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8c27d-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8c27d-194">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8c27d-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="8c27d-196">Dans une fenêtre de navigateur web, ouvrez une session dans le site de société Slack tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8c27d-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="8c27d-197">Accédez trop**Microsoft Azure AD** puis passez trop**paramètres d’équipe**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="8c27d-199">Bonjour **paramètres d’équipe** , cliquez sur hello **authentification** onglet, puis cliquez sur **modifier les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="8c27d-201">Sur hello **paramètres d’authentification SAML** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c27d-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="8c27d-203">a.</span><span class="sxs-lookup"><span data-stu-id="8c27d-203">a.</span></span>  <span data-ttu-id="8c27d-204">Bonjour **SAML 2.0 point de terminaison (HTTP)** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27d-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8c27d-205">b.</span><span class="sxs-lookup"><span data-stu-id="8c27d-205">b.</span></span>  <span data-ttu-id="8c27d-206">Bonjour **émetteur de fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27d-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8c27d-207">c.</span><span class="sxs-lookup"><span data-stu-id="8c27d-207">c.</span></span>  <span data-ttu-id="8c27d-208">Ouvrez votre fichier de certificat téléchargé dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat Public** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="8c27d-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="8c27d-209">d.</span><span class="sxs-lookup"><span data-stu-id="8c27d-209">d.</span></span> <span data-ttu-id="8c27d-210">Configurez hello trois paramètres ci-dessus comme il convient pour votre équipe de marge.</span><span class="sxs-lookup"><span data-stu-id="8c27d-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="8c27d-211">Pour plus d’informations sur les paramètres de hello, Veuillez trouver hello **guide de configuration de l’authentification unique de marge** ici.</span><span class="sxs-lookup"><span data-stu-id="8c27d-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="8c27d-212">e.</span><span class="sxs-lookup"><span data-stu-id="8c27d-212">e.</span></span>  <span data-ttu-id="8c27d-213">Cliquez sur **Enregistrer la configuration**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="8c27d-214">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8c27d-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c27d-215">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8c27d-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c27d-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c27d-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c27d-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c27d-218">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8c27d-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8c27d-220">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c27d-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c27d-221">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8c27d-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c27d-223">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c27d-225">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8c27d-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c27d-227">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c27d-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c27d-229">a.</span><span class="sxs-lookup"><span data-stu-id="8c27d-229">a.</span></span> <span data-ttu-id="8c27d-230">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c27d-231">b.</span><span class="sxs-lookup"><span data-stu-id="8c27d-231">b.</span></span> <span data-ttu-id="8c27d-232">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c27d-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c27d-233">c.</span><span class="sxs-lookup"><span data-stu-id="8c27d-233">c.</span></span> <span data-ttu-id="8c27d-234">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8c27d-235">d.</span><span class="sxs-lookup"><span data-stu-id="8c27d-235">d.</span></span> <span data-ttu-id="8c27d-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="8c27d-237">Création d’un utilisateur de test Slack</span><span class="sxs-lookup"><span data-stu-id="8c27d-237">Creating a Slack test user</span></span>

<span data-ttu-id="8c27d-238">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans la marge.</span><span class="sxs-lookup"><span data-stu-id="8c27d-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="8c27d-239">Slack prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="8c27d-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8c27d-240">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="8c27d-240">There is no action item for you in this section.</span></span> <span data-ttu-id="8c27d-241">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Slack s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="8c27d-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="8c27d-242">Si vous devez manuellement toocreate un utilisateur, vous devez tooContact [équipe de support marge](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="8c27d-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8c27d-243">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c27d-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8c27d-244">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSlack.</span><span class="sxs-lookup"><span data-stu-id="8c27d-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8c27d-246">**tooassign Britta Simon tooSlack, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c27d-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c27d-247">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8c27d-249">Dans la liste des applications hello, sélectionnez **Slack**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-249">In hello applications list, select **Slack**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="8c27d-251">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8c27d-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-253">Click **Add** button.</span></span> <span data-ttu-id="8c27d-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8c27d-256">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8c27d-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c27d-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c27d-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8c27d-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c27d-259">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8c27d-259">Testing single sign-on</span></span>

<span data-ttu-id="8c27d-260">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8c27d-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c27d-261">Lorsque vous cliquez sur la vignette de marge hello dans hello volet d’accès, vous devez obtenir application de marge automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="8c27d-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c27d-262">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8c27d-262">Additional resources</span></span>

* [<span data-ttu-id="8c27d-263">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c27d-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c27d-264">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8c27d-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

