---
title: "Didacticiel : Intégration d’Azure Active Directory avec Litmos | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="5fbf9-103">Didacticiel : Intégration d’Azure Active Directory avec Litmos</span><span class="sxs-lookup"><span data-stu-id="5fbf9-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="5fbf9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Litmos avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fbf9-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fbf9-105">Intégration Litmos à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5fbf9-106">Vous pouvez contrôler dans Azure AD qui a accès tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="5fbf9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLitmos (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5fbf9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5fbf9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fbf9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fbf9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5fbf9-110">Prerequisites</span></span>

<span data-ttu-id="5fbf9-111">tooconfigure intégration d’Azure AD avec Litmos, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="5fbf9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fbf9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fbf9-113">Un abonnement Litmos pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5fbf9-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fbf9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fbf9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fbf9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fbf9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fbf9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fbf9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5fbf9-118">Scenario description</span></span>
<span data-ttu-id="5fbf9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fbf9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fbf9-121">Ajout de Litmos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5fbf9-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="5fbf9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fbf9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="5fbf9-123">Ajout de Litmos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5fbf9-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="5fbf9-124">intégration de hello tooconfigure de Litmos dans Azure AD, vous devez tooadd Litmos à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5fbf9-125">**tooadd Litmos à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fbf9-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fbf9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="5fbf9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5fbf9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="5fbf9-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="5fbf9-133">Dans la zone de recherche de hello, tapez **Litmos**, sélectionnez **Litmos** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos dans la liste des résultats hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5fbf9-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fbf9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5fbf9-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Litmos sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5fbf9-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fbf9-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Litmos est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="5fbf9-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Litmos doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="5fbf9-139">Dans Litmos, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5fbf9-140">tooconfigure et test Azure AD l’authentification unique avec Litmos, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5fbf9-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5fbf9-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fbf9-143">**[Créer un utilisateur de test Litmos](#create-a-litmos-test-user)**  -toohave un équivalent de Britta Simon dans Litmos est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fbf9-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fbf9-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5fbf9-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fbf9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5fbf9-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Litmos.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="5fbf9-148">**tooconfigure Azure AD single sign-on avec Litmos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fbf9-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fbf9-149">Bonjour portail Azure, sur hello **Litmos** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="5fbf9-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="5fbf9-153">Sur hello **Litmos domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="5fbf9-155">a.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-155">a.</span></span> <span data-ttu-id="5fbf9-156">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="5fbf9-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="5fbf9-157">b.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-157">b.</span></span> <span data-ttu-id="5fbf9-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="5fbf9-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fbf9-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-159">These values are not real.</span></span> <span data-ttu-id="5fbf9-160">Mettre à jour ces valeurs avec hello identificateur et réponse URL réelle, qui vous seront expliquées plus loin dans le didacticiel ou contactez [Litmos l’équipe de support](https://www.litmos.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="5fbf9-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="5fbf9-163">Dans le cadre de la configuration de hello, vous devez toocustomize hello **attributs du jeton SAML** pour votre application Litmos.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Section de l’attribut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="5fbf9-165">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="5fbf9-165">Attribute Name</span></span>   | <span data-ttu-id="5fbf9-166">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="5fbf9-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="5fbf9-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="5fbf9-167">FirstName</span></span> |<span data-ttu-id="5fbf9-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5fbf9-168">user.givenname</span></span> |
    | <span data-ttu-id="5fbf9-169">LastName</span><span class="sxs-lookup"><span data-stu-id="5fbf9-169">LastName</span></span>  |<span data-ttu-id="5fbf9-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="5fbf9-170">user.surname</span></span> |
    | <span data-ttu-id="5fbf9-171">Email</span><span class="sxs-lookup"><span data-stu-id="5fbf9-171">Email</span></span> |<span data-ttu-id="5fbf9-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="5fbf9-172">user.mail</span></span> |

    <span data-ttu-id="5fbf9-173">a.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-173">a.</span></span> <span data-ttu-id="5fbf9-174">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Ajouter un attribut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Boîte de dialogue Ajouter un attribut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5fbf9-177">b.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-177">b.</span></span> <span data-ttu-id="5fbf9-178">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="5fbf9-179">c.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-179">c.</span></span> <span data-ttu-id="5fbf9-180">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5fbf9-181">d.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-181">d.</span></span> <span data-ttu-id="5fbf9-182">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="5fbf9-183">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5fbf9-183">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5fbf9-185">Dans une autre fenêtre de navigateur, site d’entreprise Litmos tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="5fbf9-186">Dans la barre de navigation hello sur le côté gauche de hello, cliquez sur **comptes**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Section Comptes côté application][22] 

