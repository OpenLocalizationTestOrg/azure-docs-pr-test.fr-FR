---
title: "Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Sales Navigator | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="b4d48-103">Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="b4d48-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="b4d48-104">Dans ce didacticiel, vous apprendrez comment toointegrate Navigator de ventes LinkedIn avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4d48-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4d48-105">Intégration LinkedIn Sales Navigator à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b4d48-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b4d48-106">Vous pouvez contrôler dans Azure AD qui a accès tooLinkedIn ventes Navigator</span><span class="sxs-lookup"><span data-stu-id="b4d48-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="b4d48-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLinkedIn Navigator Sales (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b4d48-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b4d48-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b4d48-109">Si vous voulez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, parcourir [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4d48-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4d48-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b4d48-110">Prerequisites</span></span>

<span data-ttu-id="b4d48-111">tooconfigure intégration d’Azure AD avec LinkedIn Sales navigateur, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b4d48-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="b4d48-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4d48-113">Un abonnement LinkedIn Sales Navigator pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b4d48-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4d48-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b4d48-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4d48-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b4d48-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4d48-116">Évitez d’utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b4d48-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4d48-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4d48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4d48-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b4d48-118">Scenario description</span></span>
<span data-ttu-id="b4d48-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b4d48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4d48-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b4d48-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4d48-121">Ajout de LinkedIn Sales navigateur à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b4d48-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="b4d48-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="b4d48-123">Ajout de LinkedIn Sales navigateur à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b4d48-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="b4d48-124">intégration de hello tooconfigure du navigateur de ventes LinkedIn dans Azure AD, vous devez tooadd LinkedIn Sales navigateur à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b4d48-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b4d48-125">**tooadd LinkedIn navigateur des ventes à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b4d48-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d48-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b4d48-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b4d48-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b4d48-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b4d48-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b4d48-133">Dans la zone de recherche de hello, tapez **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="b4d48-135">Dans le volet de résultats hello, sélectionnez **LinkedIn Sales Navigator**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b4d48-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b4d48-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b4d48-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Sales Navigator par le biais d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b4d48-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4d48-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le navigateur de ventes LinkedIn est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4d48-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="b4d48-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le navigateur de ventes LinkedIn hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="b4d48-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="b4d48-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le navigateur de ventes LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b4d48-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="b4d48-142">tooconfigure et test Azure AD l’authentification unique avec LinkedIn Sales navigateur, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="b4d48-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b4d48-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b4d48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b4d48-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4d48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4d48-145">**[Création d’un utilisateur de test LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)**  -toohave un équivalent de Britta Simon dans le navigateur client LinkedIn qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="b4d48-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b4d48-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4d48-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="b4d48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b4d48-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b4d48-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de navigateur de ventes LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b4d48-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="b4d48-150">**tooconfigure Azure AD l’authentification unique avec LinkedIn Sales Navigator, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b4d48-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d48-151">Bonjour portail Azure, sur hello **LinkedIn Sales Navigator** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b4d48-153">Sur hello **l’authentification unique** boîte de dialogue, dans **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b4d48-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="b4d48-155">Dans une fenêtre de navigateur web, l’authentification tooyour **LinkedIn Sales Navigator** site Web en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b4d48-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="b4d48-156">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="b4d48-157">En outre, sélectionnez **ventes Navigator** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="b4d48-159">Cliquez sur **ou cliquez ici tooload et copie des champs individuels à partir de l’écran de hello** et copie **Id d’entité** et **Url d’accès ACS (Assertion Consumer)**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="b4d48-161">Sur le portail Azure, sous **LinkedIn Sales navigateur de domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** initiée par le mode.</span><span class="sxs-lookup"><span data-stu-id="b4d48-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="b4d48-163">a.</span><span class="sxs-lookup"><span data-stu-id="b4d48-163">a.</span></span> <span data-ttu-id="b4d48-164">Bonjour **identificateur** zone de texte, entrez hello **ID d’entité** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b4d48-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="b4d48-165">b.</span><span class="sxs-lookup"><span data-stu-id="b4d48-165">b.</span></span> <span data-ttu-id="b4d48-166">Bonjour **URL de réponse** zone de texte, entrez hello **Url d’accès ACS (Assertion Consumer)** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b4d48-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="b4d48-167">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** initiée par le mode.</span><span class="sxs-lookup"><span data-stu-id="b4d48-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="b4d48-169">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="b4d48-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="b4d48-170">Votre **LinkedIn Sales Navigator** application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à configuration tooyour des attributs du jeton SAML tooadd attribut personnalisé mappages.</span><span class="sxs-lookup"><span data-stu-id="b4d48-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b4d48-171">Hello suivant capture d’écran montre un exemple.</span><span class="sxs-lookup"><span data-stu-id="b4d48-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="b4d48-172">Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais LinkedIn Sales Navigator attend qu’il toobe mappée avec une adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="b4d48-173">Vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b4d48-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="b4d48-175">Dans **attributs utilisateur** , cliquez sur **afficher et modifier tous les autres attributs utilisateur** et définir les attributs de hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="b4d48-176">utilisateur de Hello a besoin de revendications de quatre tooadd nommées **messagerie**, **service**, **firstname**, et **lastname** et valeur de hello est toobe mappée avec **user.mail**, **user.department**, **user.givenname**, et **user.surname** respectivement</span><span class="sxs-lookup"><span data-stu-id="b4d48-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="b4d48-177">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="b4d48-177">Attribute Name</span></span> | <span data-ttu-id="b4d48-178">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="b4d48-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b4d48-179">email</span><span class="sxs-lookup"><span data-stu-id="b4d48-179">email</span></span>| <span data-ttu-id="b4d48-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="b4d48-180">user.mail</span></span> |
    | <span data-ttu-id="b4d48-181">department</span><span class="sxs-lookup"><span data-stu-id="b4d48-181">department</span></span>| <span data-ttu-id="b4d48-182">user.department</span><span class="sxs-lookup"><span data-stu-id="b4d48-182">user.department</span></span> |
    | <span data-ttu-id="b4d48-183">firstname</span><span class="sxs-lookup"><span data-stu-id="b4d48-183">firstname</span></span>| <span data-ttu-id="b4d48-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b4d48-184">user.givenname</span></span> |
    | <span data-ttu-id="b4d48-185">lastname</span><span class="sxs-lookup"><span data-stu-id="b4d48-185">lastname</span></span>| <span data-ttu-id="b4d48-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="b4d48-186">user.surname</span></span> |
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="b4d48-188">a.</span><span class="sxs-lookup"><span data-stu-id="b4d48-188">a.</span></span> <span data-ttu-id="b4d48-189">Cliquez sur **ajouter un attribut** boîte de dialogue attribut tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="b4d48-192">b.</span><span class="sxs-lookup"><span data-stu-id="b4d48-192">b.</span></span> <span data-ttu-id="b4d48-193">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="b4d48-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b4d48-194">c.</span><span class="sxs-lookup"><span data-stu-id="b4d48-194">c.</span></span> <span data-ttu-id="b4d48-195">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="b4d48-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b4d48-196">d.</span><span class="sxs-lookup"><span data-stu-id="b4d48-196">d.</span></span> <span data-ttu-id="b4d48-197">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-197">Click **Ok**</span></span>

10. <span data-ttu-id="b4d48-198">Effectuer hello comme suit sur hello **nom** attribut -</span><span class="sxs-lookup"><span data-stu-id="b4d48-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="b4d48-199">a.</span><span class="sxs-lookup"><span data-stu-id="b4d48-199">a.</span></span> <span data-ttu-id="b4d48-200">Cliquez sur hello de hello attribut tooopen **modifier l’attribut** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b4d48-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="b4d48-202">b.</span><span class="sxs-lookup"><span data-stu-id="b4d48-202">b.</span></span> <span data-ttu-id="b4d48-203">Supprimer la valeur d’URL de hello de hello **espace de noms**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="b4d48-204">c.</span><span class="sxs-lookup"><span data-stu-id="b4d48-204">c.</span></span> <span data-ttu-id="b4d48-205">Cliquez sur **Ok** paramètre hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="b4d48-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="b4d48-206">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b4d48-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="b4d48-208">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b4d48-208">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="b4d48-210">Accédez trop**paramètres d’administration LinkedIn** section.</span><span class="sxs-lookup"><span data-stu-id="b4d48-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="b4d48-211">Cliquez sur **télécharger le fichier** hello de tooupload fichier Metadata XML que vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d48-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="b4d48-213">Cliquez sur **sur** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="b4d48-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="b4d48-214">État de l’authentification unique à partir de **non connecté** trop**connecté**</span><span class="sxs-lookup"><span data-stu-id="b4d48-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="b4d48-216">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="b4d48-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b4d48-217">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b4d48-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4d48-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b4d48-219">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="b4d48-220">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="b4d48-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b4d48-222">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b4d48-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d48-223">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b4d48-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b4d48-225">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b4d48-227">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b4d48-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b4d48-229">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b4d48-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b4d48-231">a.</span><span class="sxs-lookup"><span data-stu-id="b4d48-231">a.</span></span> <span data-ttu-id="b4d48-232">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4d48-233">b.</span><span class="sxs-lookup"><span data-stu-id="b4d48-233">b.</span></span> <span data-ttu-id="b4d48-234">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b4d48-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b4d48-235">c.</span><span class="sxs-lookup"><span data-stu-id="b4d48-235">c.</span></span> <span data-ttu-id="b4d48-236">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b4d48-237">d.</span><span class="sxs-lookup"><span data-stu-id="b4d48-237">d.</span></span> <span data-ttu-id="b4d48-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="b4d48-239">Création d’un utilisateur de test LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="b4d48-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="b4d48-240">Application de navigateur Sales lié prend en charge juste dans la configuration de l’utilisateur temps (JIT) et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="b4d48-241">Activer **automatiquement attribuer des licences** tooassign un utilisateur toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="b4d48-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b4d48-243">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d48-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b4d48-244">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLinkedIn Navigator de ventes.</span><span class="sxs-lookup"><span data-stu-id="b4d48-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b4d48-246">**tooassign Britta Simon tooLinkedIn ventes Navigator, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b4d48-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d48-247">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b4d48-249">Dans la liste des applications hello, sélectionnez **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="b4d48-251">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b4d48-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-253">Click **Add** button.</span></span> <span data-ttu-id="b4d48-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b4d48-256">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b4d48-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b4d48-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4d48-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b4d48-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b4d48-259">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b4d48-259">Testing single sign-on</span></span>

<span data-ttu-id="b4d48-260">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b4d48-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b4d48-261">Lorsque vous cliquez sur mosaïque LinkedIn Sales Navigator hello hello volet d’accès, vous devez être page redirigé tooOrganizational où vous avez tooprovide détails personnels de votre compte LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b4d48-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="b4d48-262">Votre compte personnel est ainsi lié à votre compte professionnel LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b4d48-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="b4d48-263">Pour plus d’informations sur hello volet d’accès, consultez [présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b4d48-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b4d48-264">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b4d48-264">Additional resources</span></span>

* [<span data-ttu-id="b4d48-265">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4d48-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4d48-266">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b4d48-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

