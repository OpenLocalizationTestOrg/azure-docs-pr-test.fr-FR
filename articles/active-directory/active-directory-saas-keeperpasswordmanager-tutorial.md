---
title: "Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Gestionnaire de mots de passe détenteur & coffre numérique."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="309a6-103">Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="309a6-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="309a6-104">Dans ce didacticiel, vous apprendrez comment toointegrate Gestionnaire de mots de passe détenteur & numérique coffre auprès d’Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="309a6-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="309a6-105">Intégration de gestionnaire de mots de passe détenteur & numérique coffre auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="309a6-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="309a6-106">Vous pouvez contrôler dans Azure AD qui a accès tooKeeper Gestionnaire de mot de passe & coffre numérique</span><span class="sxs-lookup"><span data-stu-id="309a6-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="309a6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKeeper Gestionnaire de mot de passe et le coffre numérique (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="309a6-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="309a6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="309a6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="309a6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="309a6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="309a6-110">Prerequisites</span></span>

<span data-ttu-id="309a6-111">tooconfigure intégration d’Azure AD avec le Gestionnaire de mots de passe détenteur & coffre numérique, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="309a6-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="309a6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="309a6-113">Un abonnement Keeper Password Manager & Digital Vault pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="309a6-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="309a6-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="309a6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="309a6-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="309a6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="309a6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="309a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="309a6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="309a6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="309a6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="309a6-118">Scenario description</span></span>
<span data-ttu-id="309a6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="309a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="309a6-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="309a6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="309a6-121">Ajout du Gestionnaire de mots de passe détenteur & coffre numérique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="309a6-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="309a6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="309a6-123">Ajout du Gestionnaire de mots de passe détenteur & coffre numérique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="309a6-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="309a6-124">intégration de hello tooconfigure du Gestionnaire de mots de passe détenteur & coffre numérique dans Azure AD, vous devez tooadd Gestionnaire de mots de passe détenteur & coffre numérique à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="309a6-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="309a6-125">**tooadd Gestionnaire de mots de passe détenteur & coffre numérique à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="309a6-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="309a6-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="309a6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="309a6-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="309a6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="309a6-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="309a6-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="309a6-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="309a6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="309a6-133">Dans la zone de recherche de hello, tapez **Gestionnaire de mots de passe détenteur & coffre numérique**.</span><span class="sxs-lookup"><span data-stu-id="309a6-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="309a6-135">Dans le volet de résultats hello, sélectionnez **Gestionnaire de mots de passe détenteur & coffre numérique**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="309a6-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="309a6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="309a6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="309a6-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="309a6-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le Gestionnaire de mots de passe détenteur & coffre numérique est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="309a6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="309a6-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Gestionnaire de mots de passe détenteur & coffre numérique hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="309a6-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="309a6-141">Dans le Gestionnaire de mots de passe détenteur & coffre numérique, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="309a6-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="309a6-142">tooconfigure et test Azure AD l’authentification unique avec le Gestionnaire de mots de passe détenteur & coffre numérique, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="309a6-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="309a6-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="309a6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="309a6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="309a6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="309a6-145">**[Création d’un utilisateur de test de gestionnaire de mots de passe détenteur & coffre numérique](#creating-a-keeperpasswordmanager-test-user)**  -toohave un équivalent de Britta Simon dans le Gestionnaire de mots de passe détenteur & coffre numérique qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="309a6-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="309a6-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="309a6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="309a6-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="309a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="309a6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="309a6-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Gestionnaire de mots de passe détenteur & coffre numérique.</span><span class="sxs-lookup"><span data-stu-id="309a6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="309a6-150">**tooconfigure Azure AD l’authentification unique avec le Gestionnaire de mots de passe détenteur & coffre numérique, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="309a6-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="309a6-151">Bonjour portail Azure, sur hello **Gestionnaire de mots de passe détenteur & coffre numérique** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="309a6-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="309a6-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="309a6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="309a6-155">Sur hello **Gestionnaire de mots de passe détenteur & domaine coffre numérique et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="309a6-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="309a6-157">a.</span><span class="sxs-lookup"><span data-stu-id="309a6-157">a.</span></span> <span data-ttu-id="309a6-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="309a6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="309a6-159">b.</span><span class="sxs-lookup"><span data-stu-id="309a6-159">b.</span></span> <span data-ttu-id="309a6-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="309a6-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="309a6-161">c.</span><span class="sxs-lookup"><span data-stu-id="309a6-161">c.</span></span> <span data-ttu-id="309a6-162">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="309a6-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="309a6-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="309a6-163">These values are not real.</span></span> <span data-ttu-id="309a6-164">Mettre à jour ces valeurs avec l’URL de réponse réelle hello et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="309a6-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="309a6-165">Contact [équipe de support de gestionnaire de mots de passe détenteur & numérique coffre Client](https://keepersecurity.com/contact.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="309a6-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="309a6-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="309a6-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="309a6-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="309a6-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="309a6-170">Sur hello **Gestionnaire de mots de passe détenteur & Configuration coffre numérique** , cliquez sur **configurer le Gestionnaire de mot de passe détenteur & coffre numérique** tooopen **configurer l’authentification**fenêtre.</span><span class="sxs-lookup"><span data-stu-id="309a6-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="309a6-171">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="309a6-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="309a6-173">tooconfigure l’authentification unique sur **Gestionnaire de mots de passe détenteur & Configuration coffre numérique** côté, suivez les recommandations de hello à [Guide de prise en charge détenteur](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="309a6-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="309a6-174">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="309a6-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="309a6-175">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="309a6-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="309a6-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="309a6-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="309a6-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="309a6-178">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="309a6-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="309a6-180">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="309a6-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="309a6-181">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="309a6-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="309a6-183">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="309a6-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="309a6-185">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="309a6-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="309a6-187">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="309a6-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="309a6-189">a.</span><span class="sxs-lookup"><span data-stu-id="309a6-189">a.</span></span> <span data-ttu-id="309a6-190">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="309a6-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="309a6-191">b.</span><span class="sxs-lookup"><span data-stu-id="309a6-191">b.</span></span> <span data-ttu-id="309a6-192">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="309a6-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="309a6-193">c.</span><span class="sxs-lookup"><span data-stu-id="309a6-193">c.</span></span> <span data-ttu-id="309a6-194">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="309a6-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="309a6-195">d.</span><span class="sxs-lookup"><span data-stu-id="309a6-195">d.</span></span> <span data-ttu-id="309a6-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="309a6-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="309a6-197">Création d’un utilisateur de test Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="309a6-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="309a6-198">tooenable Azure AD les utilisateurs toolog dans tooKeeper Gestionnaire de mot de passe & coffre numérique, vous devez les configurer dans le Gestionnaire de mots de passe détenteur & coffre numérique.</span><span class="sxs-lookup"><span data-stu-id="309a6-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="309a6-199">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="309a6-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="309a6-200">Vous pouvez contacter [prise en charge détenteur](https://keepersecurity.com/contact.html), si vous souhaitez que les utilisateurs de toosetup manuellement.</span><span class="sxs-lookup"><span data-stu-id="309a6-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="309a6-201">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="309a6-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="309a6-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKeeper Gestionnaire de mot de passe & coffre numérique.</span><span class="sxs-lookup"><span data-stu-id="309a6-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="309a6-204">**tooassign Britta Simon tooKeeper Gestionnaire de mot de passe & coffre numérique, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="309a6-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="309a6-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="309a6-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="309a6-207">Dans la liste des applications hello, sélectionnez **Gestionnaire de mots de passe détenteur & coffre numérique**.</span><span class="sxs-lookup"><span data-stu-id="309a6-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="309a6-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="309a6-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="309a6-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="309a6-211">Click **Add** button.</span></span> <span data-ttu-id="309a6-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="309a6-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="309a6-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="309a6-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="309a6-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="309a6-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="309a6-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="309a6-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="309a6-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="309a6-217">Testing single sign-on</span></span>

<span data-ttu-id="309a6-218">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="309a6-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="309a6-219">Lorsque vous cliquez sur le Gestionnaire de mots de passe détenteur Bonjour vignette numérique coffre Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application Gestionnaire de mots de passe détenteur & coffre numérique.</span><span class="sxs-lookup"><span data-stu-id="309a6-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="309a6-220">Après une authentification réussie, vous devez obtenir dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="309a6-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="309a6-221">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="309a6-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="309a6-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="309a6-222">Additional resources</span></span>

* [<span data-ttu-id="309a6-223">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="309a6-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="309a6-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="309a6-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

