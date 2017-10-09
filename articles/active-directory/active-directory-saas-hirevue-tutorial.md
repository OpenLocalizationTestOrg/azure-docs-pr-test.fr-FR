---
title: "Didacticiel : Intégration d’Azure Active Directory à HireVue | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="1005e-103">Didacticiel : Intégration d’Azure AD à HireVue</span><span class="sxs-lookup"><span data-stu-id="1005e-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="1005e-104">Dans ce didacticiel, vous apprendrez comment toointegrate HireVue avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1005e-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1005e-105">Intégration HireVue à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1005e-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1005e-106">Vous pouvez contrôler dans Azure AD qui a accès tooHireVue</span><span class="sxs-lookup"><span data-stu-id="1005e-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="1005e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHireVue (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1005e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1005e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1005e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1005e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1005e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1005e-110">Prerequisites</span></span>

<span data-ttu-id="1005e-111">tooconfigure intégration d’Azure AD avec HireVue, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1005e-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="1005e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1005e-113">Un abonnement HireVue pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1005e-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1005e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1005e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1005e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="1005e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1005e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1005e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1005e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1005e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1005e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1005e-118">Scenario description</span></span>
<span data-ttu-id="1005e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1005e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1005e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1005e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1005e-121">Ajout de HireVue à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1005e-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="1005e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="1005e-123">Ajout de HireVue à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1005e-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="1005e-124">intégration de hello tooconfigure de HireVue dans Azure AD, vous devez tooadd HireVue à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1005e-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1005e-125">**tooadd HireVue à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1005e-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1005e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1005e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1005e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1005e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1005e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1005e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1005e-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1005e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1005e-133">Dans la zone de recherche de hello, tapez **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="1005e-133">In hello search box, type **HireVue**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="1005e-135">Dans le volet de résultats hello, sélectionnez **HireVue**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1005e-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1005e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1005e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HireVue avec un utilisateur de test appelé "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1005e-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1005e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans HireVue est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1005e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="1005e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans HireVue doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="1005e-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="1005e-141">Dans HireVue, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="1005e-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1005e-142">tooconfigure et test Azure AD l’authentification unique avec HireVue, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="1005e-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1005e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1005e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1005e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1005e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1005e-145">**[Création d’un utilisateur de test HireVue](#creating-a-hirevue-test-user)**  -toohave un équivalent de Britta Simon dans HireVue est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1005e-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1005e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1005e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1005e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="1005e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1005e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1005e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application HireVue.</span><span class="sxs-lookup"><span data-stu-id="1005e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="1005e-150">**tooconfigure Azure AD single sign-on avec HireVue, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1005e-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="1005e-151">Bonjour portail Azure, sur hello **HireVue** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1005e-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1005e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1005e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="1005e-155">Sur hello **HireVue domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1005e-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="1005e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1005e-157">a.</span></span> <span data-ttu-id="1005e-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="1005e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="1005e-159">Environnement</span><span class="sxs-lookup"><span data-stu-id="1005e-159">Environment</span></span> | <span data-ttu-id="1005e-160">URL</span><span class="sxs-lookup"><span data-stu-id="1005e-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="1005e-161">Production</span><span class="sxs-lookup"><span data-stu-id="1005e-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="1005e-162">Staging</span><span class="sxs-lookup"><span data-stu-id="1005e-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="1005e-163">b.</span><span class="sxs-lookup"><span data-stu-id="1005e-163">b.</span></span> <span data-ttu-id="1005e-164">Bonjour **identificateur** zone de texte, tapez une URL en tant que :</span><span class="sxs-lookup"><span data-stu-id="1005e-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="1005e-165">Environnement</span><span class="sxs-lookup"><span data-stu-id="1005e-165">Environment</span></span> | <span data-ttu-id="1005e-166">URN</span><span class="sxs-lookup"><span data-stu-id="1005e-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="1005e-167">Production</span><span class="sxs-lookup"><span data-stu-id="1005e-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="1005e-168">Staging</span><span class="sxs-lookup"><span data-stu-id="1005e-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="1005e-169">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1005e-169">These values are not real.</span></span> <span data-ttu-id="1005e-170">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="1005e-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1005e-171">Contact [équipe de support Client de HireVue](mailto:samlsupport@hirevue.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="1005e-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="1005e-172">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1005e-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="1005e-174">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1005e-174">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1005e-176">Sur hello **HireVue Configuration** , cliquez sur **HireVue de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1005e-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1005e-177">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1005e-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="1005e-179">tooconfigure l’authentification unique sur **HireVue** côté, vous devez hello toosend téléchargé **Certificate(Base64)** et **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="1005e-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="1005e-180">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="1005e-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1005e-181">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="1005e-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1005e-182">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="1005e-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1005e-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1005e-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1005e-184">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="1005e-185">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="1005e-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1005e-187">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1005e-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1005e-188">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1005e-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1005e-190">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1005e-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1005e-192">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1005e-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1005e-194">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1005e-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1005e-196">a.</span><span class="sxs-lookup"><span data-stu-id="1005e-196">a.</span></span> <span data-ttu-id="1005e-197">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1005e-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1005e-198">b.</span><span class="sxs-lookup"><span data-stu-id="1005e-198">b.</span></span> <span data-ttu-id="1005e-199">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1005e-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1005e-200">c.</span><span class="sxs-lookup"><span data-stu-id="1005e-200">c.</span></span> <span data-ttu-id="1005e-201">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1005e-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1005e-202">d.</span><span class="sxs-lookup"><span data-stu-id="1005e-202">d.</span></span> <span data-ttu-id="1005e-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1005e-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="1005e-204">Création d’un utilisateur de test HireVue</span><span class="sxs-lookup"><span data-stu-id="1005e-204">Creating a HireVue test user</span></span>

<span data-ttu-id="1005e-205">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans HireVue.</span><span class="sxs-lookup"><span data-stu-id="1005e-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="1005e-206">Collaborez avec [équipe de support HireVue](mailto:samlsupport@hirevue.com) tooadd les utilisateurs de hello dans la plateforme de HireVue hello.</span><span class="sxs-lookup"><span data-stu-id="1005e-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1005e-207">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1005e-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1005e-208">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHireVue.</span><span class="sxs-lookup"><span data-stu-id="1005e-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1005e-210">**tooassign Britta Simon tooHireVue, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1005e-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="1005e-211">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1005e-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1005e-213">Dans la liste des applications hello, sélectionnez **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="1005e-213">In hello applications list, select **HireVue**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="1005e-215">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1005e-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1005e-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1005e-217">Click **Add** button.</span></span> <span data-ttu-id="1005e-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1005e-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1005e-220">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="1005e-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1005e-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1005e-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1005e-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1005e-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1005e-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1005e-223">Testing single sign-on</span></span>

<span data-ttu-id="1005e-224">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="1005e-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1005e-225">Lorsque vous cliquez sur mosaïque HireVue hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour HireVue application.</span><span class="sxs-lookup"><span data-stu-id="1005e-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1005e-226">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1005e-226">Additional resources</span></span>

* [<span data-ttu-id="1005e-227">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1005e-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1005e-228">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1005e-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

