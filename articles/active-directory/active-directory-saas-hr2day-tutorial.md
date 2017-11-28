---
title: "Didacticiel : Intégration d’Azure Active Directory avec HR2day by Merces | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et HR2day par Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="463c7-103">Didacticiel : Intégration d’Azure Active Directory avec HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="463c7-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="463c7-104">Dans ce didacticiel, vous apprendrez comment toointegrate HR2day par Merces avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="463c7-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="463c7-105">Intégration HR2day par Merces à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="463c7-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="463c7-106">Vous pouvez contrôler dans Azure AD qui a tooHR2day d’accès par Merces.</span><span class="sxs-lookup"><span data-stu-id="463c7-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="463c7-107">Vous pouvez autoriser les utilisateurs tooautomatically obtenir signée tooHR2day de Merces avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463c7-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="463c7-108">Vous pouvez gérer vos comptes dans un emplacement central--hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="463c7-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="463c7-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="463c7-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="463c7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="463c7-110">Prerequisites</span></span>

<span data-ttu-id="463c7-111">tooconfigure intégration d’Azure AD avec HR2day par Merces, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="463c7-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="463c7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="463c7-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="463c7-113">Un abonnement HR2day by Merces pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="463c7-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="463c7-114">Nous ne recommandons pas à l’aide d’un Bonjour de tootest environnement production les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="463c7-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="463c7-115">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="463c7-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="463c7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="463c7-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="463c7-117">Obtenez [un mois d’évaluation gratuite d’Azure AD](https://azure.microsoft.com/pricing/free-trial/) si vous n’y avez pas encore accès.</span><span class="sxs-lookup"><span data-stu-id="463c7-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="463c7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="463c7-118">Scenario description</span></span>
<span data-ttu-id="463c7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="463c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="463c7-120">scénario de Hello est décrite ici se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="463c7-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="463c7-121">Ajout de HR2day par Merces à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="463c7-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="463c7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="463c7-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="463c7-123">Ajouter des HR2day par Merces à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="463c7-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="463c7-124">intégration de hello tooconfigure de HR2day par Merces dans Azure AD, ajouter HR2day par Merces à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="463c7-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="463c7-125">**tooadd HR2day par Merces à partir de la galerie hello, prenez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="463c7-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="463c7-126">Bonjour [portail Azure](https://portal.azure.com), sur hello du volet de navigation gauche, sélectionnez hello **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="463c7-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="463c7-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="463c7-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="463c7-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="463c7-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="463c7-131">tooadd une nouvelle application, sélectionnez hello **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="463c7-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Applications][3]

4. <span data-ttu-id="463c7-133">Dans la zone de recherche de hello, tapez **HR2day par Merces**.</span><span class="sxs-lookup"><span data-stu-id="463c7-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="463c7-135">Dans le volet de résultats hello, sélectionnez **HR2day par Merces**, puis sélectionnez hello **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="463c7-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="463c7-137">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="463c7-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="463c7-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HR2day by Merces avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="463c7-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="463c7-139">Pour toowork de l’authentification unique, Azure AD doit tooknow qui est hello équivalent utilisateur dans HR2day par Merces tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463c7-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="463c7-140">En d’autres termes, vous devez tooestablish un lien entre un utilisateur Azure AD et un utilisateur hello dans HR2day par Merces.</span><span class="sxs-lookup"><span data-stu-id="463c7-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="463c7-141">Dans HR2day par Merces, attribuez hello **nom d’utilisateur** dans Azure AD trop **nom d’utilisateur** relation de hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="463c7-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="463c7-142">tooconfigure et test Azure AD l’authentification unique avec HR2day par Merces, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="463c7-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="463c7-143">[Configurer Azure AD l’authentification unique sur](#configuring-azure-ad-single-sign-on): activer votre toouse les utilisateurs de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="463c7-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="463c7-144">[Créer un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) : Tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="463c7-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="463c7-145">[Créer un HR2day par l’utilisateur de test Merces](#creating-an-hr2day-by-merces-test-user): créer un équivalent de Britta Simon dans HR2day par Merces est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="463c7-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="463c7-146">[Affecter l’utilisateur de test hello Azure AD](#assigning-the-azure-ad-test-user): toouse activer Britta Simon Azure AD l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="463c7-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="463c7-147">[Tester l’authentification unique sur](#testing-single-sign-on): vérifier si la configuration de hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="463c7-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="463c7-148">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="463c7-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="463c7-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre HR2day par Merces application.</span><span class="sxs-lookup"><span data-stu-id="463c7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="463c7-150">**tooconfigure Azure AD single sign-on avec HR2day par Merces, prenez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="463c7-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="463c7-151">Bonjour portail Azure, sur hello **HR2day par Merces** page d’intégration d’application, sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="463c7-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="463c7-153">tooenable l’authentification unique, Bonjour **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification**.</span><span class="sxs-lookup"><span data-stu-id="463c7-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="463c7-155">Bonjour **HR2day par l’URL et le domaine de Merces** conservez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="463c7-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="463c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="463c7-157">a.</span></span> <span data-ttu-id="463c7-158">Bonjour **URL de connexion** zone, tapez une URL à l’aide de hello modèle : `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="463c7-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="463c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="463c7-159">b.</span></span> <span data-ttu-id="463c7-160">Bonjour **identificateur** zone, tapez une URL à l’aide de hello modèle : `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="463c7-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="463c7-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="463c7-161">These values are not real.</span></span> <span data-ttu-id="463c7-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et identificateur.</span><span class="sxs-lookup"><span data-stu-id="463c7-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="463c7-163">Contact hello [HR2day par l’équipe de support client Merces](mailto:servicedesk@merces.nl) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="463c7-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="463c7-164">Sur hello **le certificat de signature SAML** section, sélectionnez **Certificate(Base64)**, puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="463c7-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="463c7-166">Cette section décrit comment tooenable utilisateurs tooauthenticate tooHR2day par Merces avec leur compte dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463c7-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="463c7-167">Pour cela, ils en utilisant la fédération basée sur hello protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="463c7-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="463c7-168">Votre HR2day par Merces application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige le jeton SAML tooyour tooadd attribut personnalisé mappages.</span><span class="sxs-lookup"><span data-stu-id="463c7-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="463c7-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="463c7-169">hello following screenshot shows an example of this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="463c7-171">Avant de pouvoir configurer assertion SAML de hello, vous devez contacter hello [HR2day par l’équipe de support Client de Merces](mailto:servicedesk@merces.nl) et demander la valeur hello d’attribut d’identificateur unique hello pour votre client.</span><span class="sxs-lookup"><span data-stu-id="463c7-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="463c7-172">Vous avez besoin de cette procédure de hello toocomplete valeur dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="463c7-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="463c7-173">Bonjour **l’authentification unique** la boîte de dialogue hello **attributs utilisateur** section, configurer des attributs de jeton SAML hello comme indiqué dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="463c7-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="463c7-174">Ensuite, extrayez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="463c7-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="463c7-175">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="463c7-175">Attribute name</span></span>    |   <span data-ttu-id="463c7-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="463c7-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="463c7-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="463c7-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="463c7-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="463c7-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="463c7-179">a.</span><span class="sxs-lookup"><span data-stu-id="463c7-179">a.</span></span> <span data-ttu-id="463c7-180">tooopen hello **ajouter un attribut** boîte de dialogue, sélectionnez **ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="463c7-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="463c7-183">b.</span><span class="sxs-lookup"><span data-stu-id="463c7-183">b.</span></span> <span data-ttu-id="463c7-184">Bonjour **nom** , tapez **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="463c7-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="463c7-185">c.</span><span class="sxs-lookup"><span data-stu-id="463c7-185">c.</span></span> <span data-ttu-id="463c7-186">À partir de hello **valeur** liste, sélectionnez **Join()**.</span><span class="sxs-lookup"><span data-stu-id="463c7-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="463c7-187">d.</span><span class="sxs-lookup"><span data-stu-id="463c7-187">d.</span></span> <span data-ttu-id="463c7-188">À partir de hello **String1** liste, sélectionnez **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="463c7-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="463c7-189">e.</span><span class="sxs-lookup"><span data-stu-id="463c7-189">e.</span></span> <span data-ttu-id="463c7-190">Pour **chaîne2**, tapez l’identificateur hello est fournie par votre équipe HR2day.</span><span class="sxs-lookup"><span data-stu-id="463c7-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="463c7-191">f.</span><span class="sxs-lookup"><span data-stu-id="463c7-191">f.</span></span> <span data-ttu-id="463c7-192">Bonjour **séparateur** , tapez  **@** .</span><span class="sxs-lookup"><span data-stu-id="463c7-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="463c7-193">g.</span><span class="sxs-lookup"><span data-stu-id="463c7-193">g.</span></span> <span data-ttu-id="463c7-194">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="463c7-194">Select **Ok**.</span></span>

7. <span data-ttu-id="463c7-195">Sélectionnez hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="463c7-195">Select hello **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="463c7-197">Bonjour **HR2day par la Configuration de Merces** section, sélectionnez **HR2day de configurer par Merces** tooopen hello **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="463c7-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="463c7-198">Hello de copie **URL de déconnexion**, **ID d’entité SAML**, et **SAML Sign-On URL du Service unique** de hello **aide-mémoire** section.</span><span class="sxs-lookup"><span data-stu-id="463c7-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="463c7-200">tooconfigure SSO pour hello de votre application, contactez [HR2day par l’équipe de support client Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="463c7-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="463c7-201">Attacher hello téléchargé **Certificate(Base64)** tooyour e-mail du fichier.</span><span class="sxs-lookup"><span data-stu-id="463c7-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="463c7-202">Fournissent également hello **URL de déconnexion**, **ID d’entité SAML**, et **SAML Sign-On URL du Service unique** afin qu’ils peuvent être configurés pour l’intégration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="463c7-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="463c7-203">Indiquez toohello Merces équipe qui a besoin de cette intégration hello toobe ID d’entité avec le modèle de hello **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="463c7-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="463c7-204">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="463c7-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="463c7-205">Après avoir ajouté cette application à partir de hello **Active Directory** > **des Applications d’entreprise** section, sélectionnez hello **Single Sign-On** onglet. Hello d’accès incorporée documentation via hello **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="463c7-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="463c7-206">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello Bonjour [AD Azure incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="463c7-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="463c7-207">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="463c7-207">Create an Azure AD test user</span></span>
<span data-ttu-id="463c7-208">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="463c7-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="463c7-210">**toocreate un utilisateur test dans Azure AD, prenez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="463c7-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="463c7-211">Bonjour **portail Azure**, sur hello du volet de navigation gauche, sélectionnez hello **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="463c7-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="463c7-213">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="463c7-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="463c7-215">tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="463c7-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="463c7-217">Bonjour **utilisateur** boîte de dialogue, hello prennent comme suit :</span><span class="sxs-lookup"><span data-stu-id="463c7-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="463c7-219">a.</span><span class="sxs-lookup"><span data-stu-id="463c7-219">a.</span></span> <span data-ttu-id="463c7-220">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="463c7-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="463c7-221">b.</span><span class="sxs-lookup"><span data-stu-id="463c7-221">b.</span></span> <span data-ttu-id="463c7-222">Bonjour **nom d’utilisateur** boîte, hello de type **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="463c7-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="463c7-223">c.</span><span class="sxs-lookup"><span data-stu-id="463c7-223">c.</span></span> <span data-ttu-id="463c7-224">Sélectionnez **afficher le mot de passe**et noter le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="463c7-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="463c7-225">d.</span><span class="sxs-lookup"><span data-stu-id="463c7-225">d.</span></span> <span data-ttu-id="463c7-226">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="463c7-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="463c7-227">Créer un utilisateur test HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="463c7-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="463c7-228">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans HR2day par Merces.</span><span class="sxs-lookup"><span data-stu-id="463c7-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="463c7-229">les utilisateurs de hello tooadd dans un compte hello HR2day, travailler avec hello [HR2day par l’équipe de support client Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="463c7-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="463c7-230">Si vous avez besoin de toocreate un utilisateur manuellement, contactez hello [HR2day par l’équipe de support client Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="463c7-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="463c7-231">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="463c7-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="463c7-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooHR2day d’accès par Merces.</span><span class="sxs-lookup"><span data-stu-id="463c7-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="463c7-234">**tooassign Britta Simon tooHR2day par Merces, prenez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="463c7-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="463c7-235">Bonjour Azure applications de portail, ouvrez hello voir, allez toohello vue d’annuaire et passez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="463c7-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="463c7-236">Ensuite, sélectionnez **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="463c7-236">Next, select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="463c7-238">Dans la liste des applications hello, sélectionnez **HR2day par Merces**.</span><span class="sxs-lookup"><span data-stu-id="463c7-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="463c7-240">Dans le menu hello hello gauche, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="463c7-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="463c7-242">Sélectionnez hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="463c7-242">Select hello **Add** button.</span></span> <span data-ttu-id="463c7-243">Ensuite, dans hello **ajouter l’affectation** boîte de dialogue, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="463c7-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="463c7-245">Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="463c7-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="463c7-246">Cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="463c7-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="463c7-247">Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.</span><span class="sxs-lookup"><span data-stu-id="463c7-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="463c7-248">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="463c7-248">Test single sign-on</span></span>

<span data-ttu-id="463c7-249">objectif de cette section Hello est tootest votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="463c7-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="463c7-250">Lorsque vous sélectionnez hello HR2day en mosaïque Merces Bonjour volet d’accès, vous automatiquement obtenez connecté tooyour HR2day par Merces application.</span><span class="sxs-lookup"><span data-stu-id="463c7-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="463c7-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="463c7-251">Additional resources</span></span>

* [<span data-ttu-id="463c7-252">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="463c7-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="463c7-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="463c7-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

