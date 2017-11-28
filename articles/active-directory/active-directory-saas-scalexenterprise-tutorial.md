---
title: "Didacticiel : Intégration d’Azure Active Directory avec ScaleX Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="93c75-103">Didacticiel : Intégration d’Azure Active Directory avec ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="93c75-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="93c75-104">Dans ce didacticiel, vous apprendrez comment toointegrate ScaleX Enterprise avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93c75-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93c75-105">Intégration ScaleX Enterprise à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="93c75-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93c75-106">Vous pouvez contrôler dans Azure AD qui a accès tooScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="93c75-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="93c75-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooScaleX entreprise (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93c75-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="93c75-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93c75-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="93c75-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="93c75-110">Qu’est-ce que l’accès aux applications et l’authentification unique avec [Azure Active Directory](active-directory-appssoaccess-whatis.md) ?</span><span class="sxs-lookup"><span data-stu-id="93c75-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93c75-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="93c75-111">Prerequisites</span></span>

<span data-ttu-id="93c75-112">tooconfigure intégration d’Azure AD avec ScaleX Enterprise, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="93c75-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="93c75-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-113">An Azure AD subscription</span></span>
- <span data-ttu-id="93c75-114">Un abonnement ScaleX Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="93c75-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93c75-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="93c75-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93c75-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="93c75-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93c75-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="93c75-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="93c75-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93c75-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93c75-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="93c75-119">Scenario description</span></span>
<span data-ttu-id="93c75-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="93c75-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93c75-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="93c75-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93c75-122">Ajout de ScaleX entreprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="93c75-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="93c75-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="93c75-124">Ajout de ScaleX entreprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="93c75-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="93c75-125">intégration de hello tooconfigure de ScaleX Enterprise dans tooAzure AD, vous devez tooadd ScaleX entreprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="93c75-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93c75-126">**tooadd ScaleX Enterprise à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93c75-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93c75-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="93c75-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93c75-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="93c75-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93c75-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="93c75-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="93c75-132">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="93c75-134">Dans la zone de recherche de hello, tapez **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="93c75-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="93c75-136">Dans le volet de résultats hello, sélectionnez **ScaleX Enterprise**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="93c75-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93c75-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93c75-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ScaleX Enterprise avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="93c75-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93c75-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello ScaleX Enterprise est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93c75-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="93c75-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ScaleX Enterprise doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="93c75-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="93c75-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="93c75-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="93c75-143">tooconfigure et test Azure AD l’authentification unique avec ScaleX Enterprise, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="93c75-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93c75-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="93c75-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93c75-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93c75-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93c75-146">**[Création d’un utilisateur de test ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave un équivalent de Britta Simon dans ScaleX Enterprise qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="93c75-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93c75-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="93c75-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93c75-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="93c75-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93c75-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93c75-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise de ScaleX.</span><span class="sxs-lookup"><span data-stu-id="93c75-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="93c75-151">**tooconfigure Azure AD single sign-on avec ScaleX Enterprise, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93c75-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="93c75-152">Bonjour portail Azure, sur hello **ScaleX Enterprise** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="93c75-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="93c75-154">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="93c75-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="93c75-156">Sur hello **URL et le domaine d’entreprise ScaleX** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="93c75-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="93c75-158">a.</span><span class="sxs-lookup"><span data-stu-id="93c75-158">a.</span></span> <span data-ttu-id="93c75-159">Bonjour **identificateur** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="93c75-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="93c75-160">b.</span><span class="sxs-lookup"><span data-stu-id="93c75-160">b.</span></span> <span data-ttu-id="93c75-161">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="93c75-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="93c75-162">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="93c75-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="93c75-164">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="93c75-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="93c75-165">Ils ne sont pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-165">These are not hello real values.</span></span> <span data-ttu-id="93c75-166">Mettre à jour ces valeurs hello identificateur réelle, les URL de réponse ou les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="93c75-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="93c75-167">Contact [équipe de support Client d’entreprise ScaleX](http://info.rescale.com/contact_sales) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="93c75-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="93c75-168">Votre application ScaleX attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous toomodify attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="93c75-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="93c75-169">Cliquez sur **afficher et modifier tous les autres attributs utilisateur** hello de tooopen de case à cocher personnalisé les paramètres d’attributs.</span><span class="sxs-lookup"><span data-stu-id="93c75-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="93c75-171">a.</span><span class="sxs-lookup"><span data-stu-id="93c75-171">a.</span></span> <span data-ttu-id="93c75-172">Cliquez avec le bouton droit sur les attributs hello **nom** et cliquez sur Supprimer.</span><span class="sxs-lookup"><span data-stu-id="93c75-172">Right click hello attribute **name** and click delete.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="93c75-174">b.</span><span class="sxs-lookup"><span data-stu-id="93c75-174">b.</span></span> <span data-ttu-id="93c75-175">Cliquez sur **emailaddress** fenêtre de modifier l’attribut attribut tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="93c75-176">Modifier sa valeur à partir de **user.mail** trop**user.userprincipalname** et cliquez sur Ok.</span><span class="sxs-lookup"><span data-stu-id="93c75-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="93c75-178">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="93c75-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="93c75-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="93c75-180">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="93c75-182">Sur hello **ScaleX Enterprise Configuration** , cliquez sur **configurer un ScaleX Enterprise** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="93c75-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="93c75-183">Hello de copie **ID d’entité SAML** et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="93c75-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="93c75-185">tooconfigure l’authentification unique sur **ScaleX Enterprise** côté, connexion toohello ScaleX Enterprise site Web d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="93c75-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="93c75-186">Cliquez sur menu hello Bonjour supérieur droit et sélectionnez **Contoso Administration**.</span><span class="sxs-lookup"><span data-stu-id="93c75-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93c75-187">Contoso est simplement un exemple.</span><span class="sxs-lookup"><span data-stu-id="93c75-187">Contoso is just an example.</span></span> <span data-ttu-id="93c75-188">Ce doit être le nom réel de votre société.</span><span class="sxs-lookup"><span data-stu-id="93c75-188">This should be your actual Company Name.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="93c75-190">Sélectionnez **intégrations** de menu du haut hello et sélectionnez **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="93c75-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="93c75-192">Remplissez le formulaire de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="93c75-192">Complete hello form as follows:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="93c75-194">a.</span><span class="sxs-lookup"><span data-stu-id="93c75-194">a.</span></span> <span data-ttu-id="93c75-195">Sélectionnez **Créer n’importe quel utilisateur pouvant s’authentifier avec l’authentification unique.**</span><span class="sxs-lookup"><span data-stu-id="93c75-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="93c75-196">b.</span><span class="sxs-lookup"><span data-stu-id="93c75-196">b.</span></span> <span data-ttu-id="93c75-197">**Fournisseur de service saml**: coller hello valeur ***urn : oasis : noms : tc : SAML:2.0:nameid-format : persistant***</span><span class="sxs-lookup"><span data-stu-id="93c75-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="93c75-198">c.</span><span class="sxs-lookup"><span data-stu-id="93c75-198">c.</span></span> <span data-ttu-id="93c75-199">**Nom du champ de courrier électronique de fournisseur d’identité dans la réponse d’ACS**: collez la valeur de hello`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="93c75-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="93c75-200">d.</span><span class="sxs-lookup"><span data-stu-id="93c75-200">d.</span></span> <span data-ttu-id="93c75-201">**ID d’entité de EntityDescriptor :** hello de coller **ID d’entité SAML** valeur copiée à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="93c75-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="93c75-202">e.</span><span class="sxs-lookup"><span data-stu-id="93c75-202">e.</span></span> <span data-ttu-id="93c75-203">**URL SingleSignOnService fournisseur d’identité :** hello de coller **SAML Sign-On URL du Service unique** de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="93c75-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="93c75-204">f.</span><span class="sxs-lookup"><span data-stu-id="93c75-204">f.</span></span> <span data-ttu-id="93c75-205">**Certificat d’identité du fournisseur public X509 :** certificat de hello ouvrir X509 téléchargé à partir de la hello Azure dans le bloc-notes et collez contenu hello dans cette zone.</span><span class="sxs-lookup"><span data-stu-id="93c75-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="93c75-206">Assurez-vous que pas de saut de ligne dans hello du milieu du contenu du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="93c75-207">g.</span><span class="sxs-lookup"><span data-stu-id="93c75-207">g.</span></span> <span data-ttu-id="93c75-208">Vérifiez hello suivant des cases à cocher : **activé, NameID de chiffrer et AuthnRequests de connexion.**</span><span class="sxs-lookup"><span data-stu-id="93c75-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="93c75-209">h.</span><span class="sxs-lookup"><span data-stu-id="93c75-209">h.</span></span> <span data-ttu-id="93c75-210">Cliquez sur **paramètres d’authentification unique de mise à jour** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="93c75-211">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="93c75-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93c75-212">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93c75-213">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93c75-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93c75-214">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="93c75-215">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="93c75-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="93c75-217">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93c75-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93c75-218">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="93c75-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93c75-220">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="93c75-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93c75-222">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="93c75-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93c75-224">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="93c75-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93c75-226">a.</span><span class="sxs-lookup"><span data-stu-id="93c75-226">a.</span></span> <span data-ttu-id="93c75-227">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93c75-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93c75-228">b.</span><span class="sxs-lookup"><span data-stu-id="93c75-228">b.</span></span> <span data-ttu-id="93c75-229">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="93c75-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93c75-230">c.</span><span class="sxs-lookup"><span data-stu-id="93c75-230">c.</span></span> <span data-ttu-id="93c75-231">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="93c75-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93c75-232">d.</span><span class="sxs-lookup"><span data-stu-id="93c75-232">d.</span></span> <span data-ttu-id="93c75-233">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="93c75-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="93c75-234">Création d’un utilisateur de test ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="93c75-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="93c75-235">tooenable Azure AD les utilisateurs toolog dans tooScaleX Enterprise, vous devez les configurer dans tooScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="93c75-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="93c75-236">Dans les cas de hello de ScaleX Enterprise, cette configuration est une tâche automatique et aucune étape manuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="93c75-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="93c75-237">Tout utilisateur qui peut s’authentifier correctement avec les informations d’identification SSO est automatiquement configuré sur hello ScaleX côté.</span><span class="sxs-lookup"><span data-stu-id="93c75-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93c75-238">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="93c75-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93c75-239">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’utilisateur accès tooScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="93c75-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="93c75-241">**tooassign Britta Simon tooScaleX Enterprise, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93c75-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="93c75-242">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="93c75-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="93c75-244">Dans la liste des applications hello, sélectionnez **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="93c75-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="93c75-246">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="93c75-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="93c75-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="93c75-248">Click **Add** button.</span></span> <span data-ttu-id="93c75-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="93c75-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="93c75-251">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="93c75-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93c75-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="93c75-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93c75-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="93c75-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="93c75-254">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="93c75-254">Testing single sign-on</span></span>

<span data-ttu-id="93c75-255">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="93c75-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93c75-256">Cliquez sur hello ScaleX Enterprise vignette Bonjour volet d’accès, vous obtenez automatiquement signé sur tooyour application ScaleX entreprise.</span><span class="sxs-lookup"><span data-stu-id="93c75-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="93c75-257">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="93c75-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="93c75-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="93c75-258">Additional resources</span></span>

* [<span data-ttu-id="93c75-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93c75-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93c75-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="93c75-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

