---
title: "Didacticiel : Intégration d’Azure Active Directory avec myPolicies | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="a0e9c-103">Didacticiel : Intégration d’Azure Active Directory avec myPolicies</span><span class="sxs-lookup"><span data-stu-id="a0e9c-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="a0e9c-104">Dans ce didacticiel, vous apprendrez comment myPolicies toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0e9c-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0e9c-105">Intégration myPolicies à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a0e9c-106">Vous pouvez contrôler dans Azure AD qui a accès toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="a0e9c-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="a0e9c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté toomyPolicies (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0e9c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a0e9c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a0e9c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0e9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0e9c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a0e9c-110">Prerequisites</span></span>

<span data-ttu-id="a0e9c-111">tooconfigure intégration d’Azure AD avec myPolicies, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="a0e9c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0e9c-113">Un abonnement myPolicies pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a0e9c-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0e9c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0e9c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0e9c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0e9c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0e9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0e9c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a0e9c-118">Scenario description</span></span>
<span data-ttu-id="a0e9c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0e9c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0e9c-121">Ajout de myPolicies à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a0e9c-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="a0e9c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="a0e9c-123">Ajout de myPolicies à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a0e9c-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="a0e9c-124">intégration de hello tooconfigure de myPolicies dans Azure AD, vous devez myPolicies tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a0e9c-125">**myPolicies tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0e9c-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0e9c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0e9c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a0e9c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a0e9c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a0e9c-133">Dans la zone de recherche de hello, tapez **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-133">In hello search box, type **myPolicies**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="a0e9c-135">Dans le volet de résultats hello, sélectionnez **myPolicies**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0e9c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0e9c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec myPolicies sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a0e9c-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0e9c-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans myPolicies est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="a0e9c-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans myPolicies doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="a0e9c-141">Dans myPolicies, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a0e9c-142">tooconfigure et test Azure AD l’authentification unique avec myPolicies, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a0e9c-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a0e9c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0e9c-145">**[Création d’un utilisateur de test myPolicies](#creating-a-mypolicies-test-user)**  -toohave un homologue de Britta Simon dans myPolicies est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0e9c-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0e9c-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0e9c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0e9c-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application myPolicies.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="a0e9c-150">**tooconfigure Azure AD single sign-on avec myPolicies, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0e9c-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0e9c-151">Bonjour portail Azure, sur hello **myPolicies** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a0e9c-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="a0e9c-155">Sur hello **myPolicies domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="a0e9c-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-157">a.</span></span> <span data-ttu-id="a0e9c-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="a0e9c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="a0e9c-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-159">b.</span></span> <span data-ttu-id="a0e9c-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="a0e9c-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0e9c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-161">These values are not real.</span></span> <span data-ttu-id="a0e9c-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="a0e9c-163">Contact [myPolicies l’équipe de support](mailto:support@mypolicies.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="a0e9c-164">application de myPolicies Hello attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="a0e9c-165">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="a0e9c-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a0e9c-167">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="a0e9c-169">Cliquez sur **afficher et modifier tous les autres attributs utilisateur** case à cocher Bonjour **attributs utilisateur** tooexpand hello attributs de section.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="a0e9c-170">Effectuer hello comme suit sur chaque hello affichée les attributs-</span><span class="sxs-lookup"><span data-stu-id="a0e9c-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="a0e9c-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="a0e9c-171">Attribute Name</span></span> | <span data-ttu-id="a0e9c-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="a0e9c-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="a0e9c-173">givenname</span><span class="sxs-lookup"><span data-stu-id="a0e9c-173">givenname</span></span> | <span data-ttu-id="a0e9c-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a0e9c-174">user.givenname</span></span> |
    | <span data-ttu-id="a0e9c-175">surname</span><span class="sxs-lookup"><span data-stu-id="a0e9c-175">surname</span></span> | <span data-ttu-id="a0e9c-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="a0e9c-176">user.surname</span></span> |
    | <span data-ttu-id="a0e9c-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="a0e9c-177">emailaddress</span></span> | <span data-ttu-id="a0e9c-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="a0e9c-178">user.mail</span></span> |
    | <span data-ttu-id="a0e9c-179">name</span><span class="sxs-lookup"><span data-stu-id="a0e9c-179">name</span></span> | <span data-ttu-id="a0e9c-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="a0e9c-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="a0e9c-181">a.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-181">a.</span></span> <span data-ttu-id="a0e9c-182">Cliquez sur hello de hello attribut tooopen **modifier l’attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a0e9c-184">b.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-184">b.</span></span> <span data-ttu-id="a0e9c-185">Supprimer la valeur d’URL de hello de hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="a0e9c-186">c.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-186">c.</span></span> <span data-ttu-id="a0e9c-187">Cliquez sur **Ok** paramètre hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="a0e9c-188">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="a0e9c-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a0e9c-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a0e9c-192">Sur hello **myPolicies Configuration** , cliquez sur **configurer myPolicies** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a0e9c-193">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a0e9c-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="a0e9c-195">tooconfigure l’authentification unique sur **myPolicies** côté, vous devez hello toosend téléchargé **Certificate(Base64)** et **SAML Sign-On URL du Service unique** trop[myPolicies l’équipe de support](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="a0e9c-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="a0e9c-196">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a0e9c-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a0e9c-197">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a0e9c-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0e9c-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0e9c-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0e9c-200">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a0e9c-202">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0e9c-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0e9c-203">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0e9c-205">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0e9c-207">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0e9c-209">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0e9c-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0e9c-211">a.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-211">a.</span></span> <span data-ttu-id="a0e9c-212">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0e9c-213">b.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-213">b.</span></span> <span data-ttu-id="a0e9c-214">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0e9c-215">c.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-215">c.</span></span> <span data-ttu-id="a0e9c-216">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a0e9c-217">d.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-217">d.</span></span> <span data-ttu-id="a0e9c-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="a0e9c-219">Création d’un utilisateur de test myPolicies</span><span class="sxs-lookup"><span data-stu-id="a0e9c-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="a0e9c-220">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans myPolicies.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="a0e9c-221">Travailler avec [myPolicies l’équipe de support](mailto:support@mypolicies.com) pour ajouter des utilisateurs de hello de plateforme de myPolicies hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="a0e9c-222">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a0e9c-223">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0e9c-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a0e9c-224">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès toomyPolicies.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a0e9c-226">**tooassign Britta Simon toomyPolicies, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0e9c-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0e9c-227">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a0e9c-229">Dans la liste des applications hello, sélectionnez **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-229">In hello applications list, select **myPolicies**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="a0e9c-231">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a0e9c-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-233">Click **Add** button.</span></span> <span data-ttu-id="a0e9c-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a0e9c-236">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a0e9c-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0e9c-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0e9c-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a0e9c-239">Testing single sign-on</span></span>

<span data-ttu-id="a0e9c-240">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a0e9c-241">Lorsque vous cliquez sur hello myPolicies vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour myPolicies application.</span><span class="sxs-lookup"><span data-stu-id="a0e9c-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="a0e9c-242">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a0e9c-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0e9c-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a0e9c-243">Additional resources</span></span>

* [<span data-ttu-id="a0e9c-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0e9c-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0e9c-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a0e9c-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

