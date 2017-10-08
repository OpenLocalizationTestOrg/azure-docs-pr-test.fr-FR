---
title: "Didacticiel : Intégration d’Azure Active Directory avec DocuSign | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="a6546-103">Didacticiel : Intégration d’Azure Active Directory avec DocuSign</span><span class="sxs-lookup"><span data-stu-id="a6546-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="a6546-104">Dans ce didacticiel, vous apprendrez comment toointegrate DocuSign avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6546-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6546-105">Intégration de DocuSign à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a6546-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6546-106">Vous pouvez contrôler dans Azure AD qui a accès tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="a6546-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="a6546-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDocuSign (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6546-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a6546-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a6546-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6546-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6546-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a6546-110">Prerequisites</span></span>

<span data-ttu-id="a6546-111">tooconfigure intégration d’Azure AD à DocuSign, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a6546-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="a6546-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6546-113">Un abonnement DocuSign pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a6546-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6546-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a6546-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6546-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a6546-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6546-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a6546-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6546-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6546-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6546-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a6546-118">Scenario description</span></span>
<span data-ttu-id="a6546-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a6546-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6546-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a6546-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6546-121">Ajout de DocuSign à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a6546-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="a6546-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="a6546-123">Ajout de DocuSign à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a6546-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="a6546-124">intégration de hello tooconfigure de DocuSign dans Azure AD, vous devez tooadd DocuSign à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a6546-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6546-125">**tooadd DocuSign à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6546-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6546-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a6546-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6546-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a6546-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a6546-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a6546-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a6546-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a6546-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a6546-133">Dans la zone de recherche de hello, tapez **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="a6546-133">In hello search box, type **DocuSign**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="a6546-135">Dans le volet de résultats hello, sélectionnez **DocuSign**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a6546-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6546-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6546-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec DocuSign, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a6546-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6546-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans DocuSign est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6546-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="a6546-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans DocuSign doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a6546-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="a6546-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a6546-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="a6546-142">tooconfigure et test Azure AD l’authentification unique à DocuSign, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a6546-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a6546-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a6546-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6546-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6546-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6546-145">**[Création d’un utilisateur de test DocuSign](#creating-a-docusign-test-user)**  -toohave un équivalent de Britta Simon dans DocuSign est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6546-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6546-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a6546-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6546-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a6546-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6546-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6546-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a6546-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="a6546-150">**tooconfigure Azure AD single sign-on avec DocuSign, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6546-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6546-151">Bonjour portail Azure, sur hello **DocuSign** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a6546-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a6546-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a6546-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="a6546-155">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base 64)** , puis enregistrez le fichier de certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a6546-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="a6546-157">Sur hello **DocuSign Configuration** section du portail Azure, cliquez sur **DocuSign de configuration** tooopen configurer l’authentification sur fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a6546-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="a6546-158">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a6546-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="a6546-160">Dans une fenêtre de navigateur web, connexion tooyour **portail d’administration DocuSign** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a6546-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="a6546-161">Dans le menu de navigation hello hello gauche, cliquez sur **domaines**.</span><span class="sxs-lookup"><span data-stu-id="a6546-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Configuration de l'authentification unique][51]

7. <span data-ttu-id="a6546-163">Dans le volet droit de hello, cliquez sur **revendication domaine**.</span><span class="sxs-lookup"><span data-stu-id="a6546-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Configuration de l'authentification unique][52]

8. <span data-ttu-id="a6546-165">Sur hello **revendication d’un domaine** boîte de dialogue, Bonjour **nom de domaine** zone de texte, tapez le domaine de votre entreprise, puis cliquez sur **revendication**.</span><span class="sxs-lookup"><span data-stu-id="a6546-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="a6546-166">Assurez-vous que vous vérifiez le domaine de hello et hello état est actif.</span><span class="sxs-lookup"><span data-stu-id="a6546-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Configuration de l'authentification unique][53]

9. <span data-ttu-id="a6546-168">Dans le menu hello situé à gauche, cliquez sur **fournisseurs d’identité**</span><span class="sxs-lookup"><span data-stu-id="a6546-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Configuration de l'authentification unique][54]
10. <span data-ttu-id="a6546-170">Dans le volet droit de hello, cliquez sur **ajouter un fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="a6546-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configuration de l'authentification unique][55]

11. <span data-ttu-id="a6546-172">Sur hello **paramètres de fournisseur d’identité** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6546-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Configuration de l'authentification unique][56]

    <span data-ttu-id="a6546-174">a.</span><span class="sxs-lookup"><span data-stu-id="a6546-174">a.</span></span> <span data-ttu-id="a6546-175">Bonjour **nom** zone de texte, tapez un nom unique pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="a6546-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="a6546-176">N’utilisez pas d’espaces.</span><span class="sxs-lookup"><span data-stu-id="a6546-176">Do not use spaces.</span></span>

    <span data-ttu-id="a6546-177">b.</span><span class="sxs-lookup"><span data-stu-id="a6546-177">b.</span></span> <span data-ttu-id="a6546-178">Coller **ID d’entité SAML** dans hello **émetteur de fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a6546-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="a6546-179">c.</span><span class="sxs-lookup"><span data-stu-id="a6546-179">c.</span></span> <span data-ttu-id="a6546-180">Coller **SAML Sign-On URL du Service unique** dans hello **Identity Provider Login URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a6546-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a6546-181">d.</span><span class="sxs-lookup"><span data-stu-id="a6546-181">d.</span></span> <span data-ttu-id="a6546-182">Coller **URL de déconnexion** dans hello **Identity Provider Logout URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a6546-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="a6546-183">e.</span><span class="sxs-lookup"><span data-stu-id="a6546-183">e.</span></span> <span data-ttu-id="a6546-184">Sélectionnez **Sign AuthN Request**(Signer la demande d’authentification).</span><span class="sxs-lookup"><span data-stu-id="a6546-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="a6546-185">f.</span><span class="sxs-lookup"><span data-stu-id="a6546-185">f.</span></span> <span data-ttu-id="a6546-186">Sous **Send AuthN request by** (Envoyer la demande d’authentification par), sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="a6546-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="a6546-187">g.</span><span class="sxs-lookup"><span data-stu-id="a6546-187">g.</span></span> <span data-ttu-id="a6546-188">Sous **Send logout request by** (Envoyer la demande de déconnexion par), sélectionnez **GET**.</span><span class="sxs-lookup"><span data-stu-id="a6546-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="a6546-189">Bonjour **un mappage d’attribut personnalisé** , choisissez le champ de hello souhaité toomap avec Azure AD revendication.</span><span class="sxs-lookup"><span data-stu-id="a6546-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="a6546-190">Dans cet exemple, hello **emailaddress** revendication est mappée avec la valeur hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="a6546-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="a6546-191">Il est le nom de la revendication hello par défaut à partir d’Azure AD pour une revendication de courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="a6546-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="a6546-192">Hello utilisation appropriée **identificateur de l’utilisateur** utilisateur de hello toomap du mappage d’utilisateur Azure AD tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="a6546-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="a6546-193">Sélectionnez hello champ approprié et entrez la valeur appropriée de hello en fonction des paramètres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="a6546-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Configuration de l'authentification unique][57]

13. <span data-ttu-id="a6546-195">Bonjour **certificat de fournisseur d’identité** , cliquez sur **ajouter un certificat**, puis téléchargez le certificat hello que vous avez téléchargé à partir du portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6546-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configuration de l'authentification unique][58]

14. <span data-ttu-id="a6546-197">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a6546-197">Click **Save**.</span></span>

15. <span data-ttu-id="a6546-198">Bonjour **fournisseurs d’identité** , cliquez sur **Actions**, puis cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="a6546-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configuration de l'authentification unique][59]
 
16. <span data-ttu-id="a6546-200">Bonjour **2.0 points de terminaison SAML** section **portail d’administration DocuSign**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6546-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Configuration de l'authentification unique][60]
   
    <span data-ttu-id="a6546-202">a.</span><span class="sxs-lookup"><span data-stu-id="a6546-202">a.</span></span> <span data-ttu-id="a6546-203">Hello de copie **URL de l’émetteur de fournisseur de Service**, puis collez dans hello **identificateur** zone de texte sur **DocuSign domaine et les URL** section Hello hello suivant de portail Azure modèle : `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="a6546-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="a6546-204">b.</span><span class="sxs-lookup"><span data-stu-id="a6546-204">b.</span></span> <span data-ttu-id="a6546-205">Hello de copie **Service Provider Login URL**, puis collez dans hello **URL de connexion** zone de texte sur **DocuSign domaine et les URL** section Hello hello suivant de portail Azure modèle : `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="a6546-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="a6546-207">c.</span><span class="sxs-lookup"><span data-stu-id="a6546-207">c.</span></span>  <span data-ttu-id="a6546-208">Cliquez sur **Fermer**</span><span class="sxs-lookup"><span data-stu-id="a6546-208">Click **Close**</span></span>
    
17. <span data-ttu-id="a6546-209">Dans hello portail Azure, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a6546-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="a6546-211">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a6546-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a6546-212">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a6546-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a6546-213">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6546-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6546-214">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6546-215">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a6546-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a6546-217">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6546-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6546-218">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a6546-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6546-220">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a6546-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6546-222">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a6546-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6546-224">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6546-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6546-226">a.</span><span class="sxs-lookup"><span data-stu-id="a6546-226">a.</span></span> <span data-ttu-id="a6546-227">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6546-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6546-228">b.</span><span class="sxs-lookup"><span data-stu-id="a6546-228">b.</span></span> <span data-ttu-id="a6546-229">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a6546-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6546-230">c.</span><span class="sxs-lookup"><span data-stu-id="a6546-230">c.</span></span> <span data-ttu-id="a6546-231">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a6546-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a6546-232">d.</span><span class="sxs-lookup"><span data-stu-id="a6546-232">d.</span></span> <span data-ttu-id="a6546-233">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6546-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="a6546-234">Création d’un utilisateur de test DocuSign</span><span class="sxs-lookup"><span data-stu-id="a6546-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="a6546-235">Prend en charge de l’application **juste à temps l’approvisionnement des utilisateurs** et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6546-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a6546-236">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6546-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a6546-237">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooDocuSign de son accès.</span><span class="sxs-lookup"><span data-stu-id="a6546-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a6546-239">**tooassign Britta Simon tooDocuSign, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6546-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6546-240">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a6546-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a6546-242">Dans la liste des applications hello, sélectionnez **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="a6546-242">In hello applications list, select **DocuSign**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="a6546-244">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a6546-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a6546-246">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a6546-246">Click **Add** button.</span></span> <span data-ttu-id="a6546-247">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a6546-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a6546-249">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a6546-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a6546-250">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a6546-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6546-251">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a6546-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6546-252">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a6546-252">Testing single sign-on</span></span>

<span data-ttu-id="a6546-253">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a6546-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a6546-254">Lorsque vous cliquez sur mosaïque DocuSign hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour DocuSign application.</span><span class="sxs-lookup"><span data-stu-id="a6546-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="a6546-255">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a6546-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a6546-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a6546-256">Additional resources</span></span>

* [<span data-ttu-id="a6546-257">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6546-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6546-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a6546-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a6546-259">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a6546-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

