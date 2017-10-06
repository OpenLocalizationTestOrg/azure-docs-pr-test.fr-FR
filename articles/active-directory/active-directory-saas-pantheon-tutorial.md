---
title: "Didacticiel : Intégration d’Azure Active Directory à Pantheon | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="f90b5-103">Didacticiel : Intégration d’Azure Active Directory à Pantheon</span><span class="sxs-lookup"><span data-stu-id="f90b5-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="f90b5-104">Dans ce didacticiel, vous apprendrez comment toointegrate Pantheon avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f90b5-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f90b5-105">Intégration Pantheon à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f90b5-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f90b5-106">Vous pouvez contrôler dans Azure AD qui a accès tooPantheon</span><span class="sxs-lookup"><span data-stu-id="f90b5-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="f90b5-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPantheon (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f90b5-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f90b5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f90b5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f90b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f90b5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f90b5-110">Prerequisites</span></span>

<span data-ttu-id="f90b5-111">tooconfigure intégration d’Azure AD avec Pantheon, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f90b5-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="f90b5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f90b5-113">Un abonnement Pantheon pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f90b5-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f90b5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f90b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f90b5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f90b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f90b5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f90b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f90b5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f90b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f90b5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f90b5-118">Scenario description</span></span>
<span data-ttu-id="f90b5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f90b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f90b5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f90b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f90b5-121">Ajout de Pantheon à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f90b5-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="f90b5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="f90b5-123">Ajout de Pantheon à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f90b5-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="f90b5-124">intégration de hello tooconfigure de Pantheon dans Azure AD, vous devez tooadd Pantheon à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f90b5-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f90b5-125">**tooadd Pantheon à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f90b5-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f90b5-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f90b5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f90b5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f90b5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f90b5-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f90b5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f90b5-133">Dans la zone de recherche de hello, tapez **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-133">In hello search box, type **Pantheon**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="f90b5-135">Dans le volet de résultats hello, sélectionnez **Pantheon**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f90b5-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f90b5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f90b5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pantheon avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f90b5-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f90b5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Pantheon est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f90b5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="f90b5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Pantheon doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f90b5-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="f90b5-141">Dans Pantheon, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f90b5-142">tooconfigure et test Azure AD l’authentification unique avec Pantheon, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f90b5-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f90b5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f90b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f90b5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f90b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f90b5-145">**[Création d’un utilisateur de test Pantheon](#creating-a-pantheon-test-user)**  -toohave un équivalent de Britta Simon dans Pantheon est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f90b5-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f90b5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f90b5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f90b5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f90b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f90b5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f90b5-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Pantheon.</span><span class="sxs-lookup"><span data-stu-id="f90b5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="f90b5-150">**tooconfigure Azure AD single sign-on avec Pantheon, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f90b5-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="f90b5-151">Bonjour portail Azure, sur hello **Pantheon** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f90b5-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f90b5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="f90b5-155">Sur hello **Pantheon domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f90b5-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="f90b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="f90b5-157">a.</span></span> <span data-ttu-id="f90b5-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="f90b5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="f90b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="f90b5-159">b.</span></span> <span data-ttu-id="f90b5-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="f90b5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f90b5-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f90b5-161">These values are not real.</span></span> <span data-ttu-id="f90b5-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="f90b5-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f90b5-163">Contact [équipe de support Pantheon](https://pantheon.io/docs/getting-support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f90b5-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="f90b5-164">Application de pantheon attend l’assertion SAML de hello dans un format spécifique, ce qui nécessite vous tooset hello Identifiant_utilisateur valeur d’attribut avec l’adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="f90b5-165">Par défaut, Azure AD utilise hello UserPrincipalName pour Identifiant_utilisateur attribut.</span><span class="sxs-lookup"><span data-stu-id="f90b5-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="f90b5-166">Mais pour une intégration réussie, vous devez tooadjust toomatch de cette valeur avec l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f90b5-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="f90b5-167">intégration de Hello fonctionne uniquement après avoir effectué le mappage correct de hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="f90b5-169">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f90b5-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="f90b5-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f90b5-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f90b5-173">Sur hello **Pantheon Configuration** , cliquez sur **Pantheon de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f90b5-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f90b5-174">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f90b5-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="f90b5-176">tooconfigure l’authentification unique sur **Pantheon** côté, vous devez hello toosend téléchargé **certificat** et **SAML Sign-On URL du Service unique** trop[Pantheon l’équipe de support](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="f90b5-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="f90b5-177">Vous devez également des informations des domaines de messagerie tooprovide hello et l’heure de la Date lorsque vous souhaitez tooenable cette connexion.</span><span class="sxs-lookup"><span data-stu-id="f90b5-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="f90b5-178">Vous trouverez plus de détails à ce propos [ici](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="f90b5-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="f90b5-179">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f90b5-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f90b5-180">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f90b5-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f90b5-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f90b5-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="f90b5-183">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f90b5-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f90b5-185">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f90b5-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f90b5-186">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f90b5-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f90b5-188">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f90b5-190">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f90b5-192">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f90b5-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f90b5-194">a.</span><span class="sxs-lookup"><span data-stu-id="f90b5-194">a.</span></span> <span data-ttu-id="f90b5-195">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f90b5-196">b.</span><span class="sxs-lookup"><span data-stu-id="f90b5-196">b.</span></span> <span data-ttu-id="f90b5-197">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f90b5-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f90b5-198">c.</span><span class="sxs-lookup"><span data-stu-id="f90b5-198">c.</span></span> <span data-ttu-id="f90b5-199">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f90b5-200">d.</span><span class="sxs-lookup"><span data-stu-id="f90b5-200">d.</span></span> <span data-ttu-id="f90b5-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="f90b5-202">Création d’un utilisateur de test Pantheon</span><span class="sxs-lookup"><span data-stu-id="f90b5-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="f90b5-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Pantheon.</span><span class="sxs-lookup"><span data-stu-id="f90b5-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="f90b5-204">Veuillez suivre hello ci-dessous utilisateur hello étapes tooadd Pantheon.</span><span class="sxs-lookup"><span data-stu-id="f90b5-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="f90b5-205">Pour l’authentification unique toowork utilisateur doit d’abord créé dans Pantheon de toobe.</span><span class="sxs-lookup"><span data-stu-id="f90b5-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="f90b5-206">TooPantheon de connexion avec les informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f90b5-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="f90b5-207">Accédez trop**organisation** page tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f90b5-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="f90b5-208">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-208">Click **People**.</span></span>

4. <span data-ttu-id="f90b5-209">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-209">Click **Add user**.</span></span>

5. <span data-ttu-id="f90b5-210">Entrez l’adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="f90b5-211">Choisissez un rôle d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="f90b5-212">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f90b5-213">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f90b5-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f90b5-214">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPantheon.</span><span class="sxs-lookup"><span data-stu-id="f90b5-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f90b5-216">**tooassign Britta Simon tooPantheon, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f90b5-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="f90b5-217">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f90b5-219">Dans la liste des applications hello, sélectionnez **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-219">In hello applications list, select **Pantheon**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="f90b5-221">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f90b5-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-223">Click **Add** button.</span></span> <span data-ttu-id="f90b5-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f90b5-226">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f90b5-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f90b5-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f90b5-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f90b5-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f90b5-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f90b5-229">Testing single sign-on</span></span>

<span data-ttu-id="f90b5-230">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f90b5-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f90b5-231">Lorsque vous cliquez sur mosaïque Pantheon hello hello volet d’accès, vous devez obtenir l’application de Pantheon automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="f90b5-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="f90b5-232">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f90b5-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f90b5-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f90b5-233">Additional resources</span></span>

* [<span data-ttu-id="f90b5-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f90b5-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f90b5-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f90b5-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

