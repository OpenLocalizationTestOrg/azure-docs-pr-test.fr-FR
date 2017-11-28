---
title: "Didacticiel : Intégration d’Azure Active Directory avec Domo | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: cc70f8e5013f864d275762bbc1f84bd9677e8c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="d3ba5-103">Didacticiel : intégration d’Azure Active Directory à Domo</span><span class="sxs-lookup"><span data-stu-id="d3ba5-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="d3ba5-104">Dans ce didacticiel, vous apprendrez comment toointegrate Domo avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3ba5-104">In this tutorial, you learn how toointegrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3ba5-105">Intégration Domo à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-105">Integrating Domo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d3ba5-106">Vous pouvez contrôler dans Azure AD qui a accès tooDomo</span><span class="sxs-lookup"><span data-stu-id="d3ba5-106">You can control in Azure AD who has access tooDomo</span></span>
- <span data-ttu-id="d3ba5-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDomo (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-107">You can enable your users tooautomatically get signed-on tooDomo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3ba5-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d3ba5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d3ba5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3ba5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3ba5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d3ba5-110">Prerequisites</span></span>

<span data-ttu-id="d3ba5-111">tooconfigure intégration d’Azure AD avec Domo, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-111">tooconfigure Azure AD integration with Domo, you need hello following items:</span></span>

- <span data-ttu-id="d3ba5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3ba5-113">Un abonnement Domo pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d3ba5-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3ba5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3ba5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3ba5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3ba5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3ba5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3ba5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d3ba5-118">Scenario description</span></span>
<span data-ttu-id="d3ba5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3ba5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3ba5-121">Ajout de Domo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d3ba5-121">Adding Domo from hello gallery</span></span>
2. <span data-ttu-id="d3ba5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-hello-gallery"></a><span data-ttu-id="d3ba5-123">Ajout de Domo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d3ba5-123">Adding Domo from hello gallery</span></span>
<span data-ttu-id="d3ba5-124">intégration de hello tooconfigure de Domo dans Azure AD, vous devez tooadd Domo à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-124">tooconfigure hello integration of Domo into Azure AD, you need tooadd Domo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d3ba5-125">**tooadd Domo à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d3ba5-125">**tooadd Domo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3ba5-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3ba5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d3ba5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d3ba5-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d3ba5-133">Dans la zone de recherche de hello, tapez **Domo**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-133">In hello search box, type **Domo**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="d3ba5-135">Dans le volet de résultats hello, sélectionnez **Domo**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-135">In hello results panel, select **Domo**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3ba5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3ba5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Domo, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d3ba5-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3ba5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Domo est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Domo is tooa user in Azure AD.</span></span> <span data-ttu-id="d3ba5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Domo doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-140">In other words, a link relationship between an Azure AD user and hello related user in Domo needs toobe established.</span></span>

