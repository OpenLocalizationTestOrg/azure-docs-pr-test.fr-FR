---
title: "Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Learning | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’apprentissage de LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="adbeb-103">Didacticiel : Intégration d’Azure Active Directory à LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="adbeb-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="adbeb-104">Dans ce didacticiel, vous apprendrez comment toointegrate Learning LinkedIn avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="adbeb-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="adbeb-105">Intégration LinkedIn Learning à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="adbeb-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="adbeb-106">Vous pouvez contrôler dans Azure AD qui a accès tooLinkedIn d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="adbeb-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="adbeb-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLinkedIn Learning (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="adbeb-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="adbeb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="adbeb-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="adbeb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adbeb-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="adbeb-110">Prerequisites</span></span>

<span data-ttu-id="adbeb-111">tooconfigure intégration d’Azure AD avec LinkedIn Learning, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="adbeb-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="adbeb-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="adbeb-113">Un abonnement LinkedIn Learning pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="adbeb-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="adbeb-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="adbeb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="adbeb-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="adbeb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="adbeb-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="adbeb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="adbeb-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="adbeb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="adbeb-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="adbeb-118">Scenario description</span></span>
<span data-ttu-id="adbeb-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="adbeb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="adbeb-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="adbeb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="adbeb-121">Ajout de LinkedIn Learning à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="adbeb-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="adbeb-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="adbeb-123">Ajout de LinkedIn Learning à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="adbeb-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="adbeb-124">tooconfigure hello intégration de LinkedIn Learning dans Azure AD, vous devez tooadd LinkedIn Learning à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="adbeb-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="adbeb-125">**tooadd Learning LinkedIn à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="adbeb-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="adbeb-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="adbeb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="adbeb-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="adbeb-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="adbeb-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="adbeb-133">Dans la zone de recherche de hello, tapez **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="adbeb-134">Dans le volet de résultats, cliquez sur **LinkedIn Learning** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="adbeb-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="adbeb-136">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="adbeb-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Learning avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="adbeb-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="adbeb-138">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LinkedIn Learning est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="adbeb-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="adbeb-139">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LinkedIn Learning doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="adbeb-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="adbeb-140">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** LinkedIn pour la formation.</span><span class="sxs-lookup"><span data-stu-id="adbeb-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="adbeb-141">tooconfigure et test Azure AD l’authentification unique avec LinkedIn Learning, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="adbeb-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="adbeb-142">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="adbeb-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="adbeb-143">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="adbeb-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="adbeb-144">**[Création d’un utilisateur de test LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="adbeb-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="adbeb-145">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adbeb-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="adbeb-146">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="adbeb-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="adbeb-147">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="adbeb-148">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="adbeb-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="adbeb-149">**tooconfigure Azure AD single sign-on avec LinkedIn apprentissage, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="adbeb-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="adbeb-150">Bonjour portail Azure, sur hello **LinkedIn Learning** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="adbeb-152">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adbeb-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="adbeb-154">Dans une fenêtre de navigateur web, client LinkedIn Learning de tooyour de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="adbeb-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="adbeb-155">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="adbeb-156">En outre, sélectionnez **Learning - par défaut** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="adbeb-158">Cliquez sur **ou cliquez ici tooload et copie des champs individuels à partir de l’écran de hello** et copie **Id d’entité** et **Url d’accès ACS (Assertion Consumer)**</span><span class="sxs-lookup"><span data-stu-id="adbeb-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="adbeb-160">Sur le portail Azure, sous **LinkedIn Learning domaine et les URL**, effectuer hello comme suit si vous souhaitez que l’authentification unique de tooconfigure dans **initialisée par IdP** mode</span><span class="sxs-lookup"><span data-stu-id="adbeb-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="adbeb-162">a.</span><span class="sxs-lookup"><span data-stu-id="adbeb-162">a.</span></span> <span data-ttu-id="adbeb-163">Bonjour **identificateur** zone de texte, entrez hello **ID d’entité** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="adbeb-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="adbeb-164">b.</span><span class="sxs-lookup"><span data-stu-id="adbeb-164">b.</span></span> <span data-ttu-id="adbeb-165">Bonjour **URL de réponse** zone de texte, entrez hello **Url d’accès ACS (Assertion Consumer)** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="adbeb-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="adbeb-166">Si vous souhaitez que l’authentification unique de tooconfigure dans **initiée par SP**, puis cliquez sur option Afficher les URL avancées du paramètre dans la section de configuration hello et configurer des URL de connexion hello avec hello modèle :</span><span class="sxs-lookup"><span data-stu-id="adbeb-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="adbeb-168">Votre application LinkedIn Learning attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="adbeb-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="adbeb-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="adbeb-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="adbeb-170">Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais LinkedIn Learning attend ce toobe mappée avec une adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="adbeb-171">Pour cela, vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="adbeb-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="adbeb-173">Dans **attributs utilisateur** , cliquez sur **afficher et modifier tous les autres attributs utilisateur** et définir les attributs de hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="adbeb-174">utilisateur de Hello a besoin de revendications de quatre tooadd nommées **messagerie**, **service**, **firstname**, et **lastname** et valeur de hello est toobe mappée avec **user.mail**, **user.department**, **user.givenname**, et **user.surname** respectivement</span><span class="sxs-lookup"><span data-stu-id="adbeb-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="adbeb-175">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="adbeb-175">Attribute Name</span></span> | <span data-ttu-id="adbeb-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="adbeb-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="adbeb-177">email</span><span class="sxs-lookup"><span data-stu-id="adbeb-177">email</span></span>| <span data-ttu-id="adbeb-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="adbeb-178">user.mail</span></span> |    
    | <span data-ttu-id="adbeb-179">department</span><span class="sxs-lookup"><span data-stu-id="adbeb-179">department</span></span>| <span data-ttu-id="adbeb-180">user.department</span><span class="sxs-lookup"><span data-stu-id="adbeb-180">user.department</span></span> |
    | <span data-ttu-id="adbeb-181">firstname</span><span class="sxs-lookup"><span data-stu-id="adbeb-181">firstname</span></span>| <span data-ttu-id="adbeb-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="adbeb-182">user.givenname</span></span> |
    | <span data-ttu-id="adbeb-183">lastname</span><span class="sxs-lookup"><span data-stu-id="adbeb-183">lastname</span></span>| <span data-ttu-id="adbeb-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="adbeb-184">user.surname</span></span> |
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="adbeb-186">a.</span><span class="sxs-lookup"><span data-stu-id="adbeb-186">a.</span></span> <span data-ttu-id="adbeb-187">Cliquez sur **ajouter un attribut** boîte de dialogue attribut tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="adbeb-190">b.</span><span class="sxs-lookup"><span data-stu-id="adbeb-190">b.</span></span> <span data-ttu-id="adbeb-191">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="adbeb-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="adbeb-192">c.</span><span class="sxs-lookup"><span data-stu-id="adbeb-192">c.</span></span> <span data-ttu-id="adbeb-193">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="adbeb-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="adbeb-194">d.</span><span class="sxs-lookup"><span data-stu-id="adbeb-194">d.</span></span> <span data-ttu-id="adbeb-195">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-195">Click **Ok**</span></span>

10. <span data-ttu-id="adbeb-196">Effectuer hello comme suit sur hello **nom** attribut -</span><span class="sxs-lookup"><span data-stu-id="adbeb-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="adbeb-197">a.</span><span class="sxs-lookup"><span data-stu-id="adbeb-197">a.</span></span> <span data-ttu-id="adbeb-198">Cliquez sur hello de hello attribut tooopen **modifier l’attribut** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="adbeb-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="adbeb-200">b.</span><span class="sxs-lookup"><span data-stu-id="adbeb-200">b.</span></span> <span data-ttu-id="adbeb-201">Supprimer la valeur d’URL de hello de hello **espace de noms**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="adbeb-202">c.</span><span class="sxs-lookup"><span data-stu-id="adbeb-202">c.</span></span> <span data-ttu-id="adbeb-203">Cliquez sur **Ok** paramètre hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="adbeb-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="adbeb-204">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="adbeb-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="adbeb-206">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-206">Click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="adbeb-208">Accédez trop**paramètres d’administration LinkedIn** section.</span><span class="sxs-lookup"><span data-stu-id="adbeb-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="adbeb-209">Téléchargement des fichiers XML hello téléchargé à partir de hello portail Azure en cliquant sur option de fichier XML de télécharger hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="adbeb-211">Cliquez sur **sur** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="adbeb-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="adbeb-212">État de l’authentification unique à partir de **non connecté** trop**connecté**</span><span class="sxs-lookup"><span data-stu-id="adbeb-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="adbeb-214">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="adbeb-215">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="adbeb-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="adbeb-217">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="adbeb-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="adbeb-218">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="adbeb-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="adbeb-220">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="adbeb-222">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="adbeb-224">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="adbeb-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="adbeb-226">a.</span><span class="sxs-lookup"><span data-stu-id="adbeb-226">a.</span></span> <span data-ttu-id="adbeb-227">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="adbeb-228">b.</span><span class="sxs-lookup"><span data-stu-id="adbeb-228">b.</span></span> <span data-ttu-id="adbeb-229">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="adbeb-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="adbeb-230">c.</span><span class="sxs-lookup"><span data-stu-id="adbeb-230">c.</span></span> <span data-ttu-id="adbeb-231">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="adbeb-232">d.</span><span class="sxs-lookup"><span data-stu-id="adbeb-232">d.</span></span> <span data-ttu-id="adbeb-233">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="adbeb-234">Création d’un utilisateur de test LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="adbeb-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="adbeb-235">L’application LinkedIn Learning prend en charge</span><span class="sxs-lookup"><span data-stu-id="adbeb-235">Linked Learning Application supports.</span></span> <span data-ttu-id="adbeb-236">Juste-à-temps l’approvisionnement des utilisateurs et après l’authentification utilisateurs sont automatiquement créés dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="adbeb-237">Dans page de paramètres d’administration hello sur le commutateur de portail hello retournement LinkedIn Learning hello **automatiquement attribuer des licences** tooactive tooenable juste en temps de préparation et cela affectera également un utilisateur toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="adbeb-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="adbeb-239">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="adbeb-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="adbeb-240">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLinkedIn d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="adbeb-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="adbeb-242">**tooassign Britta Simon tooLinkedIn de formation, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="adbeb-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="adbeb-243">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="adbeb-245">Dans la liste des applications hello, sélectionnez **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="adbeb-247">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="adbeb-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-249">Click **Add** button.</span></span> <span data-ttu-id="adbeb-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="adbeb-252">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="adbeb-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="adbeb-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="adbeb-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="adbeb-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="adbeb-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="adbeb-255">Testing single sign-on</span></span>

<span data-ttu-id="adbeb-256">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="adbeb-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="adbeb-257">Lorsque vous cliquez sur mosaïque LinkedIn Learning hello hello volet d’accès, vous devez obtenir la page d’authentification Azure hello et sur après authentification réussie, vous devez obtenir dans votre application LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="adbeb-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="adbeb-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="adbeb-258">Additional resources</span></span>

* [<span data-ttu-id="adbeb-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="adbeb-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="adbeb-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="adbeb-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png