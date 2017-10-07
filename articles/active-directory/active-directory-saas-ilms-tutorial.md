---
title: "Didacticiel : intégration d’Azure Active Directory à iLMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="92a3b-103">Didacticiel : Intégration d’Azure Active Directory à iLMS</span><span class="sxs-lookup"><span data-stu-id="92a3b-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="92a3b-104">Dans ce didacticiel, vous apprendrez comment iLMS toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92a3b-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92a3b-105">Intégration iLMS à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="92a3b-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92a3b-106">Vous pouvez contrôler dans Azure AD qui a accès tooiLMS</span><span class="sxs-lookup"><span data-stu-id="92a3b-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="92a3b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooiLMS (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92a3b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="92a3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="92a3b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92a3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92a3b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="92a3b-110">Prerequisites</span></span>

<span data-ttu-id="92a3b-111">tooconfigure intégration d’Azure AD avec iLMS, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="92a3b-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="92a3b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92a3b-113">Un abonnement iLMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="92a3b-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92a3b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="92a3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92a3b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="92a3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92a3b-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="92a3b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="92a3b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92a3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92a3b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="92a3b-118">Scenario description</span></span>
<span data-ttu-id="92a3b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="92a3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92a3b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="92a3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92a3b-121">Ajout d’iLMS à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="92a3b-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="92a3b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="92a3b-123">Ajout d’iLMS à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="92a3b-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="92a3b-124">intégration de hello tooconfigure d’iLMS dans Azure AD, vous devez iLMS tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="92a3b-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92a3b-125">**iLMS tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92a3b-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92a3b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="92a3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92a3b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="92a3b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="92a3b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="92a3b-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="92a3b-133">Dans la zone de recherche de hello, tapez **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-133">In hello search box, type **iLMS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="92a3b-135">Dans le volet de résultats hello, sélectionnez **iLMS**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="92a3b-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92a3b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92a3b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec iLMS avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="92a3b-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92a3b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans iLMS est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92a3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="92a3b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans iLMS doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="92a3b-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="92a3b-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans iLMS.</span><span class="sxs-lookup"><span data-stu-id="92a3b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="92a3b-142">tooconfigure et test Azure AD l’authentification unique avec iLMS, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="92a3b-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92a3b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="92a3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92a3b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92a3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92a3b-145">**[Création d’un utilisateur de test iLMS](#creating-an-ilms-test-user)**  -toohave un homologue de Britta Simon dans iLMS qui est de sa représentation sous forme de toohello lié Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92a3b-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="92a3b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="92a3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92a3b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="92a3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92a3b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92a3b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application iLMS.</span><span class="sxs-lookup"><span data-stu-id="92a3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="92a3b-150">**tooconfigure Azure AD single sign-on avec iLMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92a3b-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="92a3b-151">Bonjour portail Azure, sur hello **iLMS** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="92a3b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="92a3b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="92a3b-155">Sur hello **iLMS domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="92a3b-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="92a3b-157">a.</span><span class="sxs-lookup"><span data-stu-id="92a3b-157">a.</span></span> <span data-ttu-id="92a3b-158">Bonjour **identificateur** zone de texte, collez hello **identificateur** vous copiez à partir de valeur **fournisseur de services** section des paramètres SAML dans le portail d’administration iLMS.</span><span class="sxs-lookup"><span data-stu-id="92a3b-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="92a3b-159">b.</span><span class="sxs-lookup"><span data-stu-id="92a3b-159">b.</span></span> <span data-ttu-id="92a3b-160">Bonjour **URL de réponse** zone de texte, collez hello **(URL) du point de terminaison** vous copiez à partir de valeur **fournisseur de services** section des paramètres SAML dans le portail d’administration iLMS ayant des éléments suivants de hello modèle`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="92a3b-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="92a3b-161">« 123456 » est un exemple de valeur d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="92a3b-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="92a3b-162">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="92a3b-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="92a3b-164">Bonjour **URL de connexion** zone de texte, collez hello **(URL) du point de terminaison** vous copiez à partir de valeur **fournisseur de services** section des paramètres SAML dans le portail d’administration iLMS en tant que`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="92a3b-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="92a3b-165">tooenable JIT approvisionnement, iLMS application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="92a3b-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="92a3b-166">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="92a3b-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="92a3b-167">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="92a3b-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="92a3b-168">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="92a3b-168">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="92a3b-170">Créer **département, région** et **Division** les attributs et ajouter le nom hello de ces attributs dans iLMS.</span><span class="sxs-lookup"><span data-stu-id="92a3b-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="92a3b-171">Tous les attributs présentés ci-dessus sont requis.</span><span class="sxs-lookup"><span data-stu-id="92a3b-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="92a3b-172">Vous avez tooenable **créer un compte d’utilisateur Un-recognized** dans iLMS toomap ces attributs.</span><span class="sxs-lookup"><span data-stu-id="92a3b-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="92a3b-173">Suivez les instructions de hello [ici](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget une idée sur la configuration des attributs hello.</span><span class="sxs-lookup"><span data-stu-id="92a3b-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="92a3b-174">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92a3b-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="92a3b-175">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="92a3b-175">Attribute Name</span></span> | <span data-ttu-id="92a3b-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="92a3b-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="92a3b-177">division</span><span class="sxs-lookup"><span data-stu-id="92a3b-177">division</span></span> | <span data-ttu-id="92a3b-178">user.department</span><span class="sxs-lookup"><span data-stu-id="92a3b-178">user.department</span></span> |
    | <span data-ttu-id="92a3b-179">region</span><span class="sxs-lookup"><span data-stu-id="92a3b-179">region</span></span> | <span data-ttu-id="92a3b-180">user.state</span><span class="sxs-lookup"><span data-stu-id="92a3b-180">user.state</span></span> |
    | <span data-ttu-id="92a3b-181">department</span><span class="sxs-lookup"><span data-stu-id="92a3b-181">department</span></span> | <span data-ttu-id="92a3b-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="92a3b-182">user.jobtitle</span></span> |

    <span data-ttu-id="92a3b-183">a.</span><span class="sxs-lookup"><span data-stu-id="92a3b-183">a.</span></span> <span data-ttu-id="92a3b-184">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="92a3b-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="92a3b-187">b.</span><span class="sxs-lookup"><span data-stu-id="92a3b-187">b.</span></span> <span data-ttu-id="92a3b-188">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="92a3b-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="92a3b-189">c.</span><span class="sxs-lookup"><span data-stu-id="92a3b-189">c.</span></span> <span data-ttu-id="92a3b-190">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="92a3b-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="92a3b-191">d.</span><span class="sxs-lookup"><span data-stu-id="92a3b-191">d.</span></span> <span data-ttu-id="92a3b-192">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-192">Click **Ok**</span></span>

7. <span data-ttu-id="92a3b-193">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="92a3b-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="92a3b-195">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="92a3b-195">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="92a3b-197">Dans une fenêtre de navigateur web, connectez-vous tooyour **portail d’administration iLMS** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="92a3b-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="92a3b-198">Cliquez sur **SSO:SAML** sous **paramètres** tooopen SAML paramètres et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92a3b-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="92a3b-200">a.</span><span class="sxs-lookup"><span data-stu-id="92a3b-200">a.</span></span> <span data-ttu-id="92a3b-201">Développez hello **fournisseur de services** section et copie hello **identificateur** et **(URL) du point de terminaison** valeur.</span><span class="sxs-lookup"><span data-stu-id="92a3b-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="92a3b-203">b.</span><span class="sxs-lookup"><span data-stu-id="92a3b-203">b.</span></span> <span data-ttu-id="92a3b-204">Sous la section **Fournisseur d’identité**, cliquez sur **importer les métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="92a3b-205">c.</span><span class="sxs-lookup"><span data-stu-id="92a3b-205">c.</span></span> <span data-ttu-id="92a3b-206">Sélectionnez hello **métadonnées** fichier téléchargé à partir du portail Azure à partir de **le certificat de signature SAML** section.</span><span class="sxs-lookup"><span data-stu-id="92a3b-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="92a3b-208">d.</span><span class="sxs-lookup"><span data-stu-id="92a3b-208">d.</span></span> <span data-ttu-id="92a3b-209">Si vous souhaitez tooenable JIT configuration toocreate iLMS de comptes pour annuler-reconnaître les utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="92a3b-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="92a3b-210">Cochez **Créer un compte utilisateur non reconnu**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="92a3b-212">Mapper les attributs de hello dans Azure AD avec des attributs hello dans iLMS.</span><span class="sxs-lookup"><span data-stu-id="92a3b-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="92a3b-213">Dans la colonne d’attribut hello, spécifiez hello attributs nom ou hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="92a3b-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="92a3b-214">e.</span><span class="sxs-lookup"><span data-stu-id="92a3b-214">e.</span></span> <span data-ttu-id="92a3b-215">Accédez trop**les règles d’entreprise** onglet et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92a3b-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="92a3b-217">Vérifiez **créer des régions Un-recognized, Divisions et services** toocreate régions, Divisions et des services qui n’existent pas déjà au moment de hello de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="92a3b-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="92a3b-218">Vérifiez **mise à jour les profils utilisateur pendant connectez-vous** toospecify si hello profil utilisateur est mise à jour à chaque ouverture de session unique.</span><span class="sxs-lookup"><span data-stu-id="92a3b-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="92a3b-219">Si hello **« Mise à jour vide valeurs pour Non champs de profil utilisateur obligatoire »** option est activée, les champs facultatifs qui sont vides lors de la connexion dans seront également provoquent hello iLMS profil utilisateur toocontain des valeurs vides pour ces champs.</span><span class="sxs-lookup"><span data-stu-id="92a3b-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="92a3b-220">Vérifiez **envoyer un E-mail de Notification d’erreur** et entrez le courriel hello d’utilisateur de hello tooreceive hello erreur notification par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="92a3b-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="92a3b-221">Cliquez sur **enregistrer** bouton Paramètres de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="92a3b-221">Click **Save** button toosave hello settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="92a3b-223">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="92a3b-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="92a3b-224">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="92a3b-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="92a3b-225">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92a3b-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92a3b-226">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="92a3b-227">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="92a3b-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="92a3b-229">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92a3b-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92a3b-230">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="92a3b-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92a3b-232">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="92a3b-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92a3b-234">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="92a3b-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92a3b-236">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92a3b-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92a3b-238">a.</span><span class="sxs-lookup"><span data-stu-id="92a3b-238">a.</span></span> <span data-ttu-id="92a3b-239">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92a3b-240">b.</span><span class="sxs-lookup"><span data-stu-id="92a3b-240">b.</span></span> <span data-ttu-id="92a3b-241">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92a3b-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92a3b-242">c.</span><span class="sxs-lookup"><span data-stu-id="92a3b-242">c.</span></span> <span data-ttu-id="92a3b-243">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="92a3b-244">d.</span><span class="sxs-lookup"><span data-stu-id="92a3b-244">d.</span></span> <span data-ttu-id="92a3b-245">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="92a3b-246">Création d’un utilisateur de test iLMS</span><span class="sxs-lookup"><span data-stu-id="92a3b-246">Creating an iLMS test user</span></span>

<span data-ttu-id="92a3b-247">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="92a3b-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="92a3b-248">JIT fonctionnera, si vous avez cliqué sur hello **créer un compte d’utilisateur Un-recognized** case à cocher au cours du paramètre de configuration de SAML au portail d’administration iLMS.</span><span class="sxs-lookup"><span data-stu-id="92a3b-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="92a3b-249">Si vous avez besoin de toocreate un utilisateur manuellement, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="92a3b-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="92a3b-250">Ouvrez une session dans le site d’entreprise tooyour iLMS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="92a3b-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="92a3b-251">Cliquez sur **« Inscrire un utilisateur »** sous **utilisateurs** onglet tooopen **inscrire un utilisateur** page.</span><span class="sxs-lookup"><span data-stu-id="92a3b-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Ajouter un employé](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="92a3b-253">Sur hello **« Inscrire un utilisateur »** page, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="92a3b-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="92a3b-255">a.</span><span class="sxs-lookup"><span data-stu-id="92a3b-255">a.</span></span> <span data-ttu-id="92a3b-256">Bonjour **prénom** prénom de type hello Brian zone de texte.</span><span class="sxs-lookup"><span data-stu-id="92a3b-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="92a3b-257">b.</span><span class="sxs-lookup"><span data-stu-id="92a3b-257">b.</span></span> <span data-ttu-id="92a3b-258">Bonjour **nom** zone de texte, hello de type nom Simon.</span><span class="sxs-lookup"><span data-stu-id="92a3b-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="92a3b-259">c.</span><span class="sxs-lookup"><span data-stu-id="92a3b-259">c.</span></span> <span data-ttu-id="92a3b-260">Bonjour **ID de courrier électronique** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92a3b-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="92a3b-261">d.</span><span class="sxs-lookup"><span data-stu-id="92a3b-261">d.</span></span> <span data-ttu-id="92a3b-262">Bonjour **région** liste déroulante, la valeur hello select pour la région.</span><span class="sxs-lookup"><span data-stu-id="92a3b-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="92a3b-263">e.</span><span class="sxs-lookup"><span data-stu-id="92a3b-263">e.</span></span> <span data-ttu-id="92a3b-264">Bonjour **Division** liste déroulante, la valeur hello select de division.</span><span class="sxs-lookup"><span data-stu-id="92a3b-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="92a3b-265">f.</span><span class="sxs-lookup"><span data-stu-id="92a3b-265">f.</span></span> <span data-ttu-id="92a3b-266">Bonjour **service** liste déroulante, la valeur hello select pour le service.</span><span class="sxs-lookup"><span data-stu-id="92a3b-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="92a3b-267">g.</span><span class="sxs-lookup"><span data-stu-id="92a3b-267">g.</span></span> <span data-ttu-id="92a3b-268">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92a3b-269">Vous pouvez envoyer toouser de messagerie de l’inscription en sélectionnant **envoyer un message d’inscription** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="92a3b-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="92a3b-270">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a3b-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="92a3b-271">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooiLMS de son accès.</span><span class="sxs-lookup"><span data-stu-id="92a3b-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="92a3b-273">**tooassign Britta Simon tooiLMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92a3b-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="92a3b-274">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="92a3b-276">Dans la liste des applications hello, sélectionnez **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-276">In hello applications list, select **iLMS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="92a3b-278">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="92a3b-280">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-280">Click **Add** button.</span></span> <span data-ttu-id="92a3b-281">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="92a3b-283">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="92a3b-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="92a3b-284">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92a3b-285">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="92a3b-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92a3b-286">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="92a3b-286">Testing single sign-on</span></span>

<span data-ttu-id="92a3b-287">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="92a3b-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="92a3b-288">Lorsque vous cliquez sur hello iLMS vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour iLMS application.</span><span class="sxs-lookup"><span data-stu-id="92a3b-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92a3b-289">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="92a3b-289">Additional resources</span></span>

* [<span data-ttu-id="92a3b-290">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92a3b-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92a3b-291">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="92a3b-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

