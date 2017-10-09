---
title: "Didacticiel : intégration d’Azure Active Directory à IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et IBM Kenexa enquête Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="3cb6c-103">Didacticiel : intégration d’Azure Active Directory à IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3cb6c-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="3cb6c-104">Dans ce didacticiel, vous apprendrez comment toointegrate IBM Kenexa enquête Enterprise avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cb6c-105">Intégration IBM Kenexa enquête Enterprise à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3cb6c-106">Vous pouvez contrôler dans Azure AD qui a accès tooIBM Kenexa enquête Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="3cb6c-107">Vous pouvez activer vos informations d’identification tooautomatically utilisateurs tooIBM Kenexa enquête Enterprise à l’aide de l’authentification unique (SSO) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3cb6c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="3cb6c-109">Si vous souhaitez tooknow plus sur les logiciels en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cb6c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3cb6c-110">Prerequisites</span></span>

<span data-ttu-id="3cb6c-111">tooconfigure intégration d’Azure AD avec IBM Kenexa enquête Enterprise, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="3cb6c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cb6c-113">Un abonnement IBM Kenexa Survey Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3cb6c-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cb6c-114">Lorsque vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas utiliser un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="3cb6c-115">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="3cb6c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cb6c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cb6c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3cb6c-118">Scenario description</span></span>
<span data-ttu-id="3cb6c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="3cb6c-120">scénario Hello décrite dans le didacticiel de hello se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="3cb6c-121">Ajout d’IBM Kenexa enquête entreprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3cb6c-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="3cb6c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb6c-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="3cb6c-123">Ajouter IBM Kenexa enquête entreprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3cb6c-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="3cb6c-124">tooconfigure l’intégration d’entreprise d’enquête IBM Kenexa hello dans Azure AD, ajouter IBM Kenexa enquête entreprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3cb6c-125">tooadd IBM Kenexa enquête entreprise à partir de la galerie hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="3cb6c-126">Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, cliquez sur dans hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="3cb6c-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="3cb6c-130">tooadd une application, cliquez sur hello **nouvelle application** bouton.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-130">tooadd an application, click hello **New application** button.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="3cb6c-132">Dans la zone de recherche de hello, tapez **IBM Kenexa enquête entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="3cb6c-134">Dans la liste des résultats hello, sélectionnez **IBM Kenexa enquête entreprise**, puis cliquez sur hello **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa enquête Enterprise dans la liste des résultats hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3cb6c-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb6c-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3cb6c-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec IBM Kenexa Survey Enterprise au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3cb6c-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3cb6c-138">Pour l’authentification unique toowork, Azure AD doit équivalent de tooidentify hello IBM Kenexa enquête entreprise utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="3cb6c-139">En d’autres termes, Azure AD doit établir un lien entre un utilisateur Azure AD et un utilisateur associé dans IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="3cb6c-140">relation de lien de hello tooestablish, attribuer une valeur hello Hello **nom d’utilisateur** dans IBM Kenexa enquête entreprise en tant que valeur hello Hello **nom d’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="3cb6c-141">tooconfigure et test de l’authentification unique d’Azure AD avec IBM Kenexa enquête Enterprise, hello complète des blocs de construction dans hello deux sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="3cb6c-142">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb6c-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="3cb6c-143">Dans cette section, vous activez Azure Active Directory SSO Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise d’enquête IBM Kenexa en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="3cb6c-144">Bonjour portail Azure, sur hello **IBM Kenexa enquête entreprise** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique dans IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="3cb6c-146">Bonjour **l’authentification unique** la boîte de dialogue hello **Mode** boîte, sélectionnez **SAML-authentification** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="3cb6c-148">Bonjour **URL et le domaine d’entreprise enquête IBM Kenexa** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique de domaine et d’URL d’IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="3cb6c-150">a.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-150">a.</span></span> <span data-ttu-id="3cb6c-151">Bonjour **identificateur** zone de texte, tapez un URL avec hello modèle :`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="3cb6c-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="3cb6c-152">b.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-152">b.</span></span> <span data-ttu-id="3cb6c-153">Bonjour **URL de réponse** zone de texte, tapez un URL avec hello modèle :`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="3cb6c-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cb6c-154">Hello les valeurs précédentes ne sont pas réelles.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-154">hello preceding values are not real.</span></span> <span data-ttu-id="3cb6c-155">Mettre à jour avec l’identificateur de réel hello et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="3cb6c-156">tooobtain hello valeurs réelles, contact hello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="3cb6c-157">Sous **le certificat de signature SAML**, cliquez sur **certificat (Base64)**, puis enregistrez ordinateur de tooyour de fichier de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![lien de téléchargement du certificat (Base64) Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="3cb6c-159">Hello application d’entreprise d’enquête IBM Kenexa attend les assertions de sécurité Assertions Markup Language (SAML) tooreceive hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé toohello configuration des mappages de vos attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="3cb6c-160">Hello valeur de revendication d’identificateur d’utilisateur hello en réponse de hello doit correspondre à hello ID de l’authentification unique est configuré dans le système de Kenexa hello.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="3cb6c-161">toomap hello identificateur d’utilisateur approprié dans votre organisation en tant que l’authentification unique Internet Datagram Protocol (IDP), travailler avec hello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="3cb6c-162">Par défaut, AD Azure définit identificateur hello de l’utilisateur en tant que valeur de nom principal (UPN) utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="3cb6c-163">Vous pouvez modifier cette valeur sur hello **attribut** onglet, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="3cb6c-164">intégration de Hello fonctionne uniquement après avoir terminé hello mappage correctement.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![boîte de dialogue des attributs utilisateur Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="3cb6c-166">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-166">Click **Save**.</span></span>

    ![Hello configurer l’authentification unique sur bouton Enregistrer](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3cb6c-168">tooopen hello **configurer l’authentification** fenêtre, sous **Configuration d’entreprise enquête IBM Kenexa**, cliquez sur **configurer IBM Kenexa enquête entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![lien d’entreprise d’enquête configurer IBM Kenexa Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="3cb6c-170">Hello de copie **URL de déconnexion**, **ID d’entité SAML**, et **SAML-Service URL d’authentification** valeurs hello **aide-mémoire** section.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="3cb6c-171">Bonjour **configurer l’authentification** fenêtre, sous **aide-mémoire**, hello de copie **URL de déconnexion**, **ID d’entité SAML**, et  **SAML-Service URL d’authentification** valeurs.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="3cb6c-172">tooconfigure SSO sur hello **IBM Kenexa enquête entreprise** côté, envoyer hello téléchargé **certificat (Base64)**, **URL de déconnexion**, **ID d’entité SAML**, et **SAML-Service URL d’authentification** valeurs toohello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="3cb6c-173">Vous pouvez faire référence tooa la version concise de ces instructions Bonjour [portail Azure](https://portal.azure.com) lors de la configuration de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="3cb6c-174">Après avoir ajouté l’application hello de hello **Active Directory** > **des Applications d’entreprise** , cliquez simplement sur hello **l’authentification unique** onglet, puis accédez à Hello incorporé documentation via hello **Configuration** section à hello fin.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="3cb6c-175">toolearn en savoir plus sur la fonctionnalité de documentation embedded hello, consultez [AD Azure incorporé documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3cb6c-176">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb6c-176">Create an Azure AD test user</span></span>
<span data-ttu-id="3cb6c-177">Dans cette section, vous créez utilisateur test Britta Simon Bonjour portail Azure en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Créer un utilisateur de test Azure AD][100]

1. <span data-ttu-id="3cb6c-179">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cb6c-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cb6c-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cb6c-185">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cb6c-187">a.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-187">a.</span></span> <span data-ttu-id="3cb6c-188">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cb6c-189">b.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-189">b.</span></span> <span data-ttu-id="3cb6c-190">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3cb6c-191">c.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-191">c.</span></span> <span data-ttu-id="3cb6c-192">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3cb6c-193">d.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-193">d.</span></span> <span data-ttu-id="3cb6c-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="3cb6c-195">Créer un utilisateur de test IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3cb6c-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="3cb6c-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="3cb6c-197">toocreate les utilisateurs de hello système IBM Kenexa enquête Enterprise et hello de mappage des ID de l’authentification unique pour les, vous pouvez travailler avec hello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cb6c-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="3cb6c-198">Cette valeur d’ID de l’authentification unique doit également être mappé la valeur de l’identificateur utilisateur toohello d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="3cb6c-199">Vous pouvez modifier ce paramètre par défaut sur hello **attribut** onglet.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3cb6c-200">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb6c-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3cb6c-201">Dans cette section, vous activez utilisateur Britta Simon toouse Azure SSO en accordant l’accès tooIBM Kenexa enquête Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="3cb6c-203">l’utilisateur tooassign Britta Simon tooIBM Kenexa enquête entreprise, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3cb6c-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="3cb6c-204">Bonjour portail Azure, ouvrez hello **Applications** afficher, accédez toohello **active** afficher, sélectionnez **des applications d’entreprise**, puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Hello « applications d’entreprise » et les liens « Toutes les applications »][201] 

2. <span data-ttu-id="3cb6c-206">Bonjour **Applications** liste, sélectionnez **IBM Kenexa enquête entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![lien d’IBM Kenexa enquête entreprise Hello dans la liste des Applications hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="3cb6c-208">Dans le volet gauche de hello, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-208">In hello left pane, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="3cb6c-210">Cliquez sur hello **ajouter** bouton, puis, dans hello **ajouter l’affectation** volet, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="3cb6c-212">Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="3cb6c-213">Bonjour **utilisateurs et groupes** boîte de dialogue, cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="3cb6c-214">Bonjour **ajouter l’affectation** boîte de dialogue, cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3cb6c-215">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3cb6c-215">Test single sign-on</span></span>

<span data-ttu-id="3cb6c-216">Dans cette section, vous testez votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="3cb6c-217">Lorsque vous cliquez sur hello **IBM Kenexa enquête entreprise** vignette dans hello volet d’accès, vous devez être connecté automatiquement dans tooyour application d’entreprise d’enquête IBM Kenexa.</span><span class="sxs-lookup"><span data-stu-id="3cb6c-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cb6c-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3cb6c-218">Additional resources</span></span>

* [<span data-ttu-id="3cb6c-219">Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cb6c-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cb6c-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3cb6c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
