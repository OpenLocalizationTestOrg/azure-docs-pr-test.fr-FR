---
title: "Didacticiel : intégration d’Azure Active Directory à T&E Express | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="c0958-103">Didacticiel : Intégration d’Azure Active Directory à T&E Express</span><span class="sxs-lookup"><span data-stu-id="c0958-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="c0958-104">Dans ce didacticiel, vous apprendrez comment toointegrate T & E Express avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0958-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0958-105">Intégration de T & E Express avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c0958-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0958-106">Vous pouvez contrôler dans Azure AD qui a tooT d’accès & E Express</span><span class="sxs-lookup"><span data-stu-id="c0958-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="c0958-107">Vous pouvez activer votre tooT utilisateurs tooautomatically get connecté & E Express (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0958-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="c0958-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="c0958-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0958-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0958-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c0958-110">Prerequisites</span></span>

<span data-ttu-id="c0958-111">tooconfigure intégration d’Azure AD avec T & E Express, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c0958-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="c0958-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0958-113">Un abonnement T&E Express pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c0958-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0958-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c0958-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0958-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c0958-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0958-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c0958-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c0958-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0958-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0958-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c0958-118">Scenario description</span></span>
<span data-ttu-id="c0958-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c0958-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0958-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c0958-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0958-121">Ajout de T & E Express à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c0958-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="c0958-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="c0958-123">Ajout de T & E Express à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c0958-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="c0958-124">tooconfigure hello intégration de T & E Express dans Azure AD, vous devez tooadd T & E Express à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c0958-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0958-125">**tooadd T & E Express à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c0958-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0958-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c0958-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0958-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c0958-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0958-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c0958-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c0958-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c0958-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c0958-133">Dans la zone de recherche de hello, tapez **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="c0958-133">In hello search box, type **T&E Express**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="c0958-135">Dans le volet de résultats hello, sélectionnez **T & E Express**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c0958-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0958-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0958-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec T&E Express avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c0958-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0958-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans T & E Express est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0958-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="c0958-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans T & E Express toobe besoins établie.</span><span class="sxs-lookup"><span data-stu-id="c0958-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="c0958-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans T & E Express.</span><span class="sxs-lookup"><span data-stu-id="c0958-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="c0958-142">tooconfigure et test Azure AD l’authentification unique avec T & E Express, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c0958-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0958-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c0958-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0958-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0958-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0958-145">**[Création d’un utilisateur de test T & E Express](#creating-a-te-express-test-user)**  -toohave de Britta Simon dans T & E Express qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="c0958-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c0958-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c0958-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0958-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c0958-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0958-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0958-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application T & E Express.</span><span class="sxs-lookup"><span data-stu-id="c0958-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="c0958-150">**tooconfigure Azure AD l’authentification unique avec T & E Express, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c0958-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0958-151">Dans le portail de gestion Azure hello, sur hello **T & E Express** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c0958-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c0958-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c0958-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="c0958-155">Sur hello **domaine Express d’E & T et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c0958-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="c0958-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0958-157">a.</span></span> <span data-ttu-id="c0958-158">Bonjour **identificateur** valeur hello de type en tant que zone de texte :`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="c0958-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="c0958-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0958-159">b.</span></span> <span data-ttu-id="c0958-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="c0958-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0958-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="c0958-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="c0958-162">Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="c0958-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c0958-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="c0958-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="c0958-164">Contact [T & E Express prend en charge team](http://www.tyeexpress.com/contacto.aspx) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c0958-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="c0958-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c0958-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="c0958-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c0958-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c0958-169">tooconfigure l’authentification unique sur **T & E Express** côté, connexion toohello T & E express une application sans SAML unique de session à l’aide des informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c0958-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="c0958-170">Sous hello **Admin** onglet, cliquez sur **domaine SAML** page de paramètres SAML tooOpen hello.</span><span class="sxs-lookup"><span data-stu-id="c0958-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="c0958-172">Sélectionnez hello **Activar(Activate)** option à partir de **non** trop**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="c0958-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="c0958-173">Bonjour **métadonnées du fournisseur d’identité** zone de texte, collez hello métadonnées XML que vous avez donwloaded à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c0958-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="c0958-175">Cliquez sur hello **Guardar(Save)** bouton Paramètres de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="c0958-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0958-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0958-177">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0958-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c0958-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c0958-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0958-180">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c0958-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0958-182">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c0958-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0958-184">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c0958-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0958-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c0958-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0958-188">a.</span><span class="sxs-lookup"><span data-stu-id="c0958-188">a.</span></span> <span data-ttu-id="c0958-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0958-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0958-190">b.</span><span class="sxs-lookup"><span data-stu-id="c0958-190">b.</span></span> <span data-ttu-id="c0958-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0958-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0958-192">c.</span><span class="sxs-lookup"><span data-stu-id="c0958-192">c.</span></span> <span data-ttu-id="c0958-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c0958-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0958-194">d.</span><span class="sxs-lookup"><span data-stu-id="c0958-194">d.</span></span> <span data-ttu-id="c0958-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c0958-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="c0958-196">Création d’un utilisateur de test T&E Express</span><span class="sxs-lookup"><span data-stu-id="c0958-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="c0958-197">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans T & E Express, ils doivent être configurés dans T & E Express.</span><span class="sxs-lookup"><span data-stu-id="c0958-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="c0958-198">En l’occurrence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c0958-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="c0958-199">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c0958-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0958-200">Ouvrez une session dans tooyour T & E Express site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c0958-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="c0958-201">Sous la balise de l’administrateur, cliquez sur page maître pour les utilisateurs tooopen hello les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c0958-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="c0958-203">Dans la page d’accueil hello, cliquez sur  **+**  les utilisateurs de tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="c0958-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="c0958-205">Entrez toutes les informations obligatoires hello comme demandé dans le formulaire de hello et cliquez sur hello bouton toosave hello détails d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="c0958-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0958-208">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0958-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0958-209">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooT d’accès & E Express.</span><span class="sxs-lookup"><span data-stu-id="c0958-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c0958-211">**tooassign tooT de Britta Simon & E Express, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c0958-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0958-212">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c0958-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c0958-214">Dans la liste des applications hello, sélectionnez **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="c0958-214">In hello applications list, select **T&E Express**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="c0958-216">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c0958-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c0958-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c0958-218">Click **Add** button.</span></span> <span data-ttu-id="c0958-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c0958-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c0958-221">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c0958-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0958-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c0958-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0958-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c0958-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0958-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c0958-224">Testing single sign-on</span></span>

<span data-ttu-id="c0958-225">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0958-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0958-226">Lorsque vous cliquez sur hello T & E Express mosaïque hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour T & E Express l’application.</span><span class="sxs-lookup"><span data-stu-id="c0958-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0958-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c0958-227">Additional resources</span></span>

* [<span data-ttu-id="c0958-228">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0958-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0958-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c0958-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

