---
title: "Didacticiel : Intégration d’Azure Active Directory à Onit | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="c05e0-103">Didacticiel : Intégration d’Azure Active Directory avec Onit</span><span class="sxs-lookup"><span data-stu-id="c05e0-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="c05e0-104">Dans ce didacticiel, vous apprendrez comment toointegrate Onit avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c05e0-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c05e0-105">Intégration d’Onit à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c05e0-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c05e0-106">Vous pouvez contrôler dans Azure AD qui a accès tooOnit.</span><span class="sxs-lookup"><span data-stu-id="c05e0-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="c05e0-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOnit (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c05e0-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c05e0-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c05e0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c05e0-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c05e0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c05e0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c05e0-110">Prerequisites</span></span>

<span data-ttu-id="c05e0-111">tooconfigure intégration d’Azure AD à Onit, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c05e0-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="c05e0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c05e0-113">Un abonnement Onit pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c05e0-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c05e0-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c05e0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c05e0-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c05e0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c05e0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c05e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c05e0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c05e0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c05e0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c05e0-118">Scenario description</span></span>

<span data-ttu-id="c05e0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c05e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c05e0-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c05e0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c05e0-121">Ajout d’Onit à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c05e0-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="c05e0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="c05e0-123">Ajout d’Onit à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c05e0-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="c05e0-124">intégration de hello tooconfigure de Onit dans Azure AD, vous devez tooadd Onit à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c05e0-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c05e0-125">**tooadd Onit à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c05e0-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05e0-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c05e0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="c05e0-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c05e0-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="c05e0-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c05e0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="c05e0-133">Dans la zone de recherche de hello, tapez **Onit**, sélectionnez **Onit** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c05e0-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de Onit Bonjour](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c05e0-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05e0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c05e0-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Onit, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c05e0-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c05e0-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Onit est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c05e0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="c05e0-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Onit doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c05e0-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="c05e0-139">Dans Onit, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c05e0-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c05e0-140">tooconfigure et test Azure AD l’authentification unique avec Onit, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c05e0-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c05e0-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c05e0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c05e0-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c05e0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c05e0-143">**[Créer un utilisateur de test Onit](#create-an-onit-test-user)**  -toohave un équivalent de Britta Simon dans Onit est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c05e0-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c05e0-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c05e0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c05e0-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c05e0-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c05e0-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05e0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c05e0-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Onit.</span><span class="sxs-lookup"><span data-stu-id="c05e0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="c05e0-148">**tooconfigure Azure AD single sign-on avec Onit, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c05e0-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05e0-149">Bonjour portail Azure, sur hello **Onit** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c05e0-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c05e0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="c05e0-153">Sur hello **Onit domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c05e0-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="c05e0-155">a.</span><span class="sxs-lookup"><span data-stu-id="c05e0-155">a.</span></span> <span data-ttu-id="c05e0-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="c05e0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="c05e0-157">b.</span><span class="sxs-lookup"><span data-stu-id="c05e0-157">b.</span></span> <span data-ttu-id="c05e0-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="c05e0-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c05e0-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c05e0-159">These values are not real.</span></span> <span data-ttu-id="c05e0-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="c05e0-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c05e0-161">Contact [équipe de support Client de Onit](https://www.onit.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c05e0-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="c05e0-162">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="c05e0-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="c05e0-164">Application Onit attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="c05e0-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c05e0-165">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c05e0-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="c05e0-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Mémoire »** onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c05e0-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="c05e0-167">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="c05e0-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="c05e0-169">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c05e0-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c05e0-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="c05e0-170">Attribute Name</span></span> | <span data-ttu-id="c05e0-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="c05e0-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="c05e0-172">email</span><span class="sxs-lookup"><span data-stu-id="c05e0-172">email</span></span> | <span data-ttu-id="c05e0-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="c05e0-173">user.mail</span></span> |
    
    <span data-ttu-id="c05e0-174">a.</span><span class="sxs-lookup"><span data-stu-id="c05e0-174">a.</span></span> <span data-ttu-id="c05e0-175">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c05e0-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c05e0-178">b.</span><span class="sxs-lookup"><span data-stu-id="c05e0-178">b.</span></span> <span data-ttu-id="c05e0-179">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c05e0-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c05e0-180">c.</span><span class="sxs-lookup"><span data-stu-id="c05e0-180">c.</span></span> <span data-ttu-id="c05e0-181">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c05e0-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="c05e0-182">d.</span><span class="sxs-lookup"><span data-stu-id="c05e0-182">d.</span></span> <span data-ttu-id="c05e0-183">Laissez hello **Namespace** vide.</span><span class="sxs-lookup"><span data-stu-id="c05e0-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="c05e0-184">e.</span><span class="sxs-lookup"><span data-stu-id="c05e0-184">e.</span></span> <span data-ttu-id="c05e0-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-185">Click **Ok**.</span></span>

7. <span data-ttu-id="c05e0-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c05e0-186">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c05e0-188">Sur hello **Onit Configuration** , cliquez sur **Onit de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c05e0-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c05e0-189">Hello de copie **URL de déconnexion, SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c05e0-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="c05e0-191">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Onit en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c05e0-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="c05e0-192">Dans le menu hello haut de hello, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="c05e0-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="c05e0-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="c05e0-194">Cliquez sur **Edit Corporation**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="c05e0-195">![Modifier l’entreprise](./media/active-directory-saas-onit-tutorial/IC791175.png "Modifier l’entreprise")</span><span class="sxs-lookup"><span data-stu-id="c05e0-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="c05e0-196">Cliquez sur hello **sécurité** onglet.</span><span class="sxs-lookup"><span data-stu-id="c05e0-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="c05e0-197">![Modifier les informations de l’entreprise](./media/active-directory-saas-onit-tutorial/IC791176.png "Modifier les informations de l’entreprise")</span><span class="sxs-lookup"><span data-stu-id="c05e0-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="c05e0-198">Sur hello **sécurité** onglet, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c05e0-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="c05e0-199">![Authentification unique](./media/active-directory-saas-onit-tutorial/IC791177.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="c05e0-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="c05e0-200">a.</span><span class="sxs-lookup"><span data-stu-id="c05e0-200">a.</span></span> <span data-ttu-id="c05e0-201">Comme **Authentication Strategy**, sélectionnez **Single Sign On and Password**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="c05e0-202">b.</span><span class="sxs-lookup"><span data-stu-id="c05e0-202">b.</span></span> <span data-ttu-id="c05e0-203">Dans **Idp Target URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c05e0-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c05e0-204">c.</span><span class="sxs-lookup"><span data-stu-id="c05e0-204">c.</span></span> <span data-ttu-id="c05e0-205">Dans **URL de déconnexion Idp** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c05e0-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c05e0-206">d.</span><span class="sxs-lookup"><span data-stu-id="c05e0-206">d.</span></span> <span data-ttu-id="c05e0-207">Dans **Idp Cert Fingerprint (SHA1)** zone de texte, collez hello **l’empreinte numérique** valeur de certificat, ce qui vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c05e0-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="c05e0-208">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c05e0-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c05e0-209">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c05e0-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c05e0-210">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c05e0-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c05e0-211">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05e0-211">Create an Azure AD test user</span></span>

<span data-ttu-id="c05e0-212">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c05e0-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c05e0-214">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c05e0-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05e0-215">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="c05e0-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c05e0-217">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c05e0-219">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c05e0-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c05e0-221">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c05e0-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c05e0-223">a.</span><span class="sxs-lookup"><span data-stu-id="c05e0-223">a.</span></span> <span data-ttu-id="c05e0-224">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c05e0-225">b.</span><span class="sxs-lookup"><span data-stu-id="c05e0-225">b.</span></span> <span data-ttu-id="c05e0-226">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c05e0-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c05e0-227">c.</span><span class="sxs-lookup"><span data-stu-id="c05e0-227">c.</span></span> <span data-ttu-id="c05e0-228">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="c05e0-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c05e0-229">d.</span><span class="sxs-lookup"><span data-stu-id="c05e0-229">d.</span></span> <span data-ttu-id="c05e0-230">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="c05e0-231">Création d’un utilisateur de test Onit</span><span class="sxs-lookup"><span data-stu-id="c05e0-231">Create an Onit test user</span></span>

<span data-ttu-id="c05e0-232">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Onit, vous devez les configurer dans Onit.</span><span class="sxs-lookup"><span data-stu-id="c05e0-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="c05e0-233">Dans le cas de hello d’Onit, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c05e0-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="c05e0-234">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c05e0-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05e0-235">Ouverture de session tooyour **Onit** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c05e0-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="c05e0-236">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="c05e0-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="c05e0-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="c05e0-238">Sur hello **ajouter un utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c05e0-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="c05e0-239">![Ajouter un utilisateur](./media/active-directory-saas-onit-tutorial/IC791181.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="c05e0-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="c05e0-240">Hello de type **nom** et hello **adresse de messagerie** d’un Azure valide compte AD tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="c05e0-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="c05e0-241">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="c05e0-242">titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="c05e0-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c05e0-243">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05e0-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c05e0-244">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOnit.</span><span class="sxs-lookup"><span data-stu-id="c05e0-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="c05e0-246">**tooassign Britta Simon tooOnit, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c05e0-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05e0-247">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c05e0-249">Dans la liste des applications hello, sélectionnez **Onit**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-249">In hello applications list, select **Onit**.</span></span>

    ![lien d’Onit Hello dans la liste des Applications hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="c05e0-251">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="c05e0-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-253">Click **Add** button.</span></span> <span data-ttu-id="c05e0-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="c05e0-256">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c05e0-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c05e0-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c05e0-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c05e0-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c05e0-259">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c05e0-259">Test single sign-on</span></span>

<span data-ttu-id="c05e0-260">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c05e0-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c05e0-261">Lorsque vous cliquez sur mosaïque Onit hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Onit application.</span><span class="sxs-lookup"><span data-stu-id="c05e0-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="c05e0-262">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c05e0-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c05e0-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c05e0-263">Additional resources</span></span>

* [<span data-ttu-id="c05e0-264">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c05e0-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c05e0-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c05e0-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

