---
title: "Didacticiel : intégration d’Azure Active Directory à Tango Analytics | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Tango Analytique."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 2076397e746235692f07241650d5556afb3c3d28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="cb9f3-103">Didacticiel : intégration d’Azure Active Directory à Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="cb9f3-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="cb9f3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Analytique Tango avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb9f3-104">In this tutorial, you learn how toointegrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb9f3-105">Intégration Tango Analytique à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-105">Integrating Tango Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb9f3-106">Vous pouvez contrôler dans Azure AD qui a accès tooTango Analytique</span><span class="sxs-lookup"><span data-stu-id="cb9f3-106">You can control in Azure AD who has access tooTango Analytics</span></span>
- <span data-ttu-id="cb9f3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTango Analytique (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-107">You can enable your users tooautomatically get signed-on tooTango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb9f3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cb9f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb9f3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb9f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb9f3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cb9f3-110">Prerequisites</span></span>

<span data-ttu-id="cb9f3-111">tooconfigure intégration d’Azure AD avec Tango Analytique, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-111">tooconfigure Azure AD integration with Tango Analytics, you need hello following items:</span></span>

- <span data-ttu-id="cb9f3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb9f3-113">Un abonnement Tango Analytics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="cb9f3-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb9f3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb9f3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb9f3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb9f3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb9f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb9f3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cb9f3-118">Scenario description</span></span>
<span data-ttu-id="cb9f3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb9f3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb9f3-121">Ajout de Tango Analytique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cb9f3-121">Adding Tango Analytics from hello gallery</span></span>
2. <span data-ttu-id="cb9f3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-hello-gallery"></a><span data-ttu-id="cb9f3-123">Ajout de Tango Analytique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cb9f3-123">Adding Tango Analytics from hello gallery</span></span>
<span data-ttu-id="cb9f3-124">tooconfigure hello intégration de Tango Analytique dans Azure AD, vous devez tooadd Tango Analytique à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-124">tooconfigure hello integration of Tango Analytics into Azure AD, you need tooadd Tango Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb9f3-125">**tooadd Analytique Tango à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb9f3-125">**tooadd Tango Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb9f3-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb9f3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb9f3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cb9f3-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cb9f3-133">Dans la zone de recherche de hello, tapez **Tango Analytique**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-133">In hello search box, type **Tango Analytics**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="cb9f3-135">Dans le volet de résultats hello, sélectionnez **Tango Analytique**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-135">In hello results panel, select **Tango Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb9f3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb9f3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tango Analytics avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cb9f3-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb9f3-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Tango Analytique est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tango Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="cb9f3-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Tango Analytique doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-140">In other words, a link relationship between an Azure AD user and hello related user in Tango Analytics needs toobe established.</span></span>

<span data-ttu-id="cb9f3-141">Dans Tango Analytique, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-141">In Tango Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cb9f3-142">tooconfigure et test Azure AD l’authentification unique avec Tango Analytique, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-142">tooconfigure and test Azure AD single sign-on with Tango Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb9f3-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb9f3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb9f3-145">**[Création d’un utilisateur de test Tango Analytique](#creating-a-tango-analytics-test-user)**  -toohave un équivalent de Britta Simon dans Tango Analytique qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - toohave a counterpart of Britta Simon in Tango Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb9f3-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb9f3-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb9f3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb9f3-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Tango Analytique.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="cb9f3-150">**tooconfigure Azure AD single sign-on avec Tango Analytique, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb9f3-150">**tooconfigure Azure AD single sign-on with Tango Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb9f3-151">Bonjour portail Azure, sur hello **Tango Analytique** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-151">In hello Azure portal, on hello **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cb9f3-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="cb9f3-155">Sur hello **Tango Analytique domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-155">On hello **Tango Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="cb9f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-157">a.</span></span> <span data-ttu-id="cb9f3-158">Bonjour **identificateur** zone de texte, valeur de type hello`TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="cb9f3-158">In hello **Identifier** textbox, type hello value `TACORE_SSO`</span></span>

    <span data-ttu-id="cb9f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-159">b.</span></span> <span data-ttu-id="cb9f3-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="cb9f3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb9f3-161">valeur de l’URL de réponse de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-161">hello Reply URL value is not real.</span></span> <span data-ttu-id="cb9f3-162">Cette mise à jour avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-162">Update this with hello actual Reply URL.</span></span> <span data-ttu-id="cb9f3-163">Contact [équipe de support technique Tango Analytique](mailto:support@tangoanalytics.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) tooget this value.</span></span>

4. <span data-ttu-id="cb9f3-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="cb9f3-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cb9f3-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb9f3-168">tooconfigure l’authentification unique sur **Tango Analytique** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique Tango Analytique](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="cb9f3-168">tooconfigure single sign-on on **Tango Analytics** side, you need toosend hello downloaded **Metadata XML** too[Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="cb9f3-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cb9f3-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="cb9f3-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb9f3-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb9f3-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb9f3-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb9f3-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb9f3-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cb9f3-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb9f3-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb9f3-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb9f3-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb9f3-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb9f3-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb9f3-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb9f3-185">a.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-185">a.</span></span> <span data-ttu-id="cb9f3-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb9f3-187">b.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-187">b.</span></span> <span data-ttu-id="cb9f3-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb9f3-189">c.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-189">c.</span></span> <span data-ttu-id="cb9f3-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb9f3-191">d.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-191">d.</span></span> <span data-ttu-id="cb9f3-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="cb9f3-193">Création d’un utilisateur de test Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="cb9f3-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="cb9f3-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="cb9f3-195">Travailler avec [équipe de support technique Tango Analytique](mailto:support@tangoanalytics.com) pour ajouter des utilisateurs de hello de plateforme de Tango Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add hello users in hello Tango Analytics platform.</span></span> <span data-ttu-id="cb9f3-196">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb9f3-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb9f3-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb9f3-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTango Analytique.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTango Analytics.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cb9f3-200">**tooassign Britta Simon tooTango Analytique, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb9f3-200">**tooassign Britta Simon tooTango Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb9f3-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cb9f3-203">Dans la liste des applications hello, sélectionnez **Tango Analytique**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-203">In hello applications list, select **Tango Analytics**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="cb9f3-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cb9f3-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-207">Click **Add** button.</span></span> <span data-ttu-id="cb9f3-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cb9f3-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb9f3-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb9f3-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb9f3-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cb9f3-213">Testing single sign-on</span></span>

<span data-ttu-id="cb9f3-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb9f3-215">Lorsque vous cliquez sur hello Tango Analytique vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de Tango Analytique.</span><span class="sxs-lookup"><span data-stu-id="cb9f3-215">When you click hello Tango Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Tango Analytics application.</span></span>
<span data-ttu-id="cb9f3-216">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb9f3-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb9f3-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cb9f3-217">Additional resources</span></span>

* [<span data-ttu-id="cb9f3-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb9f3-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb9f3-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cb9f3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png
