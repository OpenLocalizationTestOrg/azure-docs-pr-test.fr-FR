---
title: "Didacticiel : Intégration d'Azure Active Directory à Workpath | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="ce49c-103">Didacticiel : Intégration d’Azure Active Directory à Workpath | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="ce49c-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="ce49c-104">Dans ce didacticiel, vous apprendrez comment toointegrate Workpath avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce49c-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce49c-105">Intégration Workpath à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ce49c-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce49c-106">Vous pouvez contrôler dans Azure AD qui a accès tooWorkpath</span><span class="sxs-lookup"><span data-stu-id="ce49c-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="ce49c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkpath (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce49c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ce49c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce49c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce49c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce49c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ce49c-110">Prerequisites</span></span>

<span data-ttu-id="ce49c-111">tooconfigure intégration d’Azure AD avec Workpath, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ce49c-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="ce49c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce49c-113">Un abonnement Workpath pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ce49c-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce49c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ce49c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce49c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ce49c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce49c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ce49c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce49c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce49c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce49c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ce49c-118">Scenario description</span></span>
<span data-ttu-id="ce49c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ce49c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce49c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ce49c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce49c-121">Ajout de Workpath à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ce49c-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="ce49c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="ce49c-123">Ajout de Workpath à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ce49c-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="ce49c-124">intégration de hello tooconfigure de Workpath dans Azure AD, vous devez tooadd Workpath à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ce49c-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce49c-125">**tooadd Workpath à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ce49c-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce49c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ce49c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce49c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce49c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ce49c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ce49c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ce49c-133">Dans la zone de recherche de hello, tapez **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-133">In hello search box, type **Workpath**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="ce49c-135">Dans le volet de résultats hello, sélectionnez **Workpath**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce49c-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce49c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce49c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workpath, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ce49c-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce49c-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Workpath est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce49c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="ce49c-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Workpath doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ce49c-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="ce49c-141">Dans Workpath, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ce49c-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce49c-142">tooconfigure et test Azure AD l’authentification unique avec Workpath, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ce49c-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce49c-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ce49c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce49c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce49c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce49c-145">**[Création d’un utilisateur de test Workpath](#creating-a-workpath-test-user)**  -toohave un équivalent de Britta Simon dans Workpath est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ce49c-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce49c-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ce49c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce49c-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ce49c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce49c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce49c-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Workpath.</span><span class="sxs-lookup"><span data-stu-id="ce49c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="ce49c-150">**tooconfigure Azure AD single sign-on avec Workpath, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ce49c-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce49c-151">Bonjour portail Azure, sur hello **Workpath** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ce49c-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ce49c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="ce49c-155">Sur hello **Workpath domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** mode initié effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce49c-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="ce49c-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce49c-157">a.</span></span> <span data-ttu-id="ce49c-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ce49c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="ce49c-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce49c-159">b.</span></span> <span data-ttu-id="ce49c-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ce49c-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="ce49c-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ce49c-162">Si vous le souhaitez application hello tooconfigure **SP** initiée par le mode, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce49c-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="ce49c-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="ce49c-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce49c-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ce49c-165">These values are not real.</span></span> <span data-ttu-id="ce49c-166">Mettre à jour ces valeurs avec l’URL de connexion réel hello, identificateur et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="ce49c-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="ce49c-167">Contact [équipe de support Workpath](https://help.workpath.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="ce49c-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="ce49c-168">Workpath application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="ce49c-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ce49c-169">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="ce49c-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="ce49c-170">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="ce49c-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ce49c-171">Hello suivant capture d’écran montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="ce49c-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="ce49c-173">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce49c-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ce49c-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="ce49c-174">Attribute Name</span></span> | <span data-ttu-id="ce49c-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="ce49c-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ce49c-176">first_name</span><span class="sxs-lookup"><span data-stu-id="ce49c-176">first_name</span></span> | <span data-ttu-id="ce49c-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ce49c-177">user.givenname</span></span> |
    | <span data-ttu-id="ce49c-178">last_name</span><span class="sxs-lookup"><span data-stu-id="ce49c-178">last_name</span></span> | <span data-ttu-id="ce49c-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="ce49c-179">user.surname</span></span> |
    
    <span data-ttu-id="ce49c-180">a.</span><span class="sxs-lookup"><span data-stu-id="ce49c-180">a.</span></span> <span data-ttu-id="ce49c-181">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ce49c-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ce49c-183">b.</span><span class="sxs-lookup"><span data-stu-id="ce49c-183">b.</span></span> <span data-ttu-id="ce49c-184">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="ce49c-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ce49c-186">c.</span><span class="sxs-lookup"><span data-stu-id="ce49c-186">c.</span></span> <span data-ttu-id="ce49c-187">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="ce49c-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="ce49c-188">d.</span><span class="sxs-lookup"><span data-stu-id="ce49c-188">d.</span></span> <span data-ttu-id="ce49c-189">Laissez hello **Namespace** zone de texte vide.</span><span class="sxs-lookup"><span data-stu-id="ce49c-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="ce49c-190">e.</span><span class="sxs-lookup"><span data-stu-id="ce49c-190">e.</span></span> <span data-ttu-id="ce49c-191">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="ce49c-192">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ce49c-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="ce49c-194">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ce49c-194">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ce49c-196">Sur hello **Workpath Configuration** , cliquez sur **Workpath de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ce49c-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce49c-197">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ce49c-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="ce49c-199">tooconfigure l’authentification unique sur **Workpath** côté, vous devez hello toosend téléchargé **Metadata XML**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="ce49c-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ce49c-200">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ce49c-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce49c-201">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ce49c-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce49c-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce49c-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce49c-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce49c-204">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ce49c-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ce49c-206">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ce49c-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce49c-207">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ce49c-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce49c-209">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce49c-211">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ce49c-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce49c-213">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce49c-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce49c-215">a.</span><span class="sxs-lookup"><span data-stu-id="ce49c-215">a.</span></span> <span data-ttu-id="ce49c-216">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce49c-217">b.</span><span class="sxs-lookup"><span data-stu-id="ce49c-217">b.</span></span> <span data-ttu-id="ce49c-218">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce49c-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce49c-219">c.</span><span class="sxs-lookup"><span data-stu-id="ce49c-219">c.</span></span> <span data-ttu-id="ce49c-220">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce49c-221">d.</span><span class="sxs-lookup"><span data-stu-id="ce49c-221">d.</span></span> <span data-ttu-id="ce49c-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="ce49c-223">Création d’un utilisateur de test Workpath</span><span class="sxs-lookup"><span data-stu-id="ce49c-223">Creating a Workpath test user</span></span>

<span data-ttu-id="ce49c-224">Workpath prend en charge l’approvisionnement juste-à-temps des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ce49c-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="ce49c-225">Une fois l’authentification utilisateurs sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ce49c-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce49c-226">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce49c-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce49c-227">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWorkpath.</span><span class="sxs-lookup"><span data-stu-id="ce49c-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ce49c-229">**tooassign Britta Simon tooWorkpath, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ce49c-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce49c-230">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ce49c-232">Dans la liste des applications hello, sélectionnez **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-232">In hello applications list, select **Workpath**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="ce49c-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ce49c-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-236">Click **Add** button.</span></span> <span data-ttu-id="ce49c-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ce49c-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ce49c-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce49c-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce49c-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ce49c-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce49c-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ce49c-242">Testing single sign-on</span></span>

<span data-ttu-id="ce49c-243">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ce49c-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ce49c-244">Lorsque vous cliquez sur mosaïque Workpath hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Workpath application.</span><span class="sxs-lookup"><span data-stu-id="ce49c-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="ce49c-245">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce49c-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce49c-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ce49c-246">Additional resources</span></span>

* [<span data-ttu-id="ce49c-247">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce49c-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce49c-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ce49c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

