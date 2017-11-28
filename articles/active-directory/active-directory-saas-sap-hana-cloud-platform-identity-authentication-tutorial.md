---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform Identity Authentication | Microsoft Docs"
description: "Découvrez comment tooconfigure sur l’authentification unique entre Azure Active Directory et SAP HANA Cloud Platform Identity authentification."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="40b77-103">Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="40b77-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="40b77-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAP HANA Cloud Platform Identity authentification avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40b77-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="40b77-105">Authentification d’identité SAP HANA Cloud Platform est utilisée comme un proxy IdP tooaccess SAP les applications à l’aide d’Azure AD comme hello IdP principal.</span><span class="sxs-lookup"><span data-stu-id="40b77-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="40b77-106">Intégration d’authentification d’identité SAP HANA Cloud Platform à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="40b77-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="40b77-107">Vous pouvez contrôler dans Azure AD qui a accès tooSAP application</span><span class="sxs-lookup"><span data-stu-id="40b77-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="40b77-108">Vous pouvez activer vos utilisateurs tooautomatically get tooSAP signé sur applications-session unique (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="40b77-109">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="40b77-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="40b77-110">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40b77-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="40b77-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40b77-111">Prerequisites</span></span>

<span data-ttu-id="40b77-112">tooconfigure intégration d’Azure AD avec l’authentification d’identité SAP HANA Cloud Platform, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="40b77-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="40b77-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-113">An Azure AD subscription</span></span>
- <span data-ttu-id="40b77-114">Un abonnement **SAP HANA Cloud Platform Identity Authentication** compatible avec l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="40b77-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="40b77-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="40b77-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="40b77-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="40b77-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40b77-117">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40b77-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="40b77-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40b77-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40b77-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="40b77-119">Scenario description</span></span>
<span data-ttu-id="40b77-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="40b77-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="40b77-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="40b77-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40b77-122">Ajout d’authentification d’identité plateforme Cloud SAP HANA à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="40b77-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="40b77-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="40b77-124">Avant de plonger dans les détails techniques hello, il est concepts de hello toounderstand vital que vous allez toolook à.</span><span class="sxs-lookup"><span data-stu-id="40b77-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="40b77-125">Hello fédération d’authentification d’identité SAP HANA Cloud Platform et Azure Active Directory vous permet de tooimplement l’authentification unique entre les applications ou services protégés par AAD (comme un IdP) avec les applications SAP et les services protégés par identité de plateforme Cloud SAP HANA Authentification.</span><span class="sxs-lookup"><span data-stu-id="40b77-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="40b77-126">Actuellement, l’authentification de SAP HANA Cloud Platform Identity agit comme un fournisseur d’identité Proxy tooSAP-applications.</span><span class="sxs-lookup"><span data-stu-id="40b77-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="40b77-127">Azure Active Directory joue à son tour hello début du fournisseur d’identité dans ce programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="40b77-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="40b77-128">Hello suivant le diagramme illustre ce comportement :</span><span class="sxs-lookup"><span data-stu-id="40b77-128">hello following diagram illustrates this:</span></span>    

