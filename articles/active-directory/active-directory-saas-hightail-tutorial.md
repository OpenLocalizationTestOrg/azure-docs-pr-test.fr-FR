---
title: "Didacticiel : Intégration d’Azure Active Directory à Hightail | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="7f450-103">Didacticiel : Intégration d’Azure Active Directory à Hightail</span><span class="sxs-lookup"><span data-stu-id="7f450-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="7f450-104">Dans ce didacticiel, vous apprendrez comment toointegrate Hightail avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f450-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f450-105">Intégration Hightail à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7f450-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f450-106">Vous pouvez contrôler dans Azure AD qui a accès tooHightail</span><span class="sxs-lookup"><span data-stu-id="7f450-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="7f450-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHightail (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f450-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7f450-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f450-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f450-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f450-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7f450-110">Prerequisites</span></span>

<span data-ttu-id="7f450-111">tooconfigure intégration d’Azure AD avec Hightail, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7f450-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="7f450-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f450-113">Un abonnement Hightail pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7f450-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f450-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7f450-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f450-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7f450-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f450-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7f450-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f450-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f450-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f450-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7f450-118">Scenario description</span></span>
<span data-ttu-id="7f450-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7f450-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f450-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7f450-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f450-121">Ajout de Hightail à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7f450-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="7f450-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="7f450-123">Ajout de Hightail à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7f450-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="7f450-124">intégration de hello tooconfigure de Hightail dans Azure AD, vous devez tooadd Hightail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7f450-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f450-125">**tooadd Hightail à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f450-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f450-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7f450-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f450-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7f450-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f450-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7f450-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7f450-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7f450-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7f450-133">Dans la zone de recherche de hello, tapez **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="7f450-133">In hello search box, type **Hightail**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="7f450-135">Dans le volet de résultats hello, sélectionnez **Hightail**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f450-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f450-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f450-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Hightail avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7f450-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f450-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Hightail est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f450-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="7f450-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Hightail doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7f450-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="7f450-141">Dans Hightail, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f450-142">tooconfigure et test Azure AD l’authentification unique avec Hightail, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7f450-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f450-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7f450-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f450-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f450-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f450-145">**[Création d’un utilisateur de test Hightail](#creating-a-hightail-test-user)**  -toohave un équivalent de Britta Simon dans Hightail est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7f450-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f450-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f450-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f450-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7f450-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f450-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f450-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Hightail.</span><span class="sxs-lookup"><span data-stu-id="7f450-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="7f450-150">**tooconfigure Azure AD single sign-on avec Hightail, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f450-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f450-151">Bonjour portail Azure, sur hello **Hightail** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7f450-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7f450-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f450-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="7f450-155">Sur hello **Hightail de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f450-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="7f450-157">Bonjour **URL de réponse** zone de texte, tapez l’URL hello en tant que :`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="7f450-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f450-158">Hello valeur précédente n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="7f450-158">hello preceding value is not real value.</span></span> <span data-ttu-id="7f450-159">Vous mettrez à jour la valeur de hello avec l’URL de réponse réelle hello, qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="7f450-160">Sur hello **Hightail de domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f450-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="7f450-162">a.</span><span class="sxs-lookup"><span data-stu-id="7f450-162">a.</span></span> <span data-ttu-id="7f450-163">Cliquez sur hello **afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="7f450-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="7f450-164">b.</span><span class="sxs-lookup"><span data-stu-id="7f450-164">b.</span></span> <span data-ttu-id="7f450-165">Bonjour **URL de connexion** zone de texte, tapez l’URL hello en tant que :`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="7f450-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="7f450-166">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7f450-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="7f450-168">Hightail application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="7f450-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7f450-169">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="7f450-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="7f450-170">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Mémoire »** onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="7f450-171">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="7f450-171">hello following screenshot shows an example for this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="7f450-173">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f450-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7f450-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="7f450-174">Attribute Name</span></span> | <span data-ttu-id="7f450-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="7f450-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7f450-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="7f450-176">FirstName</span></span> | <span data-ttu-id="7f450-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7f450-177">user.givenname</span></span> |
    | <span data-ttu-id="7f450-178">LastName</span><span class="sxs-lookup"><span data-stu-id="7f450-178">LastName</span></span> | <span data-ttu-id="7f450-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="7f450-179">user.surname</span></span> |
    | <span data-ttu-id="7f450-180">Email</span><span class="sxs-lookup"><span data-stu-id="7f450-180">Email</span></span> | <span data-ttu-id="7f450-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="7f450-181">user.mail</span></span> |    
    | <span data-ttu-id="7f450-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="7f450-182">UserIdentity</span></span> | <span data-ttu-id="7f450-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="7f450-183">user.mail</span></span> |
    
    <span data-ttu-id="7f450-184">a.</span><span class="sxs-lookup"><span data-stu-id="7f450-184">a.</span></span> <span data-ttu-id="7f450-185">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7f450-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="7f450-188">b.</span><span class="sxs-lookup"><span data-stu-id="7f450-188">b.</span></span> <span data-ttu-id="7f450-189">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7f450-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7f450-190">c.</span><span class="sxs-lookup"><span data-stu-id="7f450-190">c.</span></span> <span data-ttu-id="7f450-191">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7f450-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="7f450-192">d.</span><span class="sxs-lookup"><span data-stu-id="7f450-192">d.</span></span> <span data-ttu-id="7f450-193">Laissez hello **Namespace** vide.</span><span class="sxs-lookup"><span data-stu-id="7f450-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="7f450-194">e.</span><span class="sxs-lookup"><span data-stu-id="7f450-194">e.</span></span> <span data-ttu-id="7f450-195">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f450-195">Click **Ok**.</span></span>

7. <span data-ttu-id="7f450-196">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7f450-196">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7f450-198">Sur hello **Hightail de Configuration** , cliquez sur **configurer Hightail** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7f450-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7f450-199">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7f450-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="7f450-201">Avant de configurer hello Single Sign On à l’application de Hightail, veuillez liste blanche votre domaine de messagerie avec Hightail d’équipe afin que tous les hello les utilisateurs qui sont à l’aide de ce domaine, utilisez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f450-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="7f450-202">tooget SSO configuré pour votre application, vous devez locataire de Hightail toosign sur tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7f450-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="7f450-203">a.</span><span class="sxs-lookup"><span data-stu-id="7f450-203">a.</span></span> <span data-ttu-id="7f450-204">Dans le menu hello haut de hello, cliquez sur hello **compte** onglet et sélectionnez **SAML de configurer**.</span><span class="sxs-lookup"><span data-stu-id="7f450-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="7f450-206">b.</span><span class="sxs-lookup"><span data-stu-id="7f450-206">b.</span></span> <span data-ttu-id="7f450-207">Sélectionnez la case à cocher hello de **activer l’authentification SAML**.</span><span class="sxs-lookup"><span data-stu-id="7f450-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="7f450-209">c.</span><span class="sxs-lookup"><span data-stu-id="7f450-209">c.</span></span> <span data-ttu-id="7f450-210">Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **le certificat de signature de jetons SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7f450-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="7f450-212">d.</span><span class="sxs-lookup"><span data-stu-id="7f450-212">d.</span></span> <span data-ttu-id="7f450-213">Bonjour **SAML autorité (fournisseur d’identité)** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** copiés à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f450-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="7f450-215">e.</span><span class="sxs-lookup"><span data-stu-id="7f450-215">e.</span></span> <span data-ttu-id="7f450-216">Si vous le souhaitez application hello tooconfigure **mode initialisée par IDP** sélectionnez **« Journal dans initiée par le fournisseur d’identité (IdP) »**.</span><span class="sxs-lookup"><span data-stu-id="7f450-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="7f450-217">En **mode lancé par le fournisseur de service**, sélectionnez **Service Provider (SP) initiated log in** (Connexion lancée par le fournisseur de service).</span><span class="sxs-lookup"><span data-stu-id="7f450-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="7f450-219">f.</span><span class="sxs-lookup"><span data-stu-id="7f450-219">f.</span></span> <span data-ttu-id="7f450-220">Copier l’URL de consommateur SAML hello pour votre instance et le coller dans **URL de réponse** zone de texte dans **Hightail de domaine et les URL** section sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f450-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="7f450-221">g.</span><span class="sxs-lookup"><span data-stu-id="7f450-221">g.</span></span> <span data-ttu-id="7f450-222">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f450-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f450-223">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="7f450-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f450-224">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f450-225">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f450-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f450-226">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f450-227">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="7f450-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7f450-229">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f450-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f450-230">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7f450-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f450-232">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7f450-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f450-234">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f450-236">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f450-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f450-238">a.</span><span class="sxs-lookup"><span data-stu-id="7f450-238">a.</span></span> <span data-ttu-id="7f450-239">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f450-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f450-240">b.</span><span class="sxs-lookup"><span data-stu-id="7f450-240">b.</span></span> <span data-ttu-id="7f450-241">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f450-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f450-242">c.</span><span class="sxs-lookup"><span data-stu-id="7f450-242">c.</span></span> <span data-ttu-id="7f450-243">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7f450-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f450-244">d.</span><span class="sxs-lookup"><span data-stu-id="7f450-244">d.</span></span> <span data-ttu-id="7f450-245">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f450-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="7f450-246">Création d’un utilisateur de test Hightail</span><span class="sxs-lookup"><span data-stu-id="7f450-246">Creating a Hightail test user</span></span>

<span data-ttu-id="7f450-247">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Hightail.</span><span class="sxs-lookup"><span data-stu-id="7f450-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="7f450-248">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="7f450-248">There is no action item for you in this section.</span></span> <span data-ttu-id="7f450-249">Hightail prend en charge l’approvisionnement des utilisateurs de juste-à-temps en fonction des revendications personnalisées hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="7f450-250">Si vous avez configuré des revendications personnalisées hello comme indiqué dans la section de hello  **[configuration Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  ci-dessus, un utilisateur est automatiquement créé dans une application hello qu’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="7f450-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="7f450-251">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="7f450-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7f450-252">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f450-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7f450-253">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHightail.</span><span class="sxs-lookup"><span data-stu-id="7f450-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7f450-255">**tooassign Britta Simon tooHightail, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f450-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f450-256">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7f450-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7f450-258">Dans la liste des applications hello, sélectionnez **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="7f450-258">In hello applications list, select **Hightail**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="7f450-260">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7f450-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7f450-262">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7f450-262">Click **Add** button.</span></span> <span data-ttu-id="7f450-263">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7f450-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7f450-265">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7f450-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f450-266">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7f450-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f450-267">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7f450-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f450-268">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7f450-268">Testing single sign-on</span></span>

<span data-ttu-id="7f450-269">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7f450-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f450-270">Lorsque vous cliquez sur mosaïque Hightail hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Hightail application.</span><span class="sxs-lookup"><span data-stu-id="7f450-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7f450-271">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7f450-271">Additional resources</span></span>

* [<span data-ttu-id="7f450-272">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f450-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f450-273">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7f450-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

