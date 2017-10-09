---
title: "Tutoriel : Intégration d’Azure Active Directory à LinkedIn Lookup | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de recherche de LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="83357-103">Tutoriel : Intégration d’Azure Active Directory à LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="83357-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="83357-104">Dans ce didacticiel, vous apprendrez comment toointegrate recherche LinkedIn avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83357-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83357-105">Intégration de recherche de LinkedIn avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="83357-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83357-106">Vous pouvez contrôler dans Azure AD qui a accès tooLinkedIn recherche</span><span class="sxs-lookup"><span data-stu-id="83357-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="83357-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLinkedIn recherche (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83357-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="83357-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="83357-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83357-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83357-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="83357-110">Prerequisites</span></span>

<span data-ttu-id="83357-111">tooconfigure intégration d’Azure AD avec LinkedIn recherche, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="83357-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="83357-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83357-113">Un abonnement LinkedIn Lookup pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="83357-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83357-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="83357-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83357-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="83357-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83357-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="83357-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83357-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83357-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83357-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="83357-118">Scenario description</span></span>
<span data-ttu-id="83357-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="83357-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83357-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="83357-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83357-121">Ajout de LinkedIn recherche à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="83357-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="83357-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="83357-123">Ajout de LinkedIn recherche à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="83357-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="83357-124">tooconfigure hello intégration de la recherche LinkedIn dans Azure AD, vous devez tooadd LinkedIn recherche à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="83357-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83357-125">**tooadd recherche LinkedIn à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="83357-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83357-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="83357-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83357-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="83357-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83357-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="83357-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="83357-131">Cliquez sur **nouvelle application** bouton en haut de hello de nouvelle application hello dialogue tooadd.</span><span class="sxs-lookup"><span data-stu-id="83357-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="83357-133">Dans la zone de recherche de hello, tapez **LinkedIn recherche**.</span><span class="sxs-lookup"><span data-stu-id="83357-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="83357-135">Dans le volet de résultats hello, sélectionnez **LinkedIn recherche**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="83357-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83357-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83357-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Lookup, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="83357-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83357-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans la recherche de LinkedIn est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83357-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="83357-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la recherche de LinkedIn hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="83357-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="83357-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans la recherche de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="83357-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="83357-142">tooconfigure et test Azure AD l’authentification unique avec LinkedIn recherche, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="83357-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83357-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="83357-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83357-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83357-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83357-145">**[Création d’un utilisateur de test LinkedIn recherche](#creating-an-linkedin-lookup-test-user)**  -toohave un équivalent de Britta Simon dans LinkedIn recherche qui est la représentation sous forme de toohello lié Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83357-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="83357-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="83357-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83357-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="83357-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83357-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83357-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de recherche de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="83357-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="83357-150">**tooconfigure Azure AD single sign-on avec LinkedIn recherche, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="83357-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="83357-151">Bonjour portail Azure, sur hello **LinkedIn recherche** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="83357-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="83357-153">Sur hello **l’authentification unique** boîte de dialogue, dans **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="83357-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="83357-155">Dans une fenêtre de navigateur web, l’authentification tooyour **LinkedIn recherche** site Web en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="83357-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="83357-156">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="83357-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="83357-157">En outre, sélectionnez **recherche** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="83357-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="83357-159">Cliquez sur **ou cliquez ici tooload et copie des champs individuels à partir de l’écran de hello** et copie **Id d’entité** et **Url d’accès ACS (Assertion Consumer)**</span><span class="sxs-lookup"><span data-stu-id="83357-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="83357-161">Sur le portail Azure, sous **URL et le domaine de recherche LinkedIn** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="83357-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="83357-163">a.</span><span class="sxs-lookup"><span data-stu-id="83357-163">a.</span></span> <span data-ttu-id="83357-164">Bonjour **identificateur** zone de texte, entrez hello **ID d’entité** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="83357-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="83357-165">b.</span><span class="sxs-lookup"><span data-stu-id="83357-165">b.</span></span> <span data-ttu-id="83357-166">Bonjour **URL de réponse** zone de texte, entrez hello **Url d’accès ACS (Assertion Consumer)** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="83357-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="83357-167">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="83357-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="83357-169">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="83357-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="83357-170">Ceci n’est pas une valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="83357-170">This is not real value.</span></span> <span data-ttu-id="83357-171">utilisateur de Hello a tooupdate ces valeurs avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="83357-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="83357-172">Contact [équipe de support Client de recherche LinkedIn](https://business.LinkedIn.com/lookup) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="83357-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="83357-173">Votre **LinkedIn recherche** application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="83357-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="83357-174">utilisateur de Hello a configuration toohello des attributs du jeton SAML tooadd attribut personnalisé mappages.</span><span class="sxs-lookup"><span data-stu-id="83357-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="83357-175">Hello suivant capture d’écran montre un exemple.</span><span class="sxs-lookup"><span data-stu-id="83357-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="83357-176">Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais LinkedIn recherche attend ce toobe mappée avec une adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="83357-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="83357-177">Vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="83357-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="83357-179">Dans **attributs utilisateur** , cliquez sur **afficher et modifier tous les autres attributs utilisateur** et définir les attributs de hello.</span><span class="sxs-lookup"><span data-stu-id="83357-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="83357-180">utilisateur de Hello a besoin de revendications de quatre tooadd nommées **messagerie**, **service**, **firstname**, et **lastname** et valeur de hello est toobe mappée avec **user.mail**, **user.department**, **user.givenname**, et **user.surname** respectivement</span><span class="sxs-lookup"><span data-stu-id="83357-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="83357-181">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="83357-181">Attribute Name</span></span> | <span data-ttu-id="83357-182">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="83357-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="83357-183">email</span><span class="sxs-lookup"><span data-stu-id="83357-183">email</span></span>| <span data-ttu-id="83357-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="83357-184">user.mail</span></span> |    
    | <span data-ttu-id="83357-185">department</span><span class="sxs-lookup"><span data-stu-id="83357-185">department</span></span>| <span data-ttu-id="83357-186">user.department</span><span class="sxs-lookup"><span data-stu-id="83357-186">user.department</span></span> |
    | <span data-ttu-id="83357-187">firstname</span><span class="sxs-lookup"><span data-stu-id="83357-187">firstname</span></span>| <span data-ttu-id="83357-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="83357-188">user.givenname</span></span> |
    | <span data-ttu-id="83357-189">lastname</span><span class="sxs-lookup"><span data-stu-id="83357-189">lastname</span></span>| <span data-ttu-id="83357-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="83357-190">user.surname</span></span> |

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="83357-192">a.</span><span class="sxs-lookup"><span data-stu-id="83357-192">a.</span></span> <span data-ttu-id="83357-193">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="83357-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="83357-196">b.</span><span class="sxs-lookup"><span data-stu-id="83357-196">b.</span></span> <span data-ttu-id="83357-197">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="83357-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="83357-198">c.</span><span class="sxs-lookup"><span data-stu-id="83357-198">c.</span></span> <span data-ttu-id="83357-199">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="83357-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="83357-200">d.</span><span class="sxs-lookup"><span data-stu-id="83357-200">d.</span></span> <span data-ttu-id="83357-201">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="83357-201">Click **Ok**</span></span>

10. <span data-ttu-id="83357-202">Effectuer hello comme suit sur hello **nom** attribut -</span><span class="sxs-lookup"><span data-stu-id="83357-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="83357-203">a.</span><span class="sxs-lookup"><span data-stu-id="83357-203">a.</span></span> <span data-ttu-id="83357-204">Cliquez sur hello de hello attribut tooopen **modifier l’attribut** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="83357-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="83357-206">b.</span><span class="sxs-lookup"><span data-stu-id="83357-206">b.</span></span> <span data-ttu-id="83357-207">Supprimer la valeur d’URL de hello de hello **espace de noms**.</span><span class="sxs-lookup"><span data-stu-id="83357-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="83357-208">c.</span><span class="sxs-lookup"><span data-stu-id="83357-208">c.</span></span> <span data-ttu-id="83357-209">Cliquez sur **Ok** paramètre hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="83357-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="83357-210">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="83357-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="83357-212">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="83357-212">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="83357-214">Accédez trop**paramètres d’administration LinkedIn** section.</span><span class="sxs-lookup"><span data-stu-id="83357-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="83357-215">Fichier XML de téléchargement hello vous avez téléchargé à partir de hello portail Azure en cliquant sur hello **télécharger le fichier** option.</span><span class="sxs-lookup"><span data-stu-id="83357-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="83357-217">Cliquez sur **sur** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="83357-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="83357-218">État de l’authentification unique à partir de **non connecté** trop**connecté**</span><span class="sxs-lookup"><span data-stu-id="83357-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="83357-220">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="83357-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="83357-221">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="83357-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="83357-222">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83357-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83357-223">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="83357-224">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="83357-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="83357-226">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="83357-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83357-227">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="83357-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83357-229">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="83357-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83357-231">Cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="83357-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83357-233">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="83357-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83357-235">a.</span><span class="sxs-lookup"><span data-stu-id="83357-235">a.</span></span> <span data-ttu-id="83357-236">Bonjour **nom** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="83357-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="83357-237">b.</span><span class="sxs-lookup"><span data-stu-id="83357-237">b.</span></span> <span data-ttu-id="83357-238">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83357-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="83357-239">c.</span><span class="sxs-lookup"><span data-stu-id="83357-239">c.</span></span> <span data-ttu-id="83357-240">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="83357-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="83357-241">d.</span><span class="sxs-lookup"><span data-stu-id="83357-241">d.</span></span> <span data-ttu-id="83357-242">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="83357-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="83357-243">Création d’un utilisateur de test LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="83357-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="83357-244">Application de recherche lié prend en charge juste dans la configuration de l’utilisateur temps (JIT) et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="83357-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="83357-245">Activer **automatiquement attribuer des licences** tooassign un utilisateur toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="83357-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83357-247">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="83357-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="83357-248">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLinkedIn recherche.</span><span class="sxs-lookup"><span data-stu-id="83357-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="83357-250">**tooassign Britta Simon tooLinkedIn recherche, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="83357-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="83357-251">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="83357-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="83357-253">Dans la liste des applications hello, sélectionnez **LinkedIn recherche**.</span><span class="sxs-lookup"><span data-stu-id="83357-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="83357-255">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="83357-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="83357-257">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="83357-257">Click **Add** button.</span></span> <span data-ttu-id="83357-258">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="83357-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="83357-260">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="83357-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83357-261">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="83357-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83357-262">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="83357-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83357-263">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="83357-263">Testing single sign-on</span></span>

<span data-ttu-id="83357-264">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="83357-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="83357-265">Lorsque vous cliquez sur hello LinkedIn recherche vignette Bonjour volet d’accès, vous devez être page redirigé tooOrganizational où vous avez tooprovide détails personnels de votre compte LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="83357-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="83357-266">Votre compte personnel est ainsi lié à votre compte professionnel LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="83357-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="83357-267">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="83357-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="83357-268">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="83357-268">Additional resources</span></span>

* [<span data-ttu-id="83357-269">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83357-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83357-270">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="83357-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

