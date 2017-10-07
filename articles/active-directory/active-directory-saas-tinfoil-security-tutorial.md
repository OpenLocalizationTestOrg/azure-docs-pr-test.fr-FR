---
title: "Didacticiel : Intégration d’Azure Active Directory à TINFOIL SECURITY | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="931cc-103">Didacticiel : Intégration d’Azure Active Directory à TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="931cc-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="931cc-104">Dans ce didacticiel, vous apprendrez comment toointegrate TINFOIL SECURITY avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="931cc-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="931cc-105">Intégration de TINFOIL SECURITY à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="931cc-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="931cc-106">Vous pouvez contrôler dans Azure AD qui a accès tooTINFOIL sécurité</span><span class="sxs-lookup"><span data-stu-id="931cc-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="931cc-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTINFOIL sécurité (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="931cc-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="931cc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="931cc-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="931cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="931cc-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="931cc-110">Prerequisites</span></span>

<span data-ttu-id="931cc-111">tooconfigure intégration d’Azure AD à TINFOIL SECURITY, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="931cc-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="931cc-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="931cc-113">Un abonnement TINFOIL SECURITY pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="931cc-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="931cc-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="931cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="931cc-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="931cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="931cc-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="931cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="931cc-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="931cc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="931cc-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="931cc-118">Scenario description</span></span>
<span data-ttu-id="931cc-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="931cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="931cc-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="931cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="931cc-121">Ajouter TINFOIL SECURITY à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="931cc-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="931cc-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="931cc-123">Ajouter TINFOIL SECURITY à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="931cc-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="931cc-124">intégration de hello tooconfigure de TINFOIL SECURITY dans Azure AD, vous devez tooadd TINFOIL SECURITY à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="931cc-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="931cc-125">**tooadd TINFOIL SECURITY à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931cc-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="931cc-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="931cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="931cc-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="931cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="931cc-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="931cc-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="931cc-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="931cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="931cc-133">Dans la zone de recherche de hello, tapez **TINFOIL SECURITY**, sélectionnez **TINFOIL SECURITY** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="931cc-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TINFOIL SECURITY à partir de la galerie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="931cc-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="931cc-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TINFOIL SECURITY, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="931cc-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="931cc-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello TINFOIL SECURITY est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931cc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="931cc-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur en mode de sécurité TINFOIL hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="931cc-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="931cc-139">Dans TINFOIL SECURITY, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="931cc-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="931cc-140">tooconfigure et test Azure AD l’authentification unique avec TINFOIL SECURITY, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="931cc-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="931cc-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="931cc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="931cc-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="931cc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="931cc-143">**[Créer un utilisateur de test de TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave un équivalent de Britta Simon dans TINFOIL SECURITY qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="931cc-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="931cc-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="931cc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="931cc-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="931cc-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="931cc-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="931cc-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="931cc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="931cc-148">**tooconfigure Azure AD single sign-on avec TINFOIL SECURITY, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931cc-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="931cc-149">Bonjour portail Azure, sur hello **TINFOIL SECURITY** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="931cc-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="931cc-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="931cc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="931cc-153">Sur hello **URL et le domaine de sécurité TINFOIL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="931cc-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="931cc-155">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur.</span><span class="sxs-lookup"><span data-stu-id="931cc-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="931cc-157">mappages d’attributs tooadd hello requis, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="931cc-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="931cc-158">![Attributs](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="931cc-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="931cc-159">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="931cc-159">Attribute Name</span></span>    |   <span data-ttu-id="931cc-160">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="931cc-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="931cc-161">accountid</span><span class="sxs-lookup"><span data-stu-id="931cc-161">accountid</span></span> | <span data-ttu-id="931cc-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="931cc-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="931cc-163">a.</span><span class="sxs-lookup"><span data-stu-id="931cc-163">a.</span></span> <span data-ttu-id="931cc-164">Cliquez sur **Ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="931cc-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="931cc-165">![Ajouter un attribut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="931cc-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="931cc-166">![Ajouter un attribut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="931cc-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="931cc-167">b.</span><span class="sxs-lookup"><span data-stu-id="931cc-167">b.</span></span> <span data-ttu-id="931cc-168">Bonjour **nom de l’attribut** zone de texte, type **accountid**.</span><span class="sxs-lookup"><span data-stu-id="931cc-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="931cc-169">c.</span><span class="sxs-lookup"><span data-stu-id="931cc-169">c.</span></span> <span data-ttu-id="931cc-170">Bonjour **valeur d’attribut** zone de texte, valeur d’ID coller hello compte qui vous obtiendrez ultérieure du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="931cc-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="931cc-171">d.</span><span class="sxs-lookup"><span data-stu-id="931cc-171">d.</span></span> <span data-ttu-id="931cc-172">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="931cc-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="931cc-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="931cc-173">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="931cc-175">Sur hello **Configuration de la sécurité TINFOIL** , cliquez sur **configurer la sécurité TINFOIL** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="931cc-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="931cc-176">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="931cc-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="931cc-178">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TINFOIL SECURITY en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="931cc-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="931cc-179">Dans la barre d’outils de hello en haut de hello, cliquez sur **mon compte**.</span><span class="sxs-lookup"><span data-stu-id="931cc-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="931cc-180">![Tableau de bord](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Tableau de bord")</span><span class="sxs-lookup"><span data-stu-id="931cc-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="931cc-181">Cliquez sur **Security**.</span><span class="sxs-lookup"><span data-stu-id="931cc-181">Click **Security**.</span></span>
   
    <span data-ttu-id="931cc-182">![Sécurité](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="931cc-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="931cc-183">Sur hello **Single Sign-On** configuration page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="931cc-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="931cc-184">![Authentification unique](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="931cc-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="931cc-185">a.</span><span class="sxs-lookup"><span data-stu-id="931cc-185">a.</span></span> <span data-ttu-id="931cc-186">Sélectionnez **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="931cc-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="931cc-187">b.</span><span class="sxs-lookup"><span data-stu-id="931cc-187">b.</span></span> <span data-ttu-id="931cc-188">Cliquez sur **Manual Configuration**.</span><span class="sxs-lookup"><span data-stu-id="931cc-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="931cc-189">c.</span><span class="sxs-lookup"><span data-stu-id="931cc-189">c.</span></span> <span data-ttu-id="931cc-190">Dans **URL de publication SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="931cc-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="931cc-191">d.</span><span class="sxs-lookup"><span data-stu-id="931cc-191">d.</span></span> <span data-ttu-id="931cc-192">Dans **empreinte numérique du certificat SAML** zone de texte, valeur hello coller **l’empreinte numérique** dont vous avez copié à partir de **le certificat de signature SAML** section.</span><span class="sxs-lookup"><span data-stu-id="931cc-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="931cc-193">e.</span><span class="sxs-lookup"><span data-stu-id="931cc-193">e.</span></span> <span data-ttu-id="931cc-194">Copie **votre ID de compte** valeur et collez la valeur hello dans **valeur d’attribut** zone de texte sous **ajouter un attribut** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="931cc-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="931cc-195">f.</span><span class="sxs-lookup"><span data-stu-id="931cc-195">f.</span></span> <span data-ttu-id="931cc-196">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="931cc-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="931cc-197">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="931cc-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="931cc-198">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="931cc-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="931cc-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="931cc-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="931cc-200">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-200">Create an Azure AD test user</span></span>
<span data-ttu-id="931cc-201">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="931cc-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="931cc-203">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931cc-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="931cc-204">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="931cc-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="931cc-206">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="931cc-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="931cc-207">Utilisateurs et groupes -> Tous les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="931cc-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="931cc-208">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="931cc-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Utilisateur](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="931cc-210">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="931cc-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="931cc-212">a.</span><span class="sxs-lookup"><span data-stu-id="931cc-212">a.</span></span> <span data-ttu-id="931cc-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="931cc-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="931cc-214">b.</span><span class="sxs-lookup"><span data-stu-id="931cc-214">b.</span></span> <span data-ttu-id="931cc-215">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="931cc-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="931cc-216">c.</span><span class="sxs-lookup"><span data-stu-id="931cc-216">c.</span></span> <span data-ttu-id="931cc-217">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="931cc-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="931cc-218">d.</span><span class="sxs-lookup"><span data-stu-id="931cc-218">d.</span></span> <span data-ttu-id="931cc-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="931cc-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="931cc-220">Créer un utilisateur de test TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="931cc-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="931cc-221">Dans l’ordre tooenable Azure AD les utilisateurs toolog à TINFOIL SECURITY, vous devez les configurer sur TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="931cc-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="931cc-222">Dans les cas de hello de TINFOIL SECURITY, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="931cc-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="931cc-223">**tooget un utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931cc-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="931cc-224">Si l’utilisateur de hello fait partie d’un compte d’entreprise, vous devez trop[contacter l’équipe de support de TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) compte d’utilisateur tooget hello créé.</span><span class="sxs-lookup"><span data-stu-id="931cc-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="931cc-225">Si l’utilisateur de hello est un utilisateur normal de TINFOIL SECURITY SaaS, utilisateur de hello peut ajouter un tooany collaborateur de sites de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="931cc-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="931cc-226">Par courrier électronique un toosend de processus une toohello invitation spécifié cette déclencheurs toocreate un nouveau compte d’utilisateur TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="931cc-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="931cc-227">Vous pouvez utiliser n’importe quel autre TINFOIL SECURITY utilisateur compte outil de création ou API fournie par TINFOIL SECURITY tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931cc-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="931cc-228">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="931cc-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="931cc-229">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTINFOIL sécurité.</span><span class="sxs-lookup"><span data-stu-id="931cc-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="931cc-231">**tooassign Britta Simon tooTINFOIL sécurité, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931cc-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="931cc-232">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="931cc-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="931cc-234">Dans la liste des applications hello, sélectionnez **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="931cc-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![Sélectionner TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="931cc-236">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="931cc-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="931cc-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="931cc-238">Click **Add** button.</span></span> <span data-ttu-id="931cc-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="931cc-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="931cc-241">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="931cc-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="931cc-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="931cc-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="931cc-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="931cc-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="931cc-244">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="931cc-244">Test single sign-on</span></span>

<span data-ttu-id="931cc-245">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="931cc-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="931cc-246">Lorsque vous cliquez sur mosaïque de TINFOIL SECURITY hello Bonjour volet d’accès, vous devez obtenir l’application de TINFOIL SECURITY tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="931cc-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="931cc-247">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="931cc-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="931cc-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="931cc-248">Additional resources</span></span>

* [<span data-ttu-id="931cc-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="931cc-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="931cc-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="931cc-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

