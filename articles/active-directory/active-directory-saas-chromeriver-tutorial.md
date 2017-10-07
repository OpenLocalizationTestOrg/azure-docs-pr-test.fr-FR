---
title: "Didacticiel : Intégration d’Azure Active Directory à Chromeriver | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Chromeriver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 7cf0e36fb6407bf3915e26717a2a997ac13110e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="6ad66-103">Didacticiel : Intégration d’Azure Active Directory à Chromeriver</span><span class="sxs-lookup"><span data-stu-id="6ad66-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="6ad66-104">Dans ce didacticiel, vous apprendrez comment toointegrate Chromeriver avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ad66-104">In this tutorial, you learn how toointegrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ad66-105">Intégration de Chromeriver à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6ad66-105">Integrating Chromeriver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6ad66-106">Vous pouvez contrôler dans Azure AD qui a accès tooChromeriver</span><span class="sxs-lookup"><span data-stu-id="6ad66-106">You can control in Azure AD who has access tooChromeriver</span></span>
- <span data-ttu-id="6ad66-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooChromeriver (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-107">You can enable your users tooautomatically get signed-on tooChromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ad66-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="6ad66-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6ad66-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ad66-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ad66-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6ad66-110">Prerequisites</span></span>

<span data-ttu-id="6ad66-111">tooconfigure intégration d’Azure AD à Chromeriver, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6ad66-111">tooconfigure Azure AD integration with Chromeriver, you need hello following items:</span></span>

- <span data-ttu-id="6ad66-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ad66-113">Un abonnement Chromeriver pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6ad66-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ad66-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6ad66-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ad66-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="6ad66-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ad66-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6ad66-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ad66-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ad66-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ad66-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6ad66-118">Scenario description</span></span>
<span data-ttu-id="6ad66-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6ad66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ad66-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="6ad66-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ad66-121">Ajout de Chromeriver à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6ad66-121">Adding Chromeriver from hello gallery</span></span>
2. <span data-ttu-id="6ad66-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-hello-gallery"></a><span data-ttu-id="6ad66-123">Ajout de Chromeriver à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6ad66-123">Adding Chromeriver from hello gallery</span></span>
<span data-ttu-id="6ad66-124">intégration de hello tooconfigure de Chromeriver dans Azure AD, vous devez tooadd Chromeriver à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6ad66-124">tooconfigure hello integration of Chromeriver into Azure AD, you need tooadd Chromeriver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6ad66-125">**tooadd Chromeriver à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6ad66-125">**tooadd Chromeriver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ad66-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="6ad66-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ad66-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6ad66-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6ad66-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6ad66-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6ad66-133">Dans la zone de recherche de hello, tapez **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-133">In hello search box, type **Chromeriver**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_search.png)

5. <span data-ttu-id="6ad66-135">Dans le volet de résultats hello, sélectionnez **Chromeriver**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6ad66-135">In hello results panel, select **Chromeriver**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ad66-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ad66-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Chromeriver, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6ad66-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6ad66-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Chromeriver est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ad66-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Chromeriver is tooa user in Azure AD.</span></span> <span data-ttu-id="6ad66-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Chromeriver doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="6ad66-140">In other words, a link relationship between an Azure AD user and hello related user in Chromeriver needs toobe established.</span></span>

<span data-ttu-id="6ad66-141">Dans Chromeriver, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="6ad66-141">In Chromeriver, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6ad66-142">tooconfigure et test Azure AD l’authentification unique à Chromeriver, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="6ad66-142">tooconfigure and test Azure AD single sign-on with Chromeriver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6ad66-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6ad66-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6ad66-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ad66-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ad66-145">**[Création d’un utilisateur de test de Chromeriver](#creating-a-chromeriver-test-user)**  -toohave un équivalent de Britta Simon dans Chromeriver est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6ad66-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - toohave a counterpart of Britta Simon in Chromeriver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ad66-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6ad66-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ad66-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="6ad66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ad66-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ad66-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="6ad66-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="6ad66-150">**tooconfigure Azure AD single sign-on avec Chromeriver, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6ad66-150">**tooconfigure Azure AD single sign-on with Chromeriver, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ad66-151">Bonjour portail Azure, sur hello **Chromeriver** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-151">In hello Azure portal, on hello **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6ad66-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6ad66-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

3. <span data-ttu-id="6ad66-155">Sur hello **Chromeriver domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6ad66-155">On hello **Chromeriver Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="6ad66-157">a.</span><span class="sxs-lookup"><span data-stu-id="6ad66-157">a.</span></span> <span data-ttu-id="6ad66-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="6ad66-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="6ad66-159">b.</span><span class="sxs-lookup"><span data-stu-id="6ad66-159">b.</span></span> <span data-ttu-id="6ad66-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="6ad66-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ad66-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6ad66-161">These values are not real.</span></span> <span data-ttu-id="6ad66-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="6ad66-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6ad66-163">Contact [équipe de support technique Chromeriver](https://www.chromeriver.com/services/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="6ad66-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) tooget these values.</span></span>
 