![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="40b77-130">Avec cette configuration, votre client SAP HANA Cloud Platform Identity Authentication sera configuré en tant qu’application approuvée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40b77-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="40b77-131">Toutes les applications SAP et les services souhaités tooprotect par le biais de cette manière sont configurés par la suite dans la console de gestion de l’authentification de SAP HANA Cloud Platform Identity hello !</span><span class="sxs-lookup"><span data-stu-id="40b77-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="40b77-132">Cela signifie que cette autorisation pour accorder l’accès tooSAP applications et services tootake de besoins sur place de l’authentification d’identité SAP HANA Cloud Platform pour ce type de configuration (comme autorisation tooconfiguring exécutée dans Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="40b77-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="40b77-133">En configurant l’authentification d’identité plateforme Cloud SAP HANA en tant qu’application via hello Azure Active Directory Marketplace, vous n’avez pas besoin tootake administration de la configuration des revendications individuelles nécessaires / assertions SAML et les transformations nécessaires tooproduce un jeton d’authentification valide pour les applications SAP.</span><span class="sxs-lookup"><span data-stu-id="40b77-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="40b77-134">Actuellement, l’authentification unique web n’a été testée que par les deux parties.</span><span class="sxs-lookup"><span data-stu-id="40b77-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="40b77-135">Les flux nécessaires à la communication application-API ou API-API devraient fonctionner mais n’ont pas encore été testés.</span><span class="sxs-lookup"><span data-stu-id="40b77-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="40b77-136">Ils seront testés dans le cadre des activités à venir.</span><span class="sxs-lookup"><span data-stu-id="40b77-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="40b77-137">Ajouter l’authentification d’identité plateforme Cloud SAP HANA à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="40b77-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="40b77-138">intégration de hello tooconfigure d’authentification d’identité plateforme Cloud SAP HANA dans Azure AD, vous devez tooadd authentification d’identité plateforme Cloud SAP HANA à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="40b77-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="40b77-139">**tooadd SAP HANA Cloud Platform authentification de l’identité à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40b77-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="40b77-140">Bonjour [ **portail de gestion Azure**](https://portal.azure.com)sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="40b77-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40b77-142">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="40b77-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="40b77-143">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40b77-143">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="40b77-145">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="40b77-147">Dans la zone de recherche de hello, tapez **authentification d’identité SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="40b77-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="40b77-149">Dans le volet de résultats hello, sélectionnez **authentification d’identité SAP HANA Cloud Platform**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="40b77-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="40b77-151">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="40b77-152">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP HANA Cloud Platform Identity Authentication, à partir d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="40b77-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40b77-153">Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’authentification de SAP HANA Cloud Platform Identity est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40b77-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="40b77-154">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de l’authentification d’identité SAP HANA Cloud Platform hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="40b77-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="40b77-155">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’authentification d’identité SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="40b77-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="40b77-156">tooconfigure et l’authentification unique d’Azure AD avec l’authentification d’identité SAP HANA Cloud Platform de test, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="40b77-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="40b77-157">**[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="40b77-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="40b77-158">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40b77-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40b77-159">**[Création d’un utilisateur de test de l’authentification de SAP HANA Cloud Platform Identity](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave de Britta Simon dans SAP HANA Cloud Platform authentification d’identité qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="40b77-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="40b77-160">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="40b77-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40b77-161">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="40b77-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="40b77-162">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="40b77-163">Dans cette section, vous activez l’authentification unique de Azure AD dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application d’authentification d’identité SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="40b77-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="40b77-164">Application d’authentification d’identité SAP HANA Cloud Platform attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="40b77-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="40b77-165">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="40b77-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="40b77-166">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="40b77-166">hello following screenshot shows an example for this.</span></span>

![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="40b77-168">**tooconfigure l’authentification unique d’Azure AD avec l’authentification SAP HANA Cloud Platform Identity, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40b77-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="40b77-169">Dans le portail de gestion Azure hello, sur hello **authentification d’identité SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="40b77-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="40b77-171">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="40b77-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique][5]

3. <span data-ttu-id="40b77-173">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, si votre application SAP attend un attribut, par exemple « firstName ».</span><span class="sxs-lookup"><span data-stu-id="40b77-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="40b77-174">Boîte de dialogue hello SAML attributs du jeton, ajoutez l’attribut de « firstName » de hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="40b77-175">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40b77-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Configurer l’authentification unique][6]

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="40b77-178">Bonjour **nom de l’attribut** textbox, le nom « firstName » de l’attribut de type hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="40b77-179">À partir de hello **valeur d’attribut** liste, la valeur d’attribut hello Sélectionnez « user.givenname ».</span><span class="sxs-lookup"><span data-stu-id="40b77-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="40b77-180">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="40b77-180">Click **Ok**.</span></span>

4. <span data-ttu-id="40b77-181">Sur hello **URL et le domaine d’authentification de l’identité SAP HANA Cloud Platform** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40b77-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="40b77-183">Bonjour **URL de connexion** zone de texte, tapez le signe de hello sur l’URL pour l’application de SAP hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="40b77-184">Bonjour **identificateur** zone de texte, valeur hello de type modèle :`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="40b77-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="40b77-185">Si vous ne connaissez pas cette valeur, veuillez suivre documentation d’authentification d’identité SAP HANA Cloud Platform hello sur [locataire SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="40b77-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="40b77-186">Sur hello **Configuration de l’authentification SAP HANA Cloud Platform Identity** , cliquez sur **configuration SAP HANA Cloud Platform identité de l’authentification** tooopen **configurer l’authentification** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40b77-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="40b77-187">Ensuite, cliquez sur **des métadonnées XML SAML** et enregistrez le fichier hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="40b77-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="40b77-190">tooget SSO configuré pour votre application, accédez tooSAP HANA Cloud Platform Identity authentification Console d’Administration.</span><span class="sxs-lookup"><span data-stu-id="40b77-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="40b77-191">URL de Hello a hello modèle :`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="40b77-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="40b77-192">Ensuite, suivez les documentation hello sur SAP HANA Cloud Platform Identity authentification trop[configurer Microsoft Azure AD en tant que fournisseur d’identité d’entreprise au niveau d’authentification d’identité SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="40b77-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="40b77-193">Dans le portail de gestion Azure hello, cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="40b77-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="40b77-194">Continuer hello suit uniquement si vous souhaitez tooadd et activez l’authentification unique pour une autre application SAP.</span><span class="sxs-lookup"><span data-stu-id="40b77-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="40b77-195">Répétez les étapes sous hello section « Ajout SAP HANA Cloud Platform authentification d’identité à partir de la galerie de hello » tooadd une autre instance de l’authentification d’identité SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="40b77-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="40b77-196">Dans le portail de gestion Azure hello, sur hello **authentification d’identité SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **lié Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="40b77-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configurer l’authentification liée](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="40b77-198">Puis, enregistrez hello configuration.</span><span class="sxs-lookup"><span data-stu-id="40b77-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="40b77-199">nouvelle application de Hello reposera sur configuration de SSO hello pour l’application SAP précédente hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="40b77-200">Vérifiez que vous utilisez hello même fournisseurs d’identité d’entreprise dans la Console Administration de l’authentification de la plateforme Cloud SAP HANA identité de hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="40b77-201">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-201">Create an Azure AD test user</span></span>
<span data-ttu-id="40b77-202">objectif Hello de cette section est hello nouveau portail appelé Britta Simon toocreate un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="40b77-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="40b77-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40b77-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="40b77-205">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="40b77-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40b77-207">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="40b77-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40b77-209">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40b77-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40b77-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40b77-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="40b77-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40b77-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="40b77-214">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40b77-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="40b77-215">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="40b77-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="40b77-216">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="40b77-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="40b77-217">Créer un utilisateur de test SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="40b77-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="40b77-218">Vous n’avez pas besoin toocreate un utilisateur sur l’authentification d’identité SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="40b77-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="40b77-219">Les utilisateurs qui se trouvent dans le magasin de l’utilisateur hello Azure AD peuvent utiliser la fonctionnalité SSO de hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="40b77-220">Authentification d’identité SAP HANA Cloud Platform prend en charge l’option de fédération des identités hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="40b77-221">Cette option permet de hello application toocheck si les utilisateurs de hello authentifiés par le fournisseur d’identité d’entreprise hello existent dans hello utilisateur magasin de SAP HANA Cloud Platform authentification d’identité.</span><span class="sxs-lookup"><span data-stu-id="40b77-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="40b77-222">Dans le paramètre par défaut de hello, hello option de fédération d’identité est désactivé.</span><span class="sxs-lookup"><span data-stu-id="40b77-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="40b77-223">Si la fédération des identités est activée, seuls les utilisateurs hello qui sont importés dans l’authentification d’identité SAP HANA Cloud Platform sont hello à tooaccess en mesure de l’application.</span><span class="sxs-lookup"><span data-stu-id="40b77-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="40b77-224">Pour plus d’informations sur comment tooenable ou désactiver la fédération d’identité avec l’authentification SAP HANA Cloud Platform Identity, consultez Activer la fédération d’identité avec l’authentification SAP HANA Cloud Platform Identity dans [configurer la fédération d’identité avec hello utilisateur magasin de SAP HANA Cloud Platform authentification d’identité. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="40b77-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="40b77-225">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="40b77-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="40b77-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooSAP accès authentification d’identité HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="40b77-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="40b77-228">**tooassign Britta Simon tooSAP authentification d’identité HANA Cloud Platform, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40b77-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="40b77-229">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40b77-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="40b77-231">Dans la liste des applications hello, sélectionnez **authentification d’identité SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="40b77-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="40b77-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40b77-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="40b77-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="40b77-235">Click **Add** button.</span></span> <span data-ttu-id="40b77-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40b77-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="40b77-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="40b77-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40b77-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40b77-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40b77-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="40b77-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="40b77-241">Test single sign-on</span></span>

<span data-ttu-id="40b77-242">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="40b77-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="40b77-243">Lorsque vous cliquez sur mosaïque d’authentification d’identité SAP HANA Cloud Platform hello Bonjour volet d’accès, vous devez obtenir l’application d’authentification d’identité SAP HANA Cloud Platform automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="40b77-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="40b77-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="40b77-244">Additional resources</span></span>

* [<span data-ttu-id="40b77-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40b77-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40b77-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="40b77-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png