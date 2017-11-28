---
title: "Didacticiel : Intégration d’Azure Active Directory à Peoplecart | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 481c7246a63f669ab39cb4ec652cebf40ba35f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="031c3-103">Didacticiel : Intégration d’Azure Active Directory à Peoplecart</span><span class="sxs-lookup"><span data-stu-id="031c3-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="031c3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Peoplecart avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="031c3-104">In this tutorial, you learn how toointegrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="031c3-105">Intégration Peoplecart à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="031c3-105">Integrating Peoplecart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="031c3-106">Vous pouvez contrôler dans Azure AD qui a accès tooPeoplecart</span><span class="sxs-lookup"><span data-stu-id="031c3-106">You can control in Azure AD who has access tooPeoplecart</span></span>
- <span data-ttu-id="031c3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPeoplecart (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-107">You can enable your users tooautomatically get signed-on tooPeoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="031c3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="031c3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="031c3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="031c3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="031c3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="031c3-110">Prerequisites</span></span>

<span data-ttu-id="031c3-111">tooconfigure intégration d’Azure AD avec Peoplecart, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="031c3-111">tooconfigure Azure AD integration with Peoplecart, you need hello following items:</span></span>

- <span data-ttu-id="031c3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="031c3-113">Un abonnement Peoplecart pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="031c3-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="031c3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="031c3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="031c3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="031c3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="031c3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="031c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="031c3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="031c3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="031c3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="031c3-118">Scenario description</span></span>
<span data-ttu-id="031c3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="031c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="031c3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="031c3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="031c3-121">Ajout de Peoplecart à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="031c3-121">Adding Peoplecart from hello gallery</span></span>
2. <span data-ttu-id="031c3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-hello-gallery"></a><span data-ttu-id="031c3-123">Ajout de Peoplecart à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="031c3-123">Adding Peoplecart from hello gallery</span></span>
<span data-ttu-id="031c3-124">intégration de hello tooconfigure de Peoplecart dans Azure AD, vous devez tooadd Peoplecart à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="031c3-124">tooconfigure hello integration of Peoplecart into Azure AD, you need tooadd Peoplecart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="031c3-125">**tooadd Peoplecart à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="031c3-125">**tooadd Peoplecart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="031c3-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="031c3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="031c3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="031c3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="031c3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="031c3-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="031c3-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="031c3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="031c3-133">Dans la zone de recherche de hello, tapez **Peoplecart**, sélectionnez **Peoplecart** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="031c3-133">In hello search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Peoplecart dans la liste des résultats hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="031c3-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="031c3-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Peoplecart avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="031c3-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="031c3-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Peoplecart est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="031c3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Peoplecart is tooa user in Azure AD.</span></span> <span data-ttu-id="031c3-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Peoplecart doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="031c3-138">In other words, a link relationship between an Azure AD user and hello related user in Peoplecart needs toobe established.</span></span>

