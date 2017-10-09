---
title: "Didacticiel : Intégration d’Azure Active Directory à Amazon Web Services (AWS) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="2b268-103">Didacticiel : Intégration d’Azure Active Directory à Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="2b268-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="2b268-104">Dans ce didacticiel, vous apprendrez comment toointegrate Amazon Web Services (AWS) avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b268-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b268-105">Intégration Amazon Web Services (AWS) à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2b268-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b268-106">Vous pouvez contrôler dans Azure AD qui a accès tooAmazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="2b268-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="2b268-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAmazon Web Services (AWS) (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b268-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2b268-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b268-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b268-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="2b268-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2b268-110">Prerequisites</span></span>

<span data-ttu-id="2b268-111">tooconfigure intégration d’Azure AD avec Amazon Web Services (AWS), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2b268-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="2b268-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b268-113">Abonnement Amazon Web Services (AWS) avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="2b268-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b268-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2b268-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b268-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2b268-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b268-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2b268-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2b268-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b268-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b268-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2b268-118">Scenario description</span></span>
<span data-ttu-id="2b268-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2b268-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b268-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2b268-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b268-121">Ajout d’Amazon Web Services (AWS) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2b268-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="2b268-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="2b268-123">Ajout d’Amazon Web Services (AWS) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2b268-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="2b268-124">intégration de hello tooconfigure Amazon Web Services (AWS) dans Azure AD, vous devez tooadd Amazon Web Services (AWS) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2b268-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b268-125">**tooadd Amazon Web Services (AWS) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b268-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b268-126">Bonjour  **[Azure Portal](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2b268-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b268-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2b268-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b268-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2b268-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2b268-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="2b268-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2b268-133">Dans la zone de recherche de hello, tapez **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="2b268-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="2b268-135">Dans le volet de résultats hello, sélectionnez **Amazon Web Services (AWS)**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b268-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b268-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b268-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Amazon Web Services (AWS), en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2b268-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b268-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello Amazon Web Services (AWS) est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b268-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="2b268-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello Amazon Web Services (AWS) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2b268-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="2b268-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="2b268-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="2b268-142">tooconfigure et test Azure AD l’authentification unique avec Amazon Web Services (AWS), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2b268-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b268-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2b268-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b268-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b268-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b268-145">**[Création d’un utilisateur de test Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave de Britta Simon dans Amazon Web Services (AWS) qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="2b268-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2b268-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2b268-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b268-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2b268-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b268-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b268-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="2b268-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="2b268-150">**tooconfigure Azure AD l’authentification unique avec Amazon Web Services (AWS), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b268-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="2b268-151">Bonjour portail Azure, sur hello **Amazon Web Services (AWS)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2b268-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2b268-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2b268-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="2b268-155">Sur hello **Amazon Web Services (AWS) domaine et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="2b268-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="2b268-157">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2b268-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="2b268-159">Hello application logicielle de Amazon Web Services (AWS) attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="2b268-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="2b268-160">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="2b268-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="2b268-161">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="2b268-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2b268-162">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="2b268-162">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="2b268-164">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="2b268-165">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="2b268-165">Attribute Name</span></span>  | <span data-ttu-id="2b268-166">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="2b268-166">Attribute Value</span></span> | <span data-ttu-id="2b268-167">Espace de noms</span><span class="sxs-lookup"><span data-stu-id="2b268-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="2b268-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="2b268-168">RoleSessionName</span></span> | <span data-ttu-id="2b268-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="2b268-169">user.userprincipalname</span></span> | <span data-ttu-id="2b268-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="2b268-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="2b268-171">Rôle</span><span class="sxs-lookup"><span data-stu-id="2b268-171">Role</span></span>            | <span data-ttu-id="2b268-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="2b268-172">user.assignedroles</span></span> |  <span data-ttu-id="2b268-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="2b268-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="2b268-174">Vous devez tooconfigure hello configuration de l’utilisateur dans Azure AD toofetch tous les rôles de hello du AWS Console.</span><span class="sxs-lookup"><span data-stu-id="2b268-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="2b268-175">Reportez-vous hello provisionnement des étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2b268-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="2b268-176">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-176">a.</span></span> <span data-ttu-id="2b268-177">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2b268-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="2b268-179">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-179">b.</span></span> <span data-ttu-id="2b268-180">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="2b268-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2b268-182">c.</span><span class="sxs-lookup"><span data-stu-id="2b268-182">c.</span></span> <span data-ttu-id="2b268-183">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="2b268-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="2b268-184">Ajouter la valeur de Namespace hello indiquées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2b268-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="2b268-185">d.</span><span class="sxs-lookup"><span data-stu-id="2b268-185">d.</span></span> <span data-ttu-id="2b268-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b268-186">Click **Ok**.</span></span>

7. <span data-ttu-id="2b268-187">Cliquez sur **enregistrer** bouton Paramètres de hello toosave sur Azure.</span><span class="sxs-lookup"><span data-stu-id="2b268-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2b268-189">Dans une autre fenêtre de navigateur, site d’entreprise authentification tooyour Amazon Web Services (AWS) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2b268-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="2b268-190">Cliquez sur **Console Home**.</span><span class="sxs-lookup"><span data-stu-id="2b268-190">Click **Console Home**.</span></span>
   
    ![Configurer l’authentification unique][11]

10. <span data-ttu-id="2b268-192">Cliquez sur **IAM** à partir du service **Security, Identity & Compliance** (Sécurité, identité et conformité).</span><span class="sxs-lookup"><span data-stu-id="2b268-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configurer l’authentification unique][12]

11. <span data-ttu-id="2b268-194">Cliquez sur **Identity Providers**, puis sur **Create Provider**.</span><span class="sxs-lookup"><span data-stu-id="2b268-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configurer l’authentification unique][13]

12. <span data-ttu-id="2b268-196">Sur hello **configurer un fournisseur de** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique][14]
 
    <span data-ttu-id="2b268-198">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-198">a.</span></span> <span data-ttu-id="2b268-199">Pour **Provider Type**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2b268-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="2b268-200">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-200">b.</span></span> <span data-ttu-id="2b268-201">Bonjour **nom du fournisseur** zone de texte, tapez un nom de fournisseur (par exemple : *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="2b268-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="2b268-202">c.</span><span class="sxs-lookup"><span data-stu-id="2b268-202">c.</span></span> <span data-ttu-id="2b268-203">tooupload votre fichier de métadonnées téléchargé, cliquez sur **choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="2b268-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="2b268-204">d.</span><span class="sxs-lookup"><span data-stu-id="2b268-204">d.</span></span> <span data-ttu-id="2b268-205">Cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="2b268-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="2b268-206">Sur hello **vérifier les informations de fournisseur** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="2b268-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configurer l’authentification unique][15]

14. <span data-ttu-id="2b268-208">Cliquez sur **Roles**, puis sur **Create New Role**.</span><span class="sxs-lookup"><span data-stu-id="2b268-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configurer l’authentification unique][16]

15. <span data-ttu-id="2b268-210">Sur hello **définir un nom de rôle** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Configurer l’authentification unique][17] 

    <span data-ttu-id="2b268-212">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-212">a.</span></span> <span data-ttu-id="2b268-213">Bonjour **nom de rôle** zone de texte, tapez un nom de rôle (par exemple : *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="2b268-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="2b268-214">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-214">b.</span></span> <span data-ttu-id="2b268-215">Cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="2b268-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="2b268-216">Sur hello **sélectionner le Type de rôle** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Configurer l’authentification unique][18] 

    <span data-ttu-id="2b268-218">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-218">a.</span></span> <span data-ttu-id="2b268-219">Sélectionnez **Role For Identity Provider Access**.</span><span class="sxs-lookup"><span data-stu-id="2b268-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="2b268-220">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-220">b.</span></span> <span data-ttu-id="2b268-221">Bonjour **Grant Web Single Sign-On (WebSSO) tooSAML fournisseurs d’accès aux** , cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="2b268-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="2b268-222">Sur hello **établir la confiance** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Configurer l’authentification unique][19] 

    <span data-ttu-id="2b268-224">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-224">a.</span></span> <span data-ttu-id="2b268-225">En tant que fournisseur SAML, sélectionnez fournisseur SAML de hello que vous avez créé précédemment (par exemple : *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="2b268-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="2b268-226">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-226">b.</span></span> <span data-ttu-id="2b268-227">Cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="2b268-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="2b268-228">Sur hello **vérifier une approbation de rôle** boîte de dialogue, cliquez sur **étape suivante**.</span><span class="sxs-lookup"><span data-stu-id="2b268-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configurer l’authentification unique][32]