9. <span data-ttu-id="5fbf9-188">Cliquez sur hello **intégrations** onglet.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-188">Click hello **Integrations** tab.</span></span>
   
    ![Onglet Intégration][23] 

10. <span data-ttu-id="5fbf9-190">Sur hello **intégrations** onglet, faites défiler la liste trop**3e partie intégrations**, puis cliquez sur **SAML 2.0** onglet.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Section SAML 2.0][24] 

11. <span data-ttu-id="5fbf9-192">Copier la valeur hello sous **hello de point de terminaison SAML pour litmos est :** et collez-le dans hello **URL de réponse** textbox Bonjour **Litmos domaine et les URL** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Point de terminaison SAML][26] 

12. <span data-ttu-id="5fbf9-194">Dans votre **Litmos** application, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Application Litmos][25] 
     
     <span data-ttu-id="5fbf9-196">a.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-196">a.</span></span> <span data-ttu-id="5fbf9-197">Cliquez sur **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="5fbf9-198">b.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-198">b.</span></span> <span data-ttu-id="5fbf9-199">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509 de SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="5fbf9-200">c.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-200">c.</span></span> <span data-ttu-id="5fbf9-201">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5fbf9-202">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5fbf9-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5fbf9-203">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5fbf9-204">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fbf9-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5fbf9-205">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fbf9-205">Create an Azure AD test user</span></span>

<span data-ttu-id="5fbf9-206">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="5fbf9-208">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fbf9-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fbf9-209">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5fbf9-211">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5fbf9-213">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5fbf9-215">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fbf9-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5fbf9-217">a.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-217">a.</span></span> <span data-ttu-id="5fbf9-218">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fbf9-219">b.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-219">b.</span></span> <span data-ttu-id="5fbf9-220">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5fbf9-221">c.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-221">c.</span></span> <span data-ttu-id="5fbf9-222">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5fbf9-223">d.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-223">d.</span></span> <span data-ttu-id="5fbf9-224">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="5fbf9-225">Créer un utilisateur de test Litmos</span><span class="sxs-lookup"><span data-stu-id="5fbf9-225">Create a Litmos test user</span></span>

<span data-ttu-id="5fbf9-226">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Litmos.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="5fbf9-227">Hello Litmos application prend en charge juste-à-temps de configuration.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="5fbf9-228">Cela signifie que, un compte d’utilisateur est automatiquement créé les si nécessaire au cours d’une application de hello tooaccess tentative à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="5fbf9-229">**toocreate un utilisateur appelé Britta Simon dans Litmos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fbf9-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fbf9-230">Dans une autre fenêtre de navigateur, site d’entreprise Litmos tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="5fbf9-231">Dans la barre de navigation hello sur le côté gauche de hello, cliquez sur **comptes**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Section Comptes côté application][22] 

3. <span data-ttu-id="5fbf9-233">Cliquez sur hello **intégrations** onglet.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-233">Click hello **Integrations** tab.</span></span>
   
    ![Onglet Intégrations][23] 

4. <span data-ttu-id="5fbf9-235">Sur hello **intégrations** onglet, faites défiler la liste trop**3e partie intégrations**, puis cliquez sur **SAML 2.0** onglet.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="5fbf9-237">Sélectionner **Générer automatiquement les utilisateurs**</span><span class="sxs-lookup"><span data-stu-id="5fbf9-237">Select **Autogenerate Users**</span></span>
   
    ![Générer automatiquement les utilisateurs][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5fbf9-239">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fbf9-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5fbf9-240">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="5fbf9-242">**tooassign Britta Simon tooLitmos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fbf9-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fbf9-243">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5fbf9-245">Dans la liste des applications hello, sélectionnez **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-245">In hello applications list, select **Litmos**.</span></span>

    ![lien de Litmos Hello dans la liste des Applications hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="5fbf9-247">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="5fbf9-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-249">Click **Add** button.</span></span> <span data-ttu-id="5fbf9-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="5fbf9-252">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5fbf9-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fbf9-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5fbf9-255">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5fbf9-255">Test single sign-on</span></span>

<span data-ttu-id="5fbf9-256">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5fbf9-257">Lorsque vous cliquez sur hello Litmos vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Litmos application.</span><span class="sxs-lookup"><span data-stu-id="5fbf9-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5fbf9-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5fbf9-258">Additional resources</span></span>

* [<span data-ttu-id="5fbf9-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fbf9-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fbf9-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5fbf9-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

