---
title: "Didacticiel : Intégration d’Azure Active Directory à Salesforce | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la force de vente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="9626e-103">Didacticiel : Intégration d’Azure Active Directory à Salesforce</span><span class="sxs-lookup"><span data-stu-id="9626e-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="9626e-104">Dans ce didacticiel, vous apprendrez comment toointegrate Salesforce avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9626e-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9626e-105">Intégration de Salesforce à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9626e-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9626e-106">Vous pouvez contrôler dans Azure AD qui a accès tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="9626e-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="9626e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSalesforce (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9626e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9626e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9626e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9626e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9626e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9626e-110">Prerequisites</span></span>

<span data-ttu-id="9626e-111">tooconfigure intégration d’Azure AD à Salesforce, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9626e-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="9626e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9626e-113">Un abonnement Salesforce pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9626e-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9626e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9626e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9626e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9626e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9626e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9626e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9626e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9626e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9626e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9626e-118">Scenario description</span></span>
<span data-ttu-id="9626e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9626e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9626e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9626e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9626e-121">Ajout de Salesforce à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9626e-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="9626e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="9626e-123">Ajout de Salesforce à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9626e-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="9626e-124">tooconfigure hello intégration de Salesforce dans Azure AD, vous devez tooadd Salesforce à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9626e-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9626e-125">**tooadd force de vente à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9626e-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9626e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9626e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9626e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9626e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9626e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9626e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9626e-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9626e-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9626e-133">Dans la zone de recherche de hello, tapez **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="9626e-133">In hello search box, type **Salesforce**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="9626e-135">Dans le volet de résultats hello, sélectionnez **Salesforce**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9626e-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9626e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9626e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Salesforce, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9626e-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9626e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Salesforce est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9626e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="9626e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Salesforce doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9626e-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="9626e-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="9626e-142">tooconfigure et test Azure AD l’authentification unique auprès de Salesforce, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9626e-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9626e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9626e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9626e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9626e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9626e-145">**[Création d’un utilisateur de test Salesforce](#creating-a-salesforce-test-user)**  -toohave un équivalent de Britta Simon dans Salesforce est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9626e-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9626e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9626e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9626e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9626e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9626e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9626e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="9626e-150">**tooconfigure Azure AD single sign-on avec Salesforce, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9626e-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="9626e-151">Bonjour portail Azure, sur hello **Salesforce** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9626e-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9626e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9626e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="9626e-155">Sur hello **URL et domaine Salesforce** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9626e-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="9626e-157">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="9626e-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="9626e-158">Compte d’entreprise : `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9626e-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="9626e-159">Compte de développeur : `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9626e-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9626e-160">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="9626e-160">These values are not hello real.</span></span> <span data-ttu-id="9626e-161">Mettre à jour ces valeurs avec une URL de connexion réel hello.</span><span class="sxs-lookup"><span data-stu-id="9626e-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="9626e-162">Contact [équipe de support technique de force de vente Client](https://help.salesforce.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="9626e-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="9626e-163">Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9626e-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="9626e-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9626e-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9626e-167">Sur hello **Salesforce Configuration** , cliquez sur **configurer la force de vente** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9626e-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9626e-168">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="9626e-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="9626e-169">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="9626e-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="9626e-170">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à tooyour Salesforce compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9626e-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="9626e-171">Sous hello **administrateur** volet de navigation, cliquez sur **des contrôles de sécurité** tooexpand hello liés de section.</span><span class="sxs-lookup"><span data-stu-id="9626e-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="9626e-172">Puis cliquez sur **Paramètres de l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9626e-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="9626e-174">Sur hello **paramètres d’authentification unique** , cliquez sur hello **modifier** bouton.</span><span class="sxs-lookup"><span data-stu-id="9626e-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="9626e-175">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="9626e-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="9626e-176">Si vous êtes tooenable Impossible de l’authentification unique sur les paramètres de votre compte Salesforce, vous devrez peut-être toocontact [équipe de support technique de force de vente Client](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="9626e-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="9626e-177">Sélectionnez **SAML activé**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9626e-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="9626e-179">tooconfigure votre SAML unique l’authentification sur les paramètres, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="9626e-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="9626e-181">Sur hello **SAML unique Sign-On Setting Edit** , vérifiez hello suivant configurations :</span><span class="sxs-lookup"><span data-stu-id="9626e-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="9626e-183">a.</span><span class="sxs-lookup"><span data-stu-id="9626e-183">a.</span></span> <span data-ttu-id="9626e-184">Pourquoi **nom** , tapez un nom convivial pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="9626e-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="9626e-185">En fournissant une valeur pour **nom** remplir automatiquement hello **nom de l’API** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="9626e-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="9626e-186">b.</span><span class="sxs-lookup"><span data-stu-id="9626e-186">b.</span></span> <span data-ttu-id="9626e-187">Coller **ID d’entité SMAL** valeur hello **émetteur** champ Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="9626e-188">c.</span><span class="sxs-lookup"><span data-stu-id="9626e-188">c.</span></span> <span data-ttu-id="9626e-189">Bonjour **zone de texte de l’entité**, tapez votre nom de domaine Salesforce à l’aide de hello suivant le modèle :</span><span class="sxs-lookup"><span data-stu-id="9626e-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="9626e-190">Compte d’entreprise : `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9626e-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="9626e-191">Compte de développeur : `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9626e-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="9626e-192">d.</span><span class="sxs-lookup"><span data-stu-id="9626e-192">d.</span></span> <span data-ttu-id="9626e-193">Cliquez sur **Parcourir** ou **choisir un fichier** tooopen hello **tooUpload de choisir un fichier** boîte de dialogue, sélectionnez votre certificat Salesforce, puis cliquez sur **ouvrir**certificat de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="9626e-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="9626e-194">e.</span><span class="sxs-lookup"><span data-stu-id="9626e-194">e.</span></span> <span data-ttu-id="9626e-195">Pour **Type d’identité SAML**, sélectionnez **L’assertion contient le nom d’utilisateur de l’utilisateur salesforce.com**.</span><span class="sxs-lookup"><span data-stu-id="9626e-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="9626e-196">f.</span><span class="sxs-lookup"><span data-stu-id="9626e-196">f.</span></span> <span data-ttu-id="9626e-197">Pour **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello instruction de sujet**</span><span class="sxs-lookup"><span data-stu-id="9626e-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="9626e-198">g.</span><span class="sxs-lookup"><span data-stu-id="9626e-198">g.</span></span> <span data-ttu-id="9626e-199">Coller **-Service URL d’authentification** dans hello **Identity Provider Login URL** champ Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="9626e-200">h.</span><span class="sxs-lookup"><span data-stu-id="9626e-200">h.</span></span> <span data-ttu-id="9626e-201">Pour **Liaison de demande initiée par le fournisseur de service**, sélectionnez **Redirection HTTP**.</span><span class="sxs-lookup"><span data-stu-id="9626e-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="9626e-202">i.</span><span class="sxs-lookup"><span data-stu-id="9626e-202">i.</span></span> <span data-ttu-id="9626e-203">Enfin, cliquez sur **enregistrer** tooapply vos paramètres unique SAML de session.</span><span class="sxs-lookup"><span data-stu-id="9626e-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="9626e-204">Dans le volet de navigation gauche hello dans Salesforce, cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine**.</span><span class="sxs-lookup"><span data-stu-id="9626e-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="9626e-206">Faites défiler vers le bas toohello **Configuration de l’authentification** et cliquez sur hello **modifier** bouton.</span><span class="sxs-lookup"><span data-stu-id="9626e-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="9626e-208">Bonjour **Service d’authentification** section, sélectionnez hello le nom convivial de votre configuration de SAML SSO, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9626e-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="9626e-210">Si plus d’un service d’authentification est activée, les utilisateurs sont demandée tooselect le service d’authentification qu’ils aiment toosign avec lors de l’initialisation d’environnement de Salesforce tooyour de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9626e-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="9626e-211">Si vous ne souhaitez pas qu’il toohappen, vous devez **laisser tous les autres services d’authentification désactivée**.</span><span class="sxs-lookup"><span data-stu-id="9626e-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="9626e-212">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="9626e-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9626e-213">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** section, cliquez simplement sur **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="9626e-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9626e-214">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9626e-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9626e-215">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="9626e-216">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9626e-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9626e-218">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9626e-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9626e-219">Dans le volet de navigation gauche hello Bonjour **portail Azure**, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9626e-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9626e-221">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9626e-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9626e-223">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9626e-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9626e-225">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9626e-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9626e-227">a.</span><span class="sxs-lookup"><span data-stu-id="9626e-227">a.</span></span> <span data-ttu-id="9626e-228">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9626e-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9626e-229">b.</span><span class="sxs-lookup"><span data-stu-id="9626e-229">b.</span></span> <span data-ttu-id="9626e-230">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9626e-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9626e-231">c.</span><span class="sxs-lookup"><span data-stu-id="9626e-231">c.</span></span> <span data-ttu-id="9626e-232">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9626e-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9626e-233">d.</span><span class="sxs-lookup"><span data-stu-id="9626e-233">d.</span></span> <span data-ttu-id="9626e-234">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9626e-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="9626e-235">Création d’un utilisateur de test Salesforce</span><span class="sxs-lookup"><span data-stu-id="9626e-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="9626e-236">Dans cette section, un utilisateur appelé Britta Simon est créé dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="9626e-237">Salesforce prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="9626e-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="9626e-238">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9626e-238">There is no action item for you in this section.</span></span> <span data-ttu-id="9626e-239">Si un utilisateur n’existe pas déjà dans Salesforce, un nouveau est créé lorsque vous essayez de tooaccess Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9626e-240">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9626e-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9626e-241">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="9626e-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9626e-243">**tooassign Britta Simon tooSalesforce, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9626e-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="9626e-244">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9626e-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9626e-246">Dans la liste des applications hello, sélectionnez **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="9626e-246">In hello applications list, select **Salesforce**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="9626e-248">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9626e-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9626e-250">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9626e-250">Click **Add** button.</span></span> <span data-ttu-id="9626e-251">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9626e-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9626e-253">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9626e-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9626e-254">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9626e-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9626e-255">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9626e-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9626e-256">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9626e-256">Testing single sign-on</span></span>

<span data-ttu-id="9626e-257">tootest votre seule paramètres d’authentification, ouvrez hello volet d’accès au [https://myapps.microsoft.com](https://myapps.microsoft.com/), puis connectez-vous à un compte de test hello, puis cliquez sur **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="9626e-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9626e-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9626e-258">Additional resources</span></span>

* [<span data-ttu-id="9626e-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9626e-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9626e-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9626e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9626e-261">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="9626e-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