<span data-ttu-id="031c3-139">Dans Peoplecart, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="031c3-139">In Peoplecart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="031c3-140">tooconfigure et test Azure AD l’authentification unique avec Peoplecart, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="031c3-140">tooconfigure and test Azure AD single sign-on with Peoplecart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="031c3-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="031c3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="031c3-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="031c3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="031c3-143">**[Créer un utilisateur de test Peoplecart](#create-a-peoplecart-test-user)**  -toohave un équivalent de Britta Simon dans Peoplecart est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="031c3-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - toohave a counterpart of Britta Simon in Peoplecart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="031c3-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="031c3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="031c3-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="031c3-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="031c3-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="031c3-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="031c3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="031c3-148">**tooconfigure Azure AD single sign-on avec Peoplecart, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="031c3-148">**tooconfigure Azure AD single sign-on with Peoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="031c3-149">Bonjour portail Azure, sur hello **Peoplecart** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="031c3-149">In hello Azure portal, on hello **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="031c3-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="031c3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="031c3-153">Sur hello **Peoplecart domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="031c3-153">On hello **Peoplecart Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="031c3-155">a.</span><span class="sxs-lookup"><span data-stu-id="031c3-155">a.</span></span> <span data-ttu-id="031c3-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="031c3-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="031c3-157">b.</span><span class="sxs-lookup"><span data-stu-id="031c3-157">b.</span></span> <span data-ttu-id="031c3-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="031c3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="031c3-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="031c3-159">These values are not real.</span></span> <span data-ttu-id="031c3-160">Mettre à jour ces valeurs avec hello Sign-On URL réelle et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="031c3-160">Update these values with hello actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="031c3-161">Contact [équipe de support Client de Peoplecart](https://peoplecart.com/ContactUs.aspx) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="031c3-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) tooget these values.</span></span> 
 
4. <span data-ttu-id="031c3-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="031c3-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="031c3-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="031c3-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="031c3-166">Sur hello **Peoplecart Configuration** , cliquez sur **Peoplecart de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="031c3-166">On hello **Peoplecart Configuration** section, click **Configure Peoplecart** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="031c3-167">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="031c3-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="031c3-169">tooconfigure l’authentification unique sur **Peoplecart** côté, vous devez hello toosend téléchargé **Metadata XML** et **SAML Sign-On URL du Service unique** trop[ Équipe de support Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="031c3-169">tooconfigure single sign-on on **Peoplecart** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="031c3-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="031c3-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="031c3-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="031c3-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="031c3-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="031c3-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="031c3-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="031c3-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="031c3-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-174">Create an Azure AD test user</span></span>
<span data-ttu-id="031c3-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="031c3-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="031c3-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="031c3-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="031c3-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="031c3-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="031c3-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="031c3-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="031c3-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="031c3-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="031c3-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="031c3-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="031c3-186">a.</span><span class="sxs-lookup"><span data-stu-id="031c3-186">a.</span></span> <span data-ttu-id="031c3-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="031c3-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="031c3-188">b.</span><span class="sxs-lookup"><span data-stu-id="031c3-188">b.</span></span> <span data-ttu-id="031c3-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="031c3-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="031c3-190">c.</span><span class="sxs-lookup"><span data-stu-id="031c3-190">c.</span></span> <span data-ttu-id="031c3-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="031c3-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="031c3-192">d.</span><span class="sxs-lookup"><span data-stu-id="031c3-192">d.</span></span> <span data-ttu-id="031c3-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="031c3-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="031c3-194">Créer un utilisateur de test Peoplecart</span><span class="sxs-lookup"><span data-stu-id="031c3-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="031c3-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="031c3-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="031c3-196">Travailler avec [équipe de support Peoplecart](https://peoplecart.com/ContactUs.aspx) tooadd les utilisateurs de hello dans la plateforme de Peoplecart hello.</span><span class="sxs-lookup"><span data-stu-id="031c3-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) tooadd hello users in hello Peoplecart platform.</span></span> <span data-ttu-id="031c3-197">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="031c3-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="031c3-198">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="031c3-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="031c3-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPeoplecart.</span><span class="sxs-lookup"><span data-stu-id="031c3-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeoplecart.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="031c3-201">**tooassign Britta Simon tooPeoplecart, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="031c3-201">**tooassign Britta Simon tooPeoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="031c3-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="031c3-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="031c3-204">Dans la liste des applications hello, sélectionnez **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="031c3-204">In hello applications list, select **Peoplecart**.</span></span>

    ![lien de Peoplecart Hello dans la liste des Applications hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="031c3-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="031c3-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="031c3-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="031c3-208">Click **Add** button.</span></span> <span data-ttu-id="031c3-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="031c3-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="031c3-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="031c3-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="031c3-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="031c3-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="031c3-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="031c3-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="031c3-214">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="031c3-214">Test single sign-on</span></span>

<span data-ttu-id="031c3-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="031c3-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="031c3-216">Lorsque vous cliquez sur mosaïque Peoplecart hello hello volet d’accès, vous devez obtenir la page de connexion de l’application de Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="031c3-216">When you click hello Peoplecart tile in hello Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="031c3-217">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="031c3-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="031c3-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="031c3-218">Additional resources</span></span>

* [<span data-ttu-id="031c3-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="031c3-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="031c3-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="031c3-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

