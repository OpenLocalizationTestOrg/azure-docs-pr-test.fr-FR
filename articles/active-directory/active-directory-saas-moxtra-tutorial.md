---
title: "Tutorial: Intégration d'Azure Active Directory à Moxtra | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="5ee70-103">Didacticiel : Intégration d'Azure Active Directory avec Moxtra</span><span class="sxs-lookup"><span data-stu-id="5ee70-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="5ee70-104">Dans ce didacticiel, vous apprendrez comment toointegrate Moxtra avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ee70-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ee70-105">Intégration Moxtra à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5ee70-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ee70-106">Vous pouvez contrôler dans Azure AD qui a accès tooMoxtra</span><span class="sxs-lookup"><span data-stu-id="5ee70-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="5ee70-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMoxtra (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ee70-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5ee70-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ee70-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ee70-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ee70-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5ee70-110">Prerequisites</span></span>

<span data-ttu-id="5ee70-111">tooconfigure moxtra intégration d’Azure AD, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5ee70-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="5ee70-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ee70-113">Un abonnement Moxtra pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5ee70-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ee70-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5ee70-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ee70-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5ee70-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ee70-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5ee70-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ee70-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ee70-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ee70-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5ee70-118">Scenario description</span></span>
<span data-ttu-id="5ee70-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5ee70-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ee70-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5ee70-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ee70-121">Ajout de Moxtra à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5ee70-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="5ee70-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="5ee70-123">Ajout de Moxtra à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5ee70-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="5ee70-124">intégration de hello tooconfigure de Moxtra dans Azure AD, vous devez tooadd Moxtra à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5ee70-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ee70-125">**tooadd Moxtra à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ee70-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee70-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5ee70-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ee70-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ee70-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5ee70-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5ee70-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5ee70-133">Dans la zone de recherche de hello, tapez **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-133">In hello search box, type **Moxtra**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="5ee70-135">Dans le volet de résultats hello, sélectionnez **Moxtra**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5ee70-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ee70-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ee70-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Moxtra, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5ee70-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ee70-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Moxtra est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ee70-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="5ee70-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Moxtra doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5ee70-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="5ee70-141">Dans Moxtra, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5ee70-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5ee70-142">tooconfigure et test Azure AD l’authentification unique sur moxtra, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5ee70-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ee70-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5ee70-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ee70-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ee70-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ee70-145">**[Création d’un utilisateur de test Moxtra](#creating-a-moxtra-test-user)**  -toohave un équivalent de Britta Simon dans Moxtra est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5ee70-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ee70-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5ee70-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ee70-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5ee70-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ee70-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ee70-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Moxtra.</span><span class="sxs-lookup"><span data-stu-id="5ee70-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="5ee70-150">**tooconfigure Azure AD l’authentification unique sur moxtra, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ee70-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee70-151">Bonjour portail Azure, sur hello **Moxtra** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5ee70-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5ee70-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="5ee70-155">Sur hello **Moxtra domaine et les URL** section, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="5ee70-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="5ee70-157">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="5ee70-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="5ee70-158">Moxtra application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="5ee70-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="5ee70-159">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="5ee70-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="5ee70-160">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="5ee70-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="5ee70-161">Hello suivant capture d’écran montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="5ee70-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="5ee70-163">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ee70-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="5ee70-164">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="5ee70-164">Attribute Name</span></span> | <span data-ttu-id="5ee70-165">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="5ee70-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="5ee70-166">firstname</span><span class="sxs-lookup"><span data-stu-id="5ee70-166">firstname</span></span> | <span data-ttu-id="5ee70-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5ee70-167">user.givenname</span></span> |
    | <span data-ttu-id="5ee70-168">lastname</span><span class="sxs-lookup"><span data-stu-id="5ee70-168">lastname</span></span> | <span data-ttu-id="5ee70-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="5ee70-169">user.surname</span></span> |
    | <span data-ttu-id="5ee70-170">idpid</span><span class="sxs-lookup"><span data-stu-id="5ee70-170">idpid</span></span>    | <span data-ttu-id="5ee70-171">< ID d’entité SAML ></span><span class="sxs-lookup"><span data-stu-id="5ee70-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="5ee70-172">Hello valeur **idpid** attribut n’est pas réel.</span><span class="sxs-lookup"><span data-stu-id="5ee70-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="5ee70-173">Vous pouvez obtenir la valeur réelle de hello de **aide-mémoire** sous **Moxtra Configuration**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="5ee70-174">a.</span><span class="sxs-lookup"><span data-stu-id="5ee70-174">a.</span></span> <span data-ttu-id="5ee70-175">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5ee70-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="5ee70-177">b.</span><span class="sxs-lookup"><span data-stu-id="5ee70-177">b.</span></span> <span data-ttu-id="5ee70-178">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5ee70-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5ee70-180">c.</span><span class="sxs-lookup"><span data-stu-id="5ee70-180">c.</span></span> <span data-ttu-id="5ee70-181">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5ee70-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="5ee70-182">d.</span><span class="sxs-lookup"><span data-stu-id="5ee70-182">d.</span></span> <span data-ttu-id="5ee70-183">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="5ee70-184">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5ee70-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="5ee70-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5ee70-186">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5ee70-188">Sur hello **Moxtra Configuration** , cliquez sur **Moxtra de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5ee70-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ee70-189">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5ee70-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="5ee70-191">Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour Moxtra en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5ee70-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="5ee70-192">Dans la barre d’outils de hello en hello gauche, cliquez sur **Console d’administration > SAML Single Sign-on**, puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="5ee70-194">Sur hello **SAML** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ee70-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="5ee70-196">a.</span><span class="sxs-lookup"><span data-stu-id="5ee70-196">a.</span></span> <span data-ttu-id="5ee70-197">Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : *SAML*).</span><span class="sxs-lookup"><span data-stu-id="5ee70-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="5ee70-198">b.</span><span class="sxs-lookup"><span data-stu-id="5ee70-198">b.</span></span> <span data-ttu-id="5ee70-199">Bonjour **IdP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee70-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="5ee70-200">c.</span><span class="sxs-lookup"><span data-stu-id="5ee70-200">c.</span></span> <span data-ttu-id="5ee70-201">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee70-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="5ee70-202">d.</span><span class="sxs-lookup"><span data-stu-id="5ee70-202">d.</span></span> <span data-ttu-id="5ee70-203">Bonjour **AuthnContextClassRef** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="5ee70-204">e.</span><span class="sxs-lookup"><span data-stu-id="5ee70-204">e.</span></span> <span data-ttu-id="5ee70-205">Bonjour **NameID Format** zone de texte, type **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="5ee70-206">f.</span><span class="sxs-lookup"><span data-stu-id="5ee70-206">f.</span></span> <span data-ttu-id="5ee70-207">Ouvrir certificat dont vous avez téléchargé à partir du portail Azure dans le bloc-notes, copier le contenu de hello et collez-le à hello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5ee70-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="5ee70-208">g.</span><span class="sxs-lookup"><span data-stu-id="5ee70-208">g.</span></span> <span data-ttu-id="5ee70-209">Dans la zone de domaine hello SAML par courrier électronique, tapez votre domaine de messagerie SAML.</span><span class="sxs-lookup"><span data-stu-id="5ee70-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="5ee70-210">domaine de hello tooverify toosee hello étapes, cliquez sur hello »**i**» ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5ee70-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="5ee70-211">h.</span><span class="sxs-lookup"><span data-stu-id="5ee70-211">h.</span></span> <span data-ttu-id="5ee70-212">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="5ee70-213">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5ee70-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ee70-214">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5ee70-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ee70-215">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ee70-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ee70-216">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ee70-217">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5ee70-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5ee70-219">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ee70-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee70-220">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5ee70-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ee70-222">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ee70-224">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5ee70-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ee70-226">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ee70-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ee70-228">a.</span><span class="sxs-lookup"><span data-stu-id="5ee70-228">a.</span></span> <span data-ttu-id="5ee70-229">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ee70-230">b.</span><span class="sxs-lookup"><span data-stu-id="5ee70-230">b.</span></span> <span data-ttu-id="5ee70-231">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ee70-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ee70-232">c.</span><span class="sxs-lookup"><span data-stu-id="5ee70-232">c.</span></span> <span data-ttu-id="5ee70-233">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ee70-234">d.</span><span class="sxs-lookup"><span data-stu-id="5ee70-234">d.</span></span> <span data-ttu-id="5ee70-235">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="5ee70-236">Création d'un utilisateur de test Moxtra</span><span class="sxs-lookup"><span data-stu-id="5ee70-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="5ee70-237">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Moxtra.</span><span class="sxs-lookup"><span data-stu-id="5ee70-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="5ee70-238">**toocreate un utilisateur appelé Britta Simon dans Moxtra, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ee70-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee70-239">Se connecter tooyour Moxtra site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5ee70-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="5ee70-240">Dans la barre d’outils de hello en hello gauche, cliquez sur **Console d’administration > Gestion des utilisateurs**, puis **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="5ee70-242">Sur hello **ajouter un utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ee70-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="5ee70-243">a.</span><span class="sxs-lookup"><span data-stu-id="5ee70-243">a.</span></span> <span data-ttu-id="5ee70-244">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="5ee70-245">b.</span><span class="sxs-lookup"><span data-stu-id="5ee70-245">b.</span></span> <span data-ttu-id="5ee70-246">Bonjour **nom** zone de texte, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="5ee70-247">c.</span><span class="sxs-lookup"><span data-stu-id="5ee70-247">c.</span></span> <span data-ttu-id="5ee70-248">Bonjour **messagerie** zone de texte, type d’adresse de messagerie de Brian même que sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee70-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="5ee70-249">d.</span><span class="sxs-lookup"><span data-stu-id="5ee70-249">d.</span></span> <span data-ttu-id="5ee70-250">Bonjour **Division** zone de texte, type **Dev**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="5ee70-251">e.</span><span class="sxs-lookup"><span data-stu-id="5ee70-251">e.</span></span> <span data-ttu-id="5ee70-252">Bonjour **service** zone de texte, type **informatique**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="5ee70-253">f.</span><span class="sxs-lookup"><span data-stu-id="5ee70-253">f.</span></span> <span data-ttu-id="5ee70-254">Sélectionnez **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="5ee70-255">g.</span><span class="sxs-lookup"><span data-stu-id="5ee70-255">g.</span></span> <span data-ttu-id="5ee70-256">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ee70-257">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee70-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ee70-258">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMoxtra.</span><span class="sxs-lookup"><span data-stu-id="5ee70-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5ee70-260">**tooassign Britta Simon tooMoxtra, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ee70-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee70-261">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5ee70-263">Dans la liste des applications hello, sélectionnez **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-263">In hello applications list, select **Moxtra**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="5ee70-265">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5ee70-267">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-267">Click **Add** button.</span></span> <span data-ttu-id="5ee70-268">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5ee70-270">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5ee70-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ee70-271">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ee70-272">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5ee70-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ee70-273">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5ee70-273">Testing single sign-on</span></span>

<span data-ttu-id="5ee70-274">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5ee70-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5ee70-275">Lorsque vous cliquez sur mosaïque Moxtra hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Moxtra application.</span><span class="sxs-lookup"><span data-stu-id="5ee70-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="5ee70-276">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ee70-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ee70-277">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5ee70-277">Additional resources</span></span>

* [<span data-ttu-id="5ee70-278">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ee70-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ee70-279">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5ee70-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

