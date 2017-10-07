---
title: "Didacticiel : Intégration d’Azure Active Directory à Zoho | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="f56f7-103">Didacticiel : Intégration d’Azure Active Directory à Zoho</span><span class="sxs-lookup"><span data-stu-id="f56f7-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="f56f7-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zoho avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f56f7-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f56f7-105">Intégration Zoho à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f56f7-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f56f7-106">Vous pouvez contrôler dans Azure AD qui a accès tooZoho.</span><span class="sxs-lookup"><span data-stu-id="f56f7-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="f56f7-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZoho (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f56f7-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f56f7-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f56f7-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="f56f7-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f56f7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f56f7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f56f7-110">Prerequisites</span></span>

<span data-ttu-id="f56f7-111">intégration d’Azure AD avec Zoho de tooconfigure, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f56f7-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="f56f7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f56f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f56f7-113">Un abonnement Zoho pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f56f7-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f56f7-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f56f7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f56f7-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f56f7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f56f7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f56f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f56f7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f56f7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f56f7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f56f7-118">Scenario description</span></span>
<span data-ttu-id="f56f7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f56f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f56f7-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f56f7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f56f7-121">Ajout de Zoho à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f56f7-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="f56f7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f56f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="f56f7-123">Ajout de Zoho à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f56f7-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="f56f7-124">intégration de hello tooconfigure de Zoho dans Azure AD, vous devez tooadd Zoho à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f56f7-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f56f7-125">**tooadd Zoho à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f56f7-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f56f7-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f56f7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="f56f7-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f56f7-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="f56f7-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f56f7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="f56f7-133">Dans la zone de recherche de hello, tapez **Zoho**, sélectionnez **Zoho** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f56f7-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de Zoho Bonjour](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f56f7-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f56f7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f56f7-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zoho avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f56f7-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f56f7-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zoho est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f56f7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="f56f7-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zoho doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f56f7-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="f56f7-139">Dans Zoho, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f56f7-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f56f7-140">tooconfigure et test Azure AD l’authentification unique avec Zoho, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f56f7-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f56f7-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f56f7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f56f7-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f56f7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f56f7-143">**[Créer un utilisateur de test Zoho](#create-a-zoho-test-user)**  -toohave un équivalent de Britta Simon dans Zoho est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f56f7-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f56f7-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f56f7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f56f7-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f56f7-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f56f7-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f56f7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f56f7-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zoho.</span><span class="sxs-lookup"><span data-stu-id="f56f7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="f56f7-148">**tooconfigure Azure AD single sign-on avec Zoho, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f56f7-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="f56f7-149">Bonjour portail Azure, sur hello **Zoho** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="f56f7-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f56f7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="f56f7-153">Sur hello **Zoho domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f56f7-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="f56f7-155">a.</span><span class="sxs-lookup"><span data-stu-id="f56f7-155">a.</span></span> <span data-ttu-id="f56f7-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="f56f7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f56f7-157">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="f56f7-157">This value is not real.</span></span> <span data-ttu-id="f56f7-158">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="f56f7-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f56f7-159">Contact [équipe de support Client de Zoho](https://www.zoho.com/mail/contact.html) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="f56f7-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="f56f7-160">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f56f7-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="f56f7-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f56f7-162">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f56f7-164">Sur hello **Zoho Configuration** , cliquez sur **Zoho de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f56f7-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f56f7-165">Hello de copie **SAML Sign-On URL du Service unique, URL de modification du mot de passe et URL de déconnexion** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f56f7-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="f56f7-167">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zoho Mail en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f56f7-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="f56f7-168">Accédez toohello **le panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="f56f7-169">![Control Panel (Panneau de configuration)](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel (Panneau de configuration)")</span><span class="sxs-lookup"><span data-stu-id="f56f7-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="f56f7-170">Cliquez sur hello **l’authentification SAML** onglet.</span><span class="sxs-lookup"><span data-stu-id="f56f7-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="f56f7-171">![Authentification SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="f56f7-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="f56f7-172">Bonjour **détails de l’authentification SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f56f7-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f56f7-173">![Détails d’authentification SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Détails d’authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="f56f7-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="f56f7-174">a.</span><span class="sxs-lookup"><span data-stu-id="f56f7-174">a.</span></span> <span data-ttu-id="f56f7-175">Bonjour **URL de connexion** zone de texte, collez **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f56f7-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f56f7-176">b.</span><span class="sxs-lookup"><span data-stu-id="f56f7-176">b.</span></span> <span data-ttu-id="f56f7-177">Bonjour **URL de déconnexion** zone de texte, collez **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f56f7-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f56f7-178">c.</span><span class="sxs-lookup"><span data-stu-id="f56f7-178">c.</span></span> <span data-ttu-id="f56f7-179">Bonjour **URL de modification du mot de passe** zone de texte, collez **URL de modification du mot de passe** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f56f7-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="f56f7-180">d.</span><span class="sxs-lookup"><span data-stu-id="f56f7-180">d.</span></span> <span data-ttu-id="f56f7-181">Ouvrez votre certificat codé en base 64 téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **PublicKey** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="f56f7-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="f56f7-182">e.</span><span class="sxs-lookup"><span data-stu-id="f56f7-182">e.</span></span> <span data-ttu-id="f56f7-183">Comme **Algorithme**, sélectionnez **RSA**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="f56f7-184">f.</span><span class="sxs-lookup"><span data-stu-id="f56f7-184">f.</span></span> <span data-ttu-id="f56f7-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="f56f7-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f56f7-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f56f7-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f56f7-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f56f7-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f56f7-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f56f7-189">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f56f7-189">Create an Azure AD test user</span></span>

<span data-ttu-id="f56f7-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f56f7-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="f56f7-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f56f7-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f56f7-193">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="f56f7-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f56f7-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f56f7-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f56f7-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f56f7-199">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f56f7-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f56f7-201">a.</span><span class="sxs-lookup"><span data-stu-id="f56f7-201">a.</span></span> <span data-ttu-id="f56f7-202">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f56f7-203">b.</span><span class="sxs-lookup"><span data-stu-id="f56f7-203">b.</span></span> <span data-ttu-id="f56f7-204">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f56f7-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="f56f7-205">c.</span><span class="sxs-lookup"><span data-stu-id="f56f7-205">c.</span></span> <span data-ttu-id="f56f7-206">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="f56f7-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="f56f7-207">d.</span><span class="sxs-lookup"><span data-stu-id="f56f7-207">d.</span></span> <span data-ttu-id="f56f7-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="f56f7-209">Créer un utilisateur de test Zoho</span><span class="sxs-lookup"><span data-stu-id="f56f7-209">Create a Zoho test user</span></span>

<span data-ttu-id="f56f7-210">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Zoho Mail, vous devez les configurer dans Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="f56f7-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="f56f7-211">Dans les cas de hello de Zoho Mail, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="f56f7-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="f56f7-212">Vous pouvez utiliser n’importe quel autre Zoho Mail utilisateur compte outil de création ou API fournie par Zoho Mail tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="f56f7-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="f56f7-213">tooprovision un compte d’utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f56f7-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="f56f7-214">Connectez-vous à tooyour **Zoho Mail** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f56f7-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="f56f7-215">Accédez trop**le panneau de configuration \> de messagerie et de documents**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="f56f7-216">Accédez trop**détails de l’utilisateur \> ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="f56f7-217">![Ajouter un utilisateur](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="f56f7-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="f56f7-218">Sur hello **ajouter des utilisateurs** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f56f7-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="f56f7-219">![Ajouter un utilisateur](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="f56f7-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="f56f7-220">a.</span><span class="sxs-lookup"><span data-stu-id="f56f7-220">a.</span></span> <span data-ttu-id="f56f7-221">Bonjour **prénom** zone de texte, type hello premier nom d’utilisateur comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="f56f7-222">b.</span><span class="sxs-lookup"><span data-stu-id="f56f7-222">b.</span></span> <span data-ttu-id="f56f7-223">Bonjour **nom** zone de texte, type hello nom d’utilisateur comme **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="f56f7-224">c.</span><span class="sxs-lookup"><span data-stu-id="f56f7-224">c.</span></span> <span data-ttu-id="f56f7-225">Bonjour **ID de courrier électronique** zone de texte, id de courrier électronique de type hello d’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f56f7-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f56f7-226">d.</span><span class="sxs-lookup"><span data-stu-id="f56f7-226">d.</span></span> <span data-ttu-id="f56f7-227">Bonjour **mot de passe** zone de texte, entrez le mot de passe d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f56f7-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="f56f7-228">e.</span><span class="sxs-lookup"><span data-stu-id="f56f7-228">e.</span></span> <span data-ttu-id="f56f7-229">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="f56f7-230">titulaire du compte Azure Active Directory Hello recevra un e-mail avec un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="f56f7-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f56f7-231">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f56f7-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f56f7-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZoho.</span><span class="sxs-lookup"><span data-stu-id="f56f7-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="f56f7-234">**tooassign Britta Simon tooZoho, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f56f7-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="f56f7-235">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f56f7-237">Dans la liste des applications hello, sélectionnez **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-237">In hello applications list, select **Zoho**.</span></span>

    ![lien de Zoho Hello dans la liste des Applications hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="f56f7-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="f56f7-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-241">Click **Add** button.</span></span> <span data-ttu-id="f56f7-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="f56f7-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f56f7-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f56f7-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f56f7-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f56f7-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f56f7-247">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f56f7-247">Test single sign-on</span></span>

<span data-ttu-id="f56f7-248">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f56f7-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f56f7-249">Lorsque vous cliquez sur mosaïque Zoho hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Zoho application.</span><span class="sxs-lookup"><span data-stu-id="f56f7-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="f56f7-250">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f56f7-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f56f7-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f56f7-251">Additional resources</span></span>

* [<span data-ttu-id="f56f7-252">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f56f7-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f56f7-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f56f7-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

