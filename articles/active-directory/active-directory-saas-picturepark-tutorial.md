---
title: "Didacticiel : Intégration d’Azure Active Directory avec Picturepark | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="88695-103">Didacticiel : Intégration d’Azure Active Directory avec Picturepark</span><span class="sxs-lookup"><span data-stu-id="88695-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="88695-104">Dans ce didacticiel, vous apprendrez comment toointegrate Picturepark avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88695-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88695-105">Intégration de Picturepark à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="88695-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88695-106">Vous pouvez contrôler dans Azure AD qui a accès tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="88695-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="88695-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPicturepark (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88695-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="88695-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="88695-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88695-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88695-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="88695-110">Prerequisites</span></span>

<span data-ttu-id="88695-111">tooconfigure intégration d’Azure AD à Picturepark, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="88695-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="88695-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88695-113">Un abonnement Picturepark pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="88695-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88695-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="88695-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88695-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="88695-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88695-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="88695-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88695-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88695-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88695-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="88695-118">Scenario description</span></span>
<span data-ttu-id="88695-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="88695-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88695-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="88695-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88695-121">Ajout de Picturepark à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="88695-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="88695-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="88695-123">Ajout de Picturepark à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="88695-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="88695-124">intégration de hello tooconfigure de Picturepark dans Azure AD, vous devez tooadd Picturepark à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="88695-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88695-125">**tooadd Picturepark à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="88695-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88695-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="88695-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88695-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="88695-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88695-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="88695-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="88695-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="88695-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="88695-133">Dans la zone de recherche de hello, tapez **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="88695-133">In hello search box, type **Picturepark**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="88695-135">Dans le volet de résultats hello, sélectionnez **Picturepark**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="88695-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88695-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88695-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Picturepark sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="88695-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88695-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Picturepark est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88695-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="88695-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Picturepark doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="88695-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="88695-141">Dans Picturepark, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="88695-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="88695-142">tooconfigure et test Azure AD l’authentification unique à Picturepark, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="88695-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88695-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="88695-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88695-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88695-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88695-145">**[Création d’un utilisateur de test de Picturepark](#creating-a-picturepark-test-user)**  -toohave un équivalent de Britta Simon dans Picturepark est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="88695-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88695-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="88695-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88695-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="88695-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88695-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88695-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Picturepark.</span><span class="sxs-lookup"><span data-stu-id="88695-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="88695-150">**tooconfigure Azure AD single sign-on avec Picturepark, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="88695-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="88695-151">Bonjour portail Azure, sur hello **Picturepark** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="88695-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="88695-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="88695-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="88695-155">Sur hello **Picturepark domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="88695-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="88695-157">a.</span><span class="sxs-lookup"><span data-stu-id="88695-157">a.</span></span> <span data-ttu-id="88695-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="88695-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="88695-159">b.</span><span class="sxs-lookup"><span data-stu-id="88695-159">b.</span></span> <span data-ttu-id="88695-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="88695-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="88695-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="88695-161">These values are not real.</span></span> <span data-ttu-id="88695-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="88695-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="88695-163">Contact [équipe de support Client de Picturepark](https://picturepark.com/about/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="88695-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="88695-164">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="88695-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="88695-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="88695-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88695-168">Sur hello **Picturepark Configuration** , cliquez sur **configurer de Picturepark** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="88695-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="88695-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="88695-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="88695-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Picturepark en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="88695-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="88695-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **outils d’administration**, puis cliquez sur **Console de gestion**.</span><span class="sxs-lookup"><span data-stu-id="88695-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="88695-173">![Console de gestion](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console de gestion")</span><span class="sxs-lookup"><span data-stu-id="88695-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="88695-174">Cliquez sur **Authentication**, puis sur **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="88695-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="88695-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="88695-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="88695-176">Bonjour **configuration du fournisseur d’identité** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="88695-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="88695-177">![Configuration du fournisseur d’identité](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuration du fournisseur d’identité")</span><span class="sxs-lookup"><span data-stu-id="88695-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="88695-178">a.</span><span class="sxs-lookup"><span data-stu-id="88695-178">a.</span></span> <span data-ttu-id="88695-179">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="88695-179">Click **Add**.</span></span>
  
    <span data-ttu-id="88695-180">b.</span><span class="sxs-lookup"><span data-stu-id="88695-180">b.</span></span> <span data-ttu-id="88695-181">Entrez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="88695-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="88695-182">c.</span><span class="sxs-lookup"><span data-stu-id="88695-182">c.</span></span> <span data-ttu-id="88695-183">Sélectionnez **Set as default**.</span><span class="sxs-lookup"><span data-stu-id="88695-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="88695-184">d.</span><span class="sxs-lookup"><span data-stu-id="88695-184">d.</span></span> <span data-ttu-id="88695-185">Dans **URI de l’émetteur** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="88695-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="88695-186">e.</span><span class="sxs-lookup"><span data-stu-id="88695-186">e.</span></span> <span data-ttu-id="88695-187">Dans **empreinte numérique d’émetteur approuvé** zone de texte, valeur hello coller **l’empreinte numérique** dont vous avez copié à partir de **le certificat de signature SAML** section.</span><span class="sxs-lookup"><span data-stu-id="88695-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="88695-188">Cliquez sur **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="88695-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="88695-189">tooset hello **Emailaddress** attribut Bonjour **revendication** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="88695-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="88695-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="88695-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="88695-191">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="88695-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88695-192">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="88695-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88695-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88695-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88695-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="88695-195">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="88695-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="88695-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="88695-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88695-198">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="88695-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88695-200">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="88695-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88695-202">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="88695-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88695-204">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="88695-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88695-206">a.</span><span class="sxs-lookup"><span data-stu-id="88695-206">a.</span></span> <span data-ttu-id="88695-207">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88695-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88695-208">b.</span><span class="sxs-lookup"><span data-stu-id="88695-208">b.</span></span> <span data-ttu-id="88695-209">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88695-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88695-210">c.</span><span class="sxs-lookup"><span data-stu-id="88695-210">c.</span></span> <span data-ttu-id="88695-211">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="88695-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="88695-212">d.</span><span class="sxs-lookup"><span data-stu-id="88695-212">d.</span></span> <span data-ttu-id="88695-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="88695-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="88695-214">Création d’un utilisateur de test Picturepark</span><span class="sxs-lookup"><span data-stu-id="88695-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="88695-215">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Picturepark, vous devez les configurer dans Picturepark.</span><span class="sxs-lookup"><span data-stu-id="88695-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="88695-216">Dans les cas de hello de Picturepark, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="88695-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="88695-217">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="88695-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="88695-218">Connectez-vous à tooyour **Picturepark** client.</span><span class="sxs-lookup"><span data-stu-id="88695-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="88695-219">Dans la barre d’outils de hello en haut de hello, cliquez sur **outils d’administration**, puis cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="88695-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="88695-220">![Utilisateurs](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="88695-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="88695-221">Bonjour **vue d’ensemble des utilisateurs** , cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="88695-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="88695-222">![Gestion des utilisateurs](./media/active-directory-saas-picturepark-tutorial/ic795068.png "gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="88695-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="88695-223">Sur hello **Create User** boîte de dialogue, effectuer hello suivant les étapes d’un utilisateur Azure Active Directory valide souhaité tooprovision :</span><span class="sxs-lookup"><span data-stu-id="88695-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="88695-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="88695-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="88695-225">a.</span><span class="sxs-lookup"><span data-stu-id="88695-225">a.</span></span> <span data-ttu-id="88695-226">Bonjour **adresse de messagerie** hello de type zone de texte **adresse de messagerie** d’utilisateur de hello  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="88695-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="88695-227">b.</span><span class="sxs-lookup"><span data-stu-id="88695-227">b.</span></span> <span data-ttu-id="88695-228">Bonjour **mot de passe** et **confirmer le mot de passe** zones de texte, hello de type **mot de passe** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88695-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="88695-229">c.</span><span class="sxs-lookup"><span data-stu-id="88695-229">c.</span></span> <span data-ttu-id="88695-230">Bonjour **prénom** hello de type zone de texte **prénom** d’utilisateur de hello **Brian**.</span><span class="sxs-lookup"><span data-stu-id="88695-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="88695-231">d.</span><span class="sxs-lookup"><span data-stu-id="88695-231">d.</span></span> <span data-ttu-id="88695-232">Bonjour **nom** hello de type zone de texte **nom** d’utilisateur de hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="88695-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="88695-233">e.</span><span class="sxs-lookup"><span data-stu-id="88695-233">e.</span></span> <span data-ttu-id="88695-234">Bonjour **société** hello de type zone de texte **nom de la société** d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="88695-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="88695-235">f.</span><span class="sxs-lookup"><span data-stu-id="88695-235">f.</span></span> <span data-ttu-id="88695-236">Bonjour **pays** zone de texte, sélectionnez hello **pays** d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="88695-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="88695-237">g.</span><span class="sxs-lookup"><span data-stu-id="88695-237">g.</span></span> <span data-ttu-id="88695-238">Bonjour **ZIP** hello de type zone de texte **code postal** de ville de hello.</span><span class="sxs-lookup"><span data-stu-id="88695-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="88695-239">h.</span><span class="sxs-lookup"><span data-stu-id="88695-239">h.</span></span> <span data-ttu-id="88695-240">Bonjour **Ville** hello de type zone de texte **nom de Ville** d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="88695-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="88695-241">i.</span><span class="sxs-lookup"><span data-stu-id="88695-241">i.</span></span> <span data-ttu-id="88695-242">Sélectionnez une langue dans **Language**.</span><span class="sxs-lookup"><span data-stu-id="88695-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="88695-243">j.</span><span class="sxs-lookup"><span data-stu-id="88695-243">j.</span></span> <span data-ttu-id="88695-244">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="88695-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="88695-245">Vous pouvez utiliser n’importe quel autre Picturepark utilisateur compte outil de création ou API fournie par Picturepark tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88695-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88695-246">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="88695-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="88695-247">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPicturepark.</span><span class="sxs-lookup"><span data-stu-id="88695-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="88695-249">**tooassign Britta Simon tooPicturepark, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="88695-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="88695-250">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="88695-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="88695-252">Dans la liste des applications hello, sélectionnez **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="88695-252">In hello applications list, select **Picturepark**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="88695-254">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="88695-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="88695-256">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="88695-256">Click **Add** button.</span></span> <span data-ttu-id="88695-257">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="88695-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="88695-259">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="88695-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88695-260">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="88695-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88695-261">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="88695-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88695-262">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="88695-262">Testing single sign-on</span></span>

<span data-ttu-id="88695-263">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="88695-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88695-264">Lorsque vous cliquez sur mosaïque Picturepark hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Picturepark application.</span><span class="sxs-lookup"><span data-stu-id="88695-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="88695-265">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88695-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88695-266">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="88695-266">Additional resources</span></span>

* [<span data-ttu-id="88695-267">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88695-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88695-268">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="88695-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