<span data-ttu-id="d3ba5-141">Dans Domo, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-141">In Domo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d3ba5-142">tooconfigure et test Azure AD l’authentification unique avec Domo, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-142">tooconfigure and test Azure AD single sign-on with Domo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d3ba5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d3ba5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3ba5-145">**[Création d’un utilisateur de test Domo](#creating-a-domo-test-user)**  -toohave un équivalent de Britta Simon dans Domo est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - toohave a counterpart of Britta Simon in Domo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3ba5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3ba5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3ba5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3ba5-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Domo.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="d3ba5-150">**tooconfigure Azure AD single sign-on avec Domo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d3ba5-150">**tooconfigure Azure AD single sign-on with Domo, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3ba5-151">Bonjour portail Azure, sur hello **Domo** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-151">In hello Azure portal, on hello **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d3ba5-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="d3ba5-155">Sur hello **Domo domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-155">On hello **Domo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="d3ba5-157">a.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-157">a.</span></span> <span data-ttu-id="d3ba5-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="d3ba5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="d3ba5-159">b.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-159">b.</span></span> <span data-ttu-id="d3ba5-160">Bonjour **identificateur** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="d3ba5-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-161">These values are not real.</span></span> <span data-ttu-id="d3ba5-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d3ba5-163">Contact [équipe de support Client de Domo](mailto:support@domo.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-163">Contact [Domo Client support team](mailto:support@domo.com) tooget these values.</span></span>

4. <span data-ttu-id="d3ba5-164">Domo application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-164">Domo application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="d3ba5-165">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="d3ba5-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="d3ba5-167">Hello suivant capture d’écran montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-167">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="d3ba5-169">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d3ba5-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="d3ba5-170">Attribute Name</span></span> | <span data-ttu-id="d3ba5-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="d3ba5-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="d3ba5-172">name</span><span class="sxs-lookup"><span data-stu-id="d3ba5-172">name</span></span> | <span data-ttu-id="d3ba5-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="d3ba5-173">user.displayname</span></span> |
    | <span data-ttu-id="d3ba5-174">email</span><span class="sxs-lookup"><span data-stu-id="d3ba5-174">email</span></span> | <span data-ttu-id="d3ba5-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="d3ba5-175">user.mail</span></span> |
    
    <span data-ttu-id="d3ba5-176">a.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-176">a.</span></span> <span data-ttu-id="d3ba5-177">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d3ba5-180">b.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-180">b.</span></span> <span data-ttu-id="d3ba5-181">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d3ba5-182">c.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-182">c.</span></span> <span data-ttu-id="d3ba5-183">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d3ba5-184">d.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-184">d.</span></span> <span data-ttu-id="d3ba5-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="d3ba5-186">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-186">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="d3ba5-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d3ba5-188">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="d3ba5-190">Sur hello **Domo Configuration** , cliquez sur **Domo de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-190">On hello **Domo Configuration** section, click **Configure Domo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d3ba5-191">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d3ba5-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

   ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="d3ba5-193">tooconfigure l’authentification unique sur **Domo** côté, vous devez hello toosend téléchargé **certificat**, **ID d’entité SAML**, hello **SAML Single Sign-On Service URL** et hello **URL de déconnexion** trop[équipe de support Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="d3ba5-193">tooconfigure single sign-on on **Domo** side, you need toosend hello downloaded **Certificate**, **SAML Entity ID**, hello **SAML Single Sign-On Service URL** and hello **Sign-Out URL** too[Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="d3ba5-194">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-194">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3ba5-195">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d3ba5-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d3ba5-196">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d3ba5-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3ba5-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3ba5-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3ba5-199">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d3ba5-201">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d3ba5-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3ba5-202">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3ba5-204">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3ba5-206">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3ba5-208">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3ba5-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3ba5-210">a.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-210">a.</span></span> <span data-ttu-id="d3ba5-211">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3ba5-212">b.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-212">b.</span></span> <span data-ttu-id="d3ba5-213">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3ba5-214">c.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-214">c.</span></span> <span data-ttu-id="d3ba5-215">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d3ba5-216">d.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-216">d.</span></span> <span data-ttu-id="d3ba5-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="d3ba5-218">Création d’un utilisateur de test Domo</span><span class="sxs-lookup"><span data-stu-id="d3ba5-218">Creating a Domo test user</span></span>

<span data-ttu-id="d3ba5-219">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Domo.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-219">hello objective of this section is toocreate a user called Britta Simon in Domo.</span></span> <span data-ttu-id="d3ba5-220">Domo prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d3ba5-221">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-221">There is no action item for you in this section.</span></span> <span data-ttu-id="d3ba5-222">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Domo s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-222">A new user is created during an attempt tooaccess Domo if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d3ba5-223">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ba5-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d3ba5-224">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDomo.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDomo.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d3ba5-226">**tooassign Britta Simon tooDomo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d3ba5-226">**tooassign Britta Simon tooDomo, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3ba5-227">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d3ba5-229">Dans la liste des applications hello, sélectionnez **Domo**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-229">In hello applications list, select **Domo**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="d3ba5-231">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d3ba5-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-233">Click **Add** button.</span></span> <span data-ttu-id="d3ba5-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d3ba5-236">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d3ba5-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3ba5-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3ba5-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d3ba5-239">Testing single sign-on</span></span>

<span data-ttu-id="d3ba5-240">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="d3ba5-241">Lorsque vous cliquez sur mosaïque Domo hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Domo application.</span><span class="sxs-lookup"><span data-stu-id="d3ba5-241">When you click hello Domo tile in hello Access Panel, you should get automatically signed-on tooyour Domo application.</span></span>

<span data-ttu-id="d3ba5-242">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3ba5-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3ba5-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d3ba5-243">Additional resources</span></span>

* [<span data-ttu-id="d3ba5-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3ba5-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3ba5-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d3ba5-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

