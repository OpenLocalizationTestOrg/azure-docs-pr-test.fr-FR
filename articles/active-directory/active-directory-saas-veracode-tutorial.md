---
title: "Didacticiel : Intégration d’Azure Active Directory à Veracode | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="edc27-103">Didacticiel : Intégration d’Azure AD à Veracode</span><span class="sxs-lookup"><span data-stu-id="edc27-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="edc27-104">Dans ce didacticiel, vous apprendrez comment toointegrate Veracode avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edc27-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edc27-105">Intégration Veracode à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="edc27-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edc27-106">Vous pouvez contrôler dans Azure AD qui a accès tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="edc27-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="edc27-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooVeracode (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edc27-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="edc27-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="edc27-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="edc27-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edc27-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edc27-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="edc27-110">Prerequisites</span></span>

<span data-ttu-id="edc27-111">tooconfigure veracode intégration d’Azure AD, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="edc27-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="edc27-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc27-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edc27-113">Un abonnement Veracode pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="edc27-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edc27-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="edc27-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edc27-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="edc27-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edc27-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="edc27-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edc27-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edc27-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edc27-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="edc27-118">Scenario description</span></span>
<span data-ttu-id="edc27-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="edc27-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edc27-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="edc27-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edc27-121">Ajouter des Veracode à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="edc27-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="edc27-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc27-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="edc27-123">Ajouter des Veracode à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="edc27-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="edc27-124">intégration de hello tooconfigure de Veracode dans Azure AD, vous devez tooadd Veracode à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="edc27-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edc27-125">**tooadd Veracode à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="edc27-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc27-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="edc27-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="edc27-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="edc27-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edc27-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="edc27-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="edc27-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="edc27-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="edc27-133">Dans la zone de recherche de hello, tapez **Veracode**, sélectionnez **Veracode** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="edc27-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode dans la liste des résultats hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="edc27-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc27-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="edc27-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Veracode avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="edc27-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edc27-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Veracode est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edc27-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="edc27-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Veracode doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="edc27-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="edc27-139">Dans Veracode, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="edc27-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="edc27-140">tooconfigure et test Azure AD l’authentification unique sur veracode, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="edc27-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edc27-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="edc27-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edc27-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc27-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edc27-143">**[Créer un utilisateur de test Veracode](#create-a-veracode-test-user)**  -toohave un équivalent de Britta Simon dans Veracode est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="edc27-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="edc27-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="edc27-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edc27-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="edc27-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="edc27-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc27-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="edc27-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Veracode.</span><span class="sxs-lookup"><span data-stu-id="edc27-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="edc27-148">**tooconfigure Azure AD l’authentification unique sur veracode, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="edc27-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc27-149">Bonjour portail Azure, sur hello **Veracode** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="edc27-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="edc27-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="edc27-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="edc27-153">Sur hello **Veracode domaine et les URL** section, l’utilisateur n’a pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="edc27-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="edc27-155">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="edc27-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="edc27-157">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooVeracode avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="edc27-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="edc27-158">Votre application Veracode attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton saml** configuration.</span><span class="sxs-lookup"><span data-stu-id="edc27-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="edc27-159">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="edc27-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="edc27-160">![Attributs](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="edc27-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="edc27-161">mappages d’attributs tooadd hello requis, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="edc27-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="edc27-162">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="edc27-162">Attribute Name</span></span> | <span data-ttu-id="edc27-163">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="edc27-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="edc27-164">firstname</span><span class="sxs-lookup"><span data-stu-id="edc27-164">firstname</span></span> |<span data-ttu-id="edc27-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="edc27-165">User.givenname</span></span> |
    | <span data-ttu-id="edc27-166">lastname</span><span class="sxs-lookup"><span data-stu-id="edc27-166">lastname</span></span> |<span data-ttu-id="edc27-167">User.Surname</span><span class="sxs-lookup"><span data-stu-id="edc27-167">User.surname</span></span> |
    | <span data-ttu-id="edc27-168">email</span><span class="sxs-lookup"><span data-stu-id="edc27-168">email</span></span> |<span data-ttu-id="edc27-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="edc27-169">User.mail</span></span> |
    
    <span data-ttu-id="edc27-170">a.</span><span class="sxs-lookup"><span data-stu-id="edc27-170">a.</span></span> <span data-ttu-id="edc27-171">Pour chaque ligne de données dans la table hello ci-dessus, cliquez sur **ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="edc27-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="edc27-172">![Attributs](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="edc27-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="edc27-173">![Attributs](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="edc27-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="edc27-174">b.</span><span class="sxs-lookup"><span data-stu-id="edc27-174">b.</span></span> <span data-ttu-id="edc27-175">Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="edc27-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="edc27-176">c.</span><span class="sxs-lookup"><span data-stu-id="edc27-176">c.</span></span> <span data-ttu-id="edc27-177">Bonjour **valeur d’attribut** zone de texte, valeur de l’attribut select hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="edc27-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="edc27-178">d.</span><span class="sxs-lookup"><span data-stu-id="edc27-178">d.</span></span> <span data-ttu-id="edc27-179">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="edc27-179">Click **Ok**.</span></span>

7. <span data-ttu-id="edc27-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="edc27-180">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="edc27-182">Sur hello **Veracode Configuration** , cliquez sur **Veracode de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="edc27-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="edc27-183">Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="edc27-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuration de Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="edc27-185">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Veracode en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="edc27-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="edc27-186">Dans le menu hello haut de hello, cliquez sur **paramètres**, puis cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="edc27-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="edc27-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="edc27-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="edc27-188">Cliquez sur hello **SAML** onglet.</span><span class="sxs-lookup"><span data-stu-id="edc27-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="edc27-189">Bonjour **organisation SAML paramètres** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="edc27-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="edc27-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="edc27-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="edc27-191">a.</span><span class="sxs-lookup"><span data-stu-id="edc27-191">a.</span></span>  <span data-ttu-id="edc27-192">Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="edc27-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="edc27-193">b.</span><span class="sxs-lookup"><span data-stu-id="edc27-193">b.</span></span> <span data-ttu-id="edc27-194">Cliquez sur votre certificat téléchargé à partir du portail Azure, de tooupload **choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="edc27-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="edc27-195">c.</span><span class="sxs-lookup"><span data-stu-id="edc27-195">c.</span></span> <span data-ttu-id="edc27-196">Sélectionnez **Enable Self Registration**.</span><span class="sxs-lookup"><span data-stu-id="edc27-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="edc27-197">Bonjour **les paramètres d’inscription libre-service** section, effectuer hello comme suit, puis cliquez sur **enregistrer**:</span><span class="sxs-lookup"><span data-stu-id="edc27-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="edc27-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="edc27-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="edc27-199">a.</span><span class="sxs-lookup"><span data-stu-id="edc27-199">a.</span></span> <span data-ttu-id="edc27-200">Dans **New User Activation**, sélectionnez **No Activation Required**.</span><span class="sxs-lookup"><span data-stu-id="edc27-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="edc27-201">b.</span><span class="sxs-lookup"><span data-stu-id="edc27-201">b.</span></span> <span data-ttu-id="edc27-202">Dans **User Data Updates**, sélectionnez **Preference Veracode User Data**.</span><span class="sxs-lookup"><span data-stu-id="edc27-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="edc27-203">c.</span><span class="sxs-lookup"><span data-stu-id="edc27-203">c.</span></span> <span data-ttu-id="edc27-204">Pour **des détails d’attribut SAML**, sélectionnez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="edc27-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="edc27-205">**Rôles d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="edc27-205">**User Roles**</span></span>
      * <span data-ttu-id="edc27-206">**Administrateur de la stratégie**</span><span class="sxs-lookup"><span data-stu-id="edc27-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="edc27-207">**Réviseur**</span><span class="sxs-lookup"><span data-stu-id="edc27-207">**Reviewer**</span></span>
      * <span data-ttu-id="edc27-208">**Responsable de la sécurité**</span><span class="sxs-lookup"><span data-stu-id="edc27-208">**Security Lead**</span></span>
      * <span data-ttu-id="edc27-209">**Responsable**</span><span class="sxs-lookup"><span data-stu-id="edc27-209">**Executive**</span></span>
      * <span data-ttu-id="edc27-210">**Expéditeur**</span><span class="sxs-lookup"><span data-stu-id="edc27-210">**Submitter**</span></span>
      * <span data-ttu-id="edc27-211">**Créateur**</span><span class="sxs-lookup"><span data-stu-id="edc27-211">**Creator**</span></span>
      * <span data-ttu-id="edc27-212">**Tous les types d’analyse**</span><span class="sxs-lookup"><span data-stu-id="edc27-212">**All Scan Types**</span></span>
      * <span data-ttu-id="edc27-213">**Appartenance aux équipes**</span><span class="sxs-lookup"><span data-stu-id="edc27-213">**Team Memberships**</span></span>
      * <span data-ttu-id="edc27-214">**Équipe par défaut**</span><span class="sxs-lookup"><span data-stu-id="edc27-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="edc27-215">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="edc27-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="edc27-216">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="edc27-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="edc27-217">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edc27-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="edc27-218">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc27-218">Create an Azure AD test user</span></span>

<span data-ttu-id="edc27-219">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="edc27-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="edc27-221">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="edc27-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc27-222">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="edc27-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="edc27-224">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="edc27-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="edc27-226">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="edc27-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="edc27-228">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="edc27-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="edc27-230">a.</span><span class="sxs-lookup"><span data-stu-id="edc27-230">a.</span></span> <span data-ttu-id="edc27-231">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edc27-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edc27-232">b.</span><span class="sxs-lookup"><span data-stu-id="edc27-232">b.</span></span> <span data-ttu-id="edc27-233">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc27-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="edc27-234">c.</span><span class="sxs-lookup"><span data-stu-id="edc27-234">c.</span></span> <span data-ttu-id="edc27-235">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="edc27-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="edc27-236">d.</span><span class="sxs-lookup"><span data-stu-id="edc27-236">d.</span></span> <span data-ttu-id="edc27-237">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="edc27-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="edc27-238">Créer un utilisateur de test Veracode</span><span class="sxs-lookup"><span data-stu-id="edc27-238">Create a Veracode test user</span></span>
<span data-ttu-id="edc27-239">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Veracode, vous devez les configurer dans Veracode.</span><span class="sxs-lookup"><span data-stu-id="edc27-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="edc27-240">Dans les cas de hello de Veracode, cette configuration est une tâche automatique.</span><span class="sxs-lookup"><span data-stu-id="edc27-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="edc27-241">Vous n’avez rien à faire.</span><span class="sxs-lookup"><span data-stu-id="edc27-241">There is no action item for you.</span></span> <span data-ttu-id="edc27-242">Les utilisateurs sont automatiquement créés si nécessaire pendant hello première seule tentative de connexion.</span><span class="sxs-lookup"><span data-stu-id="edc27-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="edc27-243">Vous pouvez utiliser n’importe quel autre Veracode utilisateur compte outil de création ou API fournie par Veracode tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edc27-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="edc27-244">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc27-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="edc27-245">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="edc27-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="edc27-247">**tooassign Britta Simon tooVeracode, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="edc27-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc27-248">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="edc27-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="edc27-250">Dans la liste des applications hello, sélectionnez **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="edc27-250">In hello applications list, select **Veracode**.</span></span>

    ![lien de Veracode Hello dans la liste des Applications hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="edc27-252">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="edc27-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="edc27-254">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="edc27-254">Click **Add** button.</span></span> <span data-ttu-id="edc27-255">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="edc27-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="edc27-257">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="edc27-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edc27-258">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="edc27-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edc27-259">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="edc27-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="edc27-260">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="edc27-260">Test single sign-on</span></span>

<span data-ttu-id="edc27-261">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="edc27-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="edc27-262">Lorsque vous cliquez sur mosaïque Veracode hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Veracode application.</span><span class="sxs-lookup"><span data-stu-id="edc27-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="edc27-263">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edc27-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="edc27-264">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="edc27-264">Additional resources</span></span>

* [<span data-ttu-id="edc27-265">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edc27-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edc27-266">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="edc27-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

