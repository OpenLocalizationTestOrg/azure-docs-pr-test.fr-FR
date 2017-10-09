---
title: "Didacticiel : Intégration d’Azure Active Directory à MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et transfert MOVEit - intégration d’Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="fe389-103">Didacticiel : Intégration d’Azure Active Directory à MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="fe389-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="fe389-104">Dans ce didacticiel, vous apprendrez comment toointegrate MOVEit transfert - intégration d’Azure AD avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe389-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe389-105">Intégration de transfert MOVEit - intégration d’Azure AD avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fe389-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fe389-106">Vous pouvez contrôler dans Azure AD qui a accès tooMOVEit transfert - intégration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="fe389-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMOVEit transfert - intégration d’Azure AD (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fe389-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fe389-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fe389-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe389-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe389-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fe389-110">Prerequisites</span></span>

<span data-ttu-id="fe389-111">tooconfigure intégration d’Azure AD avec transfert MOVEit - intégration d’Azure AD, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fe389-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="fe389-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe389-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe389-113">Un abonnement MOVEit Transfer - Azure AD integration pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fe389-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe389-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fe389-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe389-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="fe389-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe389-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fe389-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe389-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe389-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe389-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fe389-118">Scenario description</span></span>
<span data-ttu-id="fe389-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fe389-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe389-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="fe389-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe389-121">Ajout de transfert MOVEit - intégration d’Azure AD à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fe389-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="fe389-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe389-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="fe389-123">Ajout de transfert MOVEit - intégration d’Azure AD à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fe389-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="fe389-124">intégration de hello tooconfigure de transfert de MOVEit - intégration d’Azure AD dans Azure AD, vous devez tooadd MOVEit transfert - intégration d’Azure AD à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fe389-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fe389-125">**tooadd MOVEit transfert - intégration d’Azure AD à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fe389-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe389-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="fe389-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="fe389-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fe389-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fe389-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fe389-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="fe389-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fe389-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="fe389-133">Dans la zone de recherche de hello, tapez **MOVEit transfert - intégration d’Azure AD**, sélectionnez **MOVEit transfert - intégration d’Azure AD** à partir du volet de résultats, puis sur **ajouter** hello tooadd de bouton application.</span><span class="sxs-lookup"><span data-stu-id="fe389-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Transfert de MOVEit - intégration d’Azure AD dans la liste des résultats hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fe389-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe389-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fe389-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MOVEit Transfer - Azure AD integration avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fe389-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe389-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans MOVEit transfert - intégration d’Azure AD est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="fe389-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans MOVEit transfert - intégration d’Azure AD doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="fe389-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="fe389-139">Dans transfert MOVEit - intégration d’Azure AD, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="fe389-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fe389-140">tooconfigure et test Azure AD l’authentification unique avec transfert MOVEit - intégration d’Azure AD, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="fe389-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fe389-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fe389-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fe389-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe389-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe389-143">**[Créer un transfert MOVEit - utilisateur de test d’intégration Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  intégration d’Azure AD - toohave de Britta Simon dans MOVEit transfert contrepartie - qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fe389-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe389-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fe389-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe389-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="fe389-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fe389-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe389-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fe389-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre transfert MOVEit - application d’intégration Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="fe389-148">**tooconfigure Azure AD single sign-on avec MOVEit transfert - intégration d’Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fe389-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe389-149">Bonjour portail Azure, sur hello **MOVEit transfert - intégration d’Azure AD** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fe389-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="fe389-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fe389-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="fe389-153">Sur hello **MOVEit transfert - URL et intégration d’Azure AD domaine** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe389-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="fe389-155">a.</span><span class="sxs-lookup"><span data-stu-id="fe389-155">a.</span></span> <span data-ttu-id="fe389-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="fe389-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="fe389-157">b.</span><span class="sxs-lookup"><span data-stu-id="fe389-157">b.</span></span> <span data-ttu-id="fe389-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="fe389-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="fe389-159">c.</span><span class="sxs-lookup"><span data-stu-id="fe389-159">c.</span></span> <span data-ttu-id="fe389-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="fe389-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="fe389-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="fe389-161">These values are not real.</span></span> <span data-ttu-id="fe389-162">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="fe389-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="fe389-163">Vous pouvez faire référence à ces valeurs ultérieurement en **URL du Service fournisseur de métadonnées** section ou contactez [MOVEit transfert - équipe de prise en charge des clients Azure AD intégration](https://community.ipswitch.com/s/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="fe389-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="fe389-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fe389-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="fe389-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fe389-166">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="fe389-168">Ouverture de session tooyour client de transfert de MOVEit en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fe389-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="fe389-169">Dans le volet de navigation gauche hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="fe389-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Section Paramètres côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="fe389-171">Cliquez sur le lien **Authentification unique** qui se trouve sous **Stratégies de sécurité -> Authentification des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fe389-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Stratégies de sécurité côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="fe389-173">Cliquez sur le document de métadonnées du lien toodownload hello hello URL des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="fe389-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![URL de métadonnées du fournisseur de service](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="fe389-175">Vérifiez **entityID** correspond à **identificateur** Bonjour **MOVEit transfert - URL et intégration d’Azure AD domaine** section.</span><span class="sxs-lookup"><span data-stu-id="fe389-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="fe389-176">Vérifiez **AssertionConsumerService** emplacement URL correspond à **URL de réponse** Bonjour **MOVEit transfert - URL et intégration d’Azure AD domaine** section.</span><span class="sxs-lookup"><span data-stu-id="fe389-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="fe389-178">Cliquez sur **ajouter un fournisseur d’identité** bouton tooadd un nouveau fournisseur d’identité fédérée.</span><span class="sxs-lookup"><span data-stu-id="fe389-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Ajouter un fournisseur d’identité](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="fe389-180">Cliquez sur **Parcourir...**  tooselect hello du fichier de métadonnées que vous avez téléchargé à partir du portail Azure, puis cliquez sur **ajouter un fournisseur d’identité** hello de tooupload téléchargé le fichier.</span><span class="sxs-lookup"><span data-stu-id="fe389-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Fournisseur d’identité SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="fe389-182">Sélectionnez «**Oui**» en tant que **activé** Bonjour **modifier les paramètres de fournisseur d’identité fédérée...**  page, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fe389-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Paramètres de fournisseur d’identité fédérée](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="fe389-184">Bonjour **modifier fédéré identité du fournisseur de paramètres utilisateur** page, effectuer hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="fe389-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Modifier les paramètres de fournisseur d’identité fédérée](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="fe389-186">a.</span><span class="sxs-lookup"><span data-stu-id="fe389-186">a.</span></span> <span data-ttu-id="fe389-187">Sélectionnez **SAML NameID** comme **Nom de connexion**.</span><span class="sxs-lookup"><span data-stu-id="fe389-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="fe389-188">b.</span><span class="sxs-lookup"><span data-stu-id="fe389-188">b.</span></span> <span data-ttu-id="fe389-189">Sélectionnez **autres** en tant que **nom complet** et Bonjour **nom de l’attribut** zone de texte, insérez les valeur hello : `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="fe389-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="fe389-190">c.</span><span class="sxs-lookup"><span data-stu-id="fe389-190">c.</span></span> <span data-ttu-id="fe389-191">Sélectionnez **autres** en tant que **messagerie** et Bonjour **nom de l’attribut** zone de texte, insérez les valeur hello : `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="fe389-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="fe389-192">d.</span><span class="sxs-lookup"><span data-stu-id="fe389-192">d.</span></span> <span data-ttu-id="fe389-193">Sélectionnez **Oui** sous **Auto-create account on signon** (Créer automatiquement un compte lors de l’authentification).</span><span class="sxs-lookup"><span data-stu-id="fe389-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="fe389-194">e.</span><span class="sxs-lookup"><span data-stu-id="fe389-194">e.</span></span> <span data-ttu-id="fe389-195">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fe389-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="fe389-196">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="fe389-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fe389-197">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="fe389-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fe389-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe389-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fe389-199">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe389-199">Create an Azure AD test user</span></span>

<span data-ttu-id="fe389-200">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="fe389-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="fe389-202">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fe389-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe389-203">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="fe389-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fe389-205">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fe389-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fe389-207">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fe389-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fe389-209">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe389-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fe389-211">a.</span><span class="sxs-lookup"><span data-stu-id="fe389-211">a.</span></span> <span data-ttu-id="fe389-212">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe389-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe389-213">b.</span><span class="sxs-lookup"><span data-stu-id="fe389-213">b.</span></span> <span data-ttu-id="fe389-214">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe389-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fe389-215">c.</span><span class="sxs-lookup"><span data-stu-id="fe389-215">c.</span></span> <span data-ttu-id="fe389-216">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="fe389-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fe389-217">d.</span><span class="sxs-lookup"><span data-stu-id="fe389-217">d.</span></span> <span data-ttu-id="fe389-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fe389-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="fe389-219">Créer un utilisateur de test MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="fe389-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="fe389-220">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans transfert MOVEit - intégration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="fe389-221">MOVEit Transfer - Azure AD integration prend en charge l’approvisionnement juste-à-temps que vous avez activé.</span><span class="sxs-lookup"><span data-stu-id="fe389-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="fe389-222">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="fe389-222">There is no action item for you in this section.</span></span> <span data-ttu-id="fe389-223">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess MOVEit transfert - intégration d’Azure AD s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="fe389-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="fe389-224">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [MOVEit transfert - équipe de prise en charge des clients Azure AD intégration](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="fe389-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fe389-225">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe389-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fe389-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMOVEit transfert - intégration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="fe389-228">**tooassign Britta Simon tooMOVEit transfert - intégration d’Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fe389-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe389-229">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fe389-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fe389-231">Dans la liste des applications hello, sélectionnez **MOVEit transfert - intégration d’Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="fe389-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Hello MOVEit transfert - intégration d’Azure AD de lien dans la liste des Applications hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="fe389-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fe389-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="fe389-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fe389-235">Click **Add** button.</span></span> <span data-ttu-id="fe389-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fe389-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="fe389-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="fe389-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fe389-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fe389-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe389-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fe389-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fe389-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fe389-241">Test single sign-on</span></span>

<span data-ttu-id="fe389-242">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="fe389-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="fe389-243">Lorsque vous cliquez sur hello MOVEit transfert - vignette de l’intégration d’Azure AD dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour MOVEit transfert - application d’intégration Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe389-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fe389-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fe389-244">Additional resources</span></span>

* [<span data-ttu-id="fe389-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe389-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe389-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fe389-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