19. <span data-ttu-id="2b268-230">Sur hello **attacher une stratégie** boîte de dialogue, cliquez sur **étape suivante**.</span><span class="sxs-lookup"><span data-stu-id="2b268-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configurer l’authentification unique][33]

20. <span data-ttu-id="2b268-232">Sur hello **révision** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique][34]
 
    <span data-ttu-id="2b268-234">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-234">a.</span></span> <span data-ttu-id="2b268-235">Cliquez sur **Create Role**.</span><span class="sxs-lookup"><span data-stu-id="2b268-235">Click **Create Role**.</span></span>

    <span data-ttu-id="2b268-236">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-236">b.</span></span> <span data-ttu-id="2b268-237">Créez autant de rôles en fonction des besoins et les mapper toohello fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="2b268-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="2b268-238">Maintenant configurer hello l’approvisionnement d’utilisateurs toofetch tous les rôles de hello du AWS</span><span class="sxs-lookup"><span data-stu-id="2b268-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="2b268-239">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-239">a.</span></span> <span data-ttu-id="2b268-240">Dans la connexion à la Console de AWS hello avec votre compte racine</span><span class="sxs-lookup"><span data-stu-id="2b268-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="2b268-241">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-241">b.</span></span> <span data-ttu-id="2b268-242">Dans hello coin supérieur droit sur votre nom, puis sur hello **mes informations d’identification de sécurité** option.</span><span class="sxs-lookup"><span data-stu-id="2b268-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="2b268-243">Un écran contenant un message d’avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2b268-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="2b268-244">Cliquez sur le bouton de hello **informations d’identification de sécurité** bouton toopass hello écran.</span><span class="sxs-lookup"><span data-stu-id="2b268-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Configurer l’authentification unique][36]

       ![Configurer l’authentification unique][37]

    <span data-ttu-id="2b268-247">c.</span><span class="sxs-lookup"><span data-stu-id="2b268-247">c.</span></span> <span data-ttu-id="2b268-248">Bonjour clés d’accès de section, cliquez sur hello **créer de nouvelle clé d’accès** bouton.</span><span class="sxs-lookup"><span data-stu-id="2b268-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="2b268-249">Cette opération génère hello ID clé d’accès et une valeur de jeton.</span><span class="sxs-lookup"><span data-stu-id="2b268-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Configurer l’authentification unique][38]

    <span data-ttu-id="2b268-251">d.</span><span class="sxs-lookup"><span data-stu-id="2b268-251">d.</span></span> <span data-ttu-id="2b268-252">Copiez ces deux valeurs et téléchargez-les, pour ne pas les perdre.</span><span class="sxs-lookup"><span data-stu-id="2b268-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="2b268-253">e.</span><span class="sxs-lookup"><span data-stu-id="2b268-253">e.</span></span> <span data-ttu-id="2b268-254">Bonjour portail Azure, sur la page d’intégration d’application hello Amazon Web Services (AWS), cliquez sur **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="2b268-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configurer l’authentification unique][35]

    <span data-ttu-id="2b268-256">f.</span><span class="sxs-lookup"><span data-stu-id="2b268-256">f.</span></span> <span data-ttu-id="2b268-257">Définir le mode d’approvisionnement hello trop**automatique**</span><span class="sxs-lookup"><span data-stu-id="2b268-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Configurer l’authentification unique][39]

    <span data-ttu-id="2b268-259">g.</span><span class="sxs-lookup"><span data-stu-id="2b268-259">g.</span></span> <span data-ttu-id="2b268-260">En hello **clientsecret** et **Secret jeton** collez les valeurs correspondantes hello, qui vous avez copié à partir de la Console de AWS.</span><span class="sxs-lookup"><span data-stu-id="2b268-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="2b268-261">h.</span><span class="sxs-lookup"><span data-stu-id="2b268-261">h.</span></span> <span data-ttu-id="2b268-262">Vous pouvez cliquer sur hello **tester la connexion** bouton connectivité de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="2b268-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="2b268-263">Une fois qu’il réussit vous pouvez démarrer hello mise en service du connecteur.</span><span class="sxs-lookup"><span data-stu-id="2b268-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Configurer l’authentification unique][40]

    <span data-ttu-id="2b268-265">i.</span><span class="sxs-lookup"><span data-stu-id="2b268-265">i.</span></span> <span data-ttu-id="2b268-266">À présent activer hello état d’approvisionnement trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="2b268-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="2b268-267">Cela démarre l’extraction des rôles de hello à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2b268-267">This starts fetching hello roles from hello application.</span></span>

       ![Configurer l’authentification unique][41]

    > [!NOTE]
    > <span data-ttu-id="2b268-269">Service de configuration d’Active Directory Azure s’exécute chaque après certains rôles de hello toosync temps de AWS.</span><span class="sxs-lookup"><span data-stu-id="2b268-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="2b268-270">Vous devez voir hello tout fournisseur d’identité relié les rôles AWS dans Azure AD et vous pouvez les utiliser lors de l’affectation hello application toousers ou des groupes.</span><span class="sxs-lookup"><span data-stu-id="2b268-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b268-271">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b268-272">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="2b268-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2b268-274">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b268-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b268-275">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2b268-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b268-277">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2b268-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b268-279">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2b268-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b268-281">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b268-283">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-283">a.</span></span> <span data-ttu-id="2b268-284">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b268-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b268-285">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-285">b.</span></span> <span data-ttu-id="2b268-286">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b268-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b268-287">c.</span><span class="sxs-lookup"><span data-stu-id="2b268-287">c.</span></span> <span data-ttu-id="2b268-288">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2b268-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b268-289">d.</span><span class="sxs-lookup"><span data-stu-id="2b268-289">d.</span></span> <span data-ttu-id="2b268-290">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b268-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="2b268-291">Création d’un utilisateur de test pour Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="2b268-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="2b268-292">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooAmazon Web Services (AWS), vous devez les configurer dans Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="2b268-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="2b268-293">Dans les cas de hello Amazon Web Services (AWS), cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2b268-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="2b268-294">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b268-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b268-295">Connectez-vous à tooyour **Amazon Web Services (AWS)** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2b268-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="2b268-296">Cliquez sur hello **accueil de la Console** icône.</span><span class="sxs-lookup"><span data-stu-id="2b268-296">Click hello **Console Home** icon.</span></span> 
   
    ![Configurer l’authentification unique][11]

