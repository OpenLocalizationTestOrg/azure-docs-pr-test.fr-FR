---
title: "Didacticiel : Intégration d’Azure Active Directory à TimeOffManager | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="bbeb0-103">Didacticiel : Intégration d’Azure AD à TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="bbeb0-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="bbeb0-104">Dans ce didacticiel, vous apprendrez comment toointegrate TimeOffManager avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbeb0-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbeb0-105">Intégration de TimeOffManager à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bbeb0-106">Vous pouvez contrôler dans Azure AD qui a accès tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="bbeb0-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="bbeb0-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTimeOffManager (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbeb0-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bbeb0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bbeb0-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbeb0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbeb0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bbeb0-110">Prerequisites</span></span>

<span data-ttu-id="bbeb0-111">tooconfigure intégration d’Azure AD à TimeOffManager, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="bbeb0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbeb0-113">Un abonnement TimeOffManager pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bbeb0-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbeb0-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbeb0-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbeb0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbeb0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbeb0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbeb0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bbeb0-118">Scenario description</span></span>
<span data-ttu-id="bbeb0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbeb0-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbeb0-121">Ajouter des TimeOffManager à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bbeb0-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="bbeb0-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="bbeb0-123">Ajouter des TimeOffManager à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bbeb0-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="bbeb0-124">intégration de hello tooconfigure de TimeOffManager dans Azure AD, vous devez tooadd TimeOffManager à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bbeb0-125">**tooadd TimeOffManager à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbeb0-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbeb0-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bbeb0-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bbeb0-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bbeb0-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bbeb0-133">Dans la zone de recherche de hello, tapez **TimeOffManager**, sélectionnez **TimeOffManager** à partir du Panneau de résultats, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Ajouter à partir de la galerie](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbeb0-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="bbeb0-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TimeOffManager, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bbeb0-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bbeb0-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TimeOffManager est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="bbeb0-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TimeOffManager doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="bbeb0-139">Dans TimeOffManager, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bbeb0-140">tooconfigure et test Azure AD l’authentification unique à TimeOffManager, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bbeb0-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bbeb0-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbeb0-143">**[Créer un utilisateur de test de TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave un équivalent de Britta Simon dans TimeOffManager est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbeb0-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbeb0-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bbeb0-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bbeb0-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="bbeb0-148">**tooconfigure Azure AD single sign-on avec TimeOffManager, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbeb0-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbeb0-149">Bonjour portail Azure, sur hello **TimeOffManager** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bbeb0-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="bbeb0-153">Sur hello **TimeOffManager domaine et les URL** section, hello suivants :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Section Domaine et URL TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="bbeb0-155">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="bbeb0-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bbeb0-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-156">This value is not real.</span></span> <span data-ttu-id="bbeb0-157">Mettre à jour cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="bbeb0-158">Vous pouvez obtenir cette valeur à partir de **l’authentification unique sur la page Paramètres** qui est expliqué plus loin dans le didacticiel de hello ou un Contact [équipe de support technique de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbeb0-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="bbeb0-159">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="bbeb0-161">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooTimeOffManger avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="bbeb0-162">Votre application TimeOffManger attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="bbeb0-163">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="bbeb0-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="bbeb0-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="bbeb0-165">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="bbeb0-165">Attribute Name</span></span> | <span data-ttu-id="bbeb0-166">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="bbeb0-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bbeb0-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="bbeb0-167">Firstname</span></span> |<span data-ttu-id="bbeb0-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="bbeb0-168">User.givenname</span></span> |
    | <span data-ttu-id="bbeb0-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="bbeb0-169">Lastname</span></span> |<span data-ttu-id="bbeb0-170">User.Surname</span><span class="sxs-lookup"><span data-stu-id="bbeb0-170">User.surname</span></span> |
    | <span data-ttu-id="bbeb0-171">Email</span><span class="sxs-lookup"><span data-stu-id="bbeb0-171">Email</span></span> |<span data-ttu-id="bbeb0-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="bbeb0-172">User.mail</span></span> |
    
    <span data-ttu-id="bbeb0-173">a.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-173">a.</span></span>  <span data-ttu-id="bbeb0-174">Pour chaque ligne de données dans la table hello ci-dessus, cliquez sur **ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="bbeb0-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="bbeb0-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="bbeb0-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="bbeb0-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="bbeb0-177">b.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-177">b.</span></span>  <span data-ttu-id="bbeb0-178">Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bbeb0-179">c.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-179">c.</span></span>  <span data-ttu-id="bbeb0-180">Bonjour **valeur d’attribut** zone de texte, valeur de l’attribut select hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="bbeb0-181">d.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-181">d.</span></span>  <span data-ttu-id="bbeb0-182">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="bbeb0-183">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bbeb0-183">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bbeb0-185">Sur hello **TimeOffManager Configuration** , cliquez sur **configurer de TimeOffManager** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bbeb0-186">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bbeb0-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Section Configuration de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="bbeb0-188">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TimeOffManager en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="bbeb0-189">Accédez trop**compte \> Options compte \> paramètres d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="bbeb0-190">![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="bbeb0-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="bbeb0-191">Bonjour **paramètres d’authentification unique** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="bbeb0-192">![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="bbeb0-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="bbeb0-193">a.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-193">a.</span></span> <span data-ttu-id="bbeb0-194">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez hello l’intégralité du certificat dans **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="bbeb0-195">b.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-195">b.</span></span> <span data-ttu-id="bbeb0-196">Dans **émetteur Idp** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="bbeb0-197">c.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-197">c.</span></span> <span data-ttu-id="bbeb0-198">Dans **URL de point de terminaison IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="bbeb0-199">d.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-199">d.</span></span> <span data-ttu-id="bbeb0-200">Dans **Enforce SAML**, sélectionnez **No**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="bbeb0-201">e.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-201">e.</span></span> <span data-ttu-id="bbeb0-202">Dans **Auto-Create Users**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="bbeb0-203">f.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-203">f.</span></span> <span data-ttu-id="bbeb0-204">Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="bbeb0-205">g.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-205">g.</span></span> <span data-ttu-id="bbeb0-206">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="bbeb0-207">Dans **l’authentification unique sur les paramètres** page, de copier la valeur de hello **Assertion Consumer Service URL** et collez-le dans hello **URL de réponse** zone de texte sous **TimeOffManager Domaine et les URL** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="bbeb0-208">![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="bbeb0-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="bbeb0-209">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bbeb0-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bbeb0-210">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bbeb0-211">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbeb0-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbeb0-212">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-212">Create an Azure AD test user</span></span>
<span data-ttu-id="bbeb0-213">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bbeb0-215">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbeb0-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbeb0-216">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbeb0-218">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes --> Tous les utilisateurs](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbeb0-220">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbeb0-222">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbeb0-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbeb0-224">a.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-224">a.</span></span> <span data-ttu-id="bbeb0-225">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbeb0-226">b.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-226">b.</span></span> <span data-ttu-id="bbeb0-227">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbeb0-228">c.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-228">c.</span></span> <span data-ttu-id="bbeb0-229">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bbeb0-230">d.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-230">d.</span></span> <span data-ttu-id="bbeb0-231">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="bbeb0-232">Créer un utilisateur de test TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="bbeb0-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="bbeb0-233">Dans l’ordre tooenable Azure AD les utilisateurs toolog à TimeOffManager, ils doivent être tooTimeOffManager mis en service.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="bbeb0-234">TimeOffManager prend en charge l’approvisionnement juste-à-temps des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="bbeb0-235">Vous n’avez rien à faire.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-235">There is no action item for you.</span></span>  

<span data-ttu-id="bbeb0-236">les utilisateurs de Hello sont automatiquement ajoutés pendant hello première connexion à l’aide de l’authentification unique sur.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="bbeb0-237">Vous pouvez utiliser n’importe quel autre TimeOffManager utilisateur compte outil de création ou API fournie par TimeOffManager tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bbeb0-238">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbeb0-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bbeb0-239">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bbeb0-241">**tooassign Britta Simon tooTimeOffManager, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbeb0-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbeb0-242">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bbeb0-244">Dans la liste des applications hello, sélectionnez **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager dans la liste des applications](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="bbeb0-246">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bbeb0-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-248">Click **Add** button.</span></span> <span data-ttu-id="bbeb0-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bbeb0-251">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bbeb0-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbeb0-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bbeb0-254">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bbeb0-254">Test single sign-on</span></span>

<span data-ttu-id="bbeb0-255">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bbeb0-256">Lorsque vous cliquez sur mosaïque TimeOffManager hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour TimeOffManager application.</span><span class="sxs-lookup"><span data-stu-id="bbeb0-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="bbeb0-257">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbeb0-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbeb0-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bbeb0-258">Additional resources</span></span>

* [<span data-ttu-id="bbeb0-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbeb0-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbeb0-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bbeb0-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