4. <span data-ttu-id="6ad66-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6ad66-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

5. <span data-ttu-id="6ad66-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6ad66-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-chromeriver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ad66-168">tooconfigure l’authentification unique sur **Chromeriver** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="6ad66-168">tooconfigure single sign-on on **Chromeriver** side, you need toosend hello downloaded **Metadata XML** too[Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="6ad66-169">Vous recevrez une notification dès que l’authentification unique aura été activée pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6ad66-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="6ad66-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="6ad66-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6ad66-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="6ad66-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6ad66-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ad66-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ad66-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ad66-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="6ad66-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6ad66-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6ad66-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ad66-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="6ad66-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ad66-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ad66-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="6ad66-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ad66-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6ad66-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ad66-185">a.</span><span class="sxs-lookup"><span data-stu-id="6ad66-185">a.</span></span> <span data-ttu-id="6ad66-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ad66-187">b.</span><span class="sxs-lookup"><span data-stu-id="6ad66-187">b.</span></span> <span data-ttu-id="6ad66-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6ad66-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ad66-189">c.</span><span class="sxs-lookup"><span data-stu-id="6ad66-189">c.</span></span> <span data-ttu-id="6ad66-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6ad66-191">d.</span><span class="sxs-lookup"><span data-stu-id="6ad66-191">d.</span></span> <span data-ttu-id="6ad66-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="6ad66-193">Création d’un utilisateur de test Chromeriver</span><span class="sxs-lookup"><span data-stu-id="6ad66-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="6ad66-194">tooenable Azure AD les utilisateurs toolog dans tooChromeriver, vous devez les configurer dans Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="6ad66-194">tooenable Azure AD users toolog in tooChromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="6ad66-195">Dans les cas de hello de Chromeriver, les comptes d’utilisateur de hello doivent toobe créé par votre [équipe de support technique Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="6ad66-195">In hello case of Chromeriver, hello user accounts need toobe created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="6ad66-196">Vous pouvez utiliser n’importe quel autre Chromeriver utilisateur compte outil de création ou API fournie par Chromeriver tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6ad66-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6ad66-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad66-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6ad66-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooChromeriver.</span><span class="sxs-lookup"><span data-stu-id="6ad66-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooChromeriver.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6ad66-200">**tooassign Britta Simon tooChromeriver, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6ad66-200">**tooassign Britta Simon tooChromeriver, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ad66-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6ad66-203">Dans la liste des applications hello, sélectionnez **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-203">In hello applications list, select **Chromeriver**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_app.png) 

3. <span data-ttu-id="6ad66-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6ad66-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-207">Click **Add** button.</span></span> <span data-ttu-id="6ad66-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6ad66-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="6ad66-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6ad66-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ad66-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6ad66-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ad66-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6ad66-213">Testing single sign-on</span></span>

<span data-ttu-id="6ad66-214">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="6ad66-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6ad66-215">Lorsque vous cliquez sur mosaïque Chromeriver hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Chromeriver application.</span><span class="sxs-lookup"><span data-stu-id="6ad66-215">When you click hello Chromeriver tile in hello Access Panel, you should get automatically signed-on tooyour Chromeriver application.</span></span> <span data-ttu-id="6ad66-216">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ad66-216">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ad66-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6ad66-217">Additional resources</span></span>

* [<span data-ttu-id="6ad66-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ad66-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ad66-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6ad66-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_203.png