3. <span data-ttu-id="2b268-298">Cliquez sur Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="2b268-298">Click Identity and Access Management.</span></span> 
   
    ![Configurer l’authentification unique][28]

4. <span data-ttu-id="2b268-300">Bonjour du tableau de bord, cliquez sur **utilisateurs**, puis cliquez sur **créer de nouveaux utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2b268-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configurer l’authentification unique][29]

5. <span data-ttu-id="2b268-302">Dans la boîte de dialogue Créer un utilisateur hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b268-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Configurer l’authentification unique][30]   
    
    <span data-ttu-id="2b268-304">a.</span><span class="sxs-lookup"><span data-stu-id="2b268-304">a.</span></span> <span data-ttu-id="2b268-305">Bonjour **Entrez les noms d’utilisateur** zones de texte, tapez le nom d’utilisateur Brita Simon (userprincipalname) dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b268-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="2b268-306">b.</span><span class="sxs-lookup"><span data-stu-id="2b268-306">b.</span></span> <span data-ttu-id="2b268-307">Cliquez sur **Create** (Créer).</span><span class="sxs-lookup"><span data-stu-id="2b268-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2b268-308">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b268-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2b268-309">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooAmazon accès Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="2b268-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2b268-311">**tooassign Britta Simon tooAmazon Web Services (AWS), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b268-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="2b268-312">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2b268-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2b268-314">Dans la liste des applications hello, sélectionnez **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="2b268-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="2b268-316">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2b268-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2b268-318">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2b268-318">Click **Add** button.</span></span> <span data-ttu-id="2b268-319">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2b268-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2b268-321">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2b268-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b268-322">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2b268-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b268-323">Sur **sélectionner un rôle** onglet, le rôle approprié de hello select pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="2b268-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="2b268-324">Tous ces rôles sont affichées avec le nom de rôle hello et le nom de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="2b268-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="2b268-325">Ainsi, vous pouvez facilement identifier les rôles AWS hello.</span><span class="sxs-lookup"><span data-stu-id="2b268-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="2b268-326">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2b268-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b268-327">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2b268-327">Testing single sign-on</span></span>

<span data-ttu-id="2b268-328">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2b268-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b268-329">Lorsque vous cliquez sur hello Amazon Web Services (AWS) vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application d’Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="2b268-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2b268-330">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2b268-330">Additional resources</span></span>

* [<span data-ttu-id="2b268-331">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b268-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b268-332">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2b268-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
