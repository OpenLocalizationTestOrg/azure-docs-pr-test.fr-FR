---
title: "Didacticiel : intégration d’Azure Active Directory à ICIMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="64757-103">Didacticiel : intégration d’Azure Active Directory à ICIMS</span><span class="sxs-lookup"><span data-stu-id="64757-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="64757-104">Dans ce didacticiel, vous apprendrez comment toointegrate ICIMS avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64757-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64757-105">Intégration ICIMS à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="64757-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64757-106">Vous pouvez contrôler dans Azure AD qui a accès tooICIMS</span><span class="sxs-lookup"><span data-stu-id="64757-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="64757-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooICIMS (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64757-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="64757-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="64757-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64757-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64757-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64757-110">Prerequisites</span></span>

<span data-ttu-id="64757-111">tooconfigure intégration d’Azure AD avec ICIMS, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="64757-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="64757-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64757-113">Un abonnement ICIMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="64757-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64757-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="64757-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64757-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="64757-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64757-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="64757-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64757-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64757-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64757-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="64757-118">Scenario description</span></span>
<span data-ttu-id="64757-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="64757-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64757-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="64757-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64757-121">Ajout de ICIMS à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="64757-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="64757-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="64757-123">Ajout de ICIMS à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="64757-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="64757-124">intégration de hello tooconfigure de ICIMS dans Azure AD, vous devez tooadd ICIMS à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="64757-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64757-125">**tooadd ICIMS à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64757-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64757-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="64757-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="64757-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="64757-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64757-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="64757-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="64757-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="64757-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="64757-133">Dans la zone de recherche de hello, tapez **ICIMS**, sélectionnez **ICIMS** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="64757-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS dans la liste des résultats hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="64757-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="64757-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ICIMS, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="64757-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64757-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ICIMS est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64757-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="64757-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ICIMS doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="64757-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="64757-139">Dans ICIMS, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="64757-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64757-140">tooconfigure et test Azure AD l’authentification unique avec ICIMS, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="64757-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64757-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="64757-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64757-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64757-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64757-143">**[Créer un utilisateur de test ICIMS](#create-an-icims-test-user)**  -toohave un équivalent de Britta Simon dans ICIMS est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="64757-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64757-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="64757-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64757-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="64757-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="64757-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="64757-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64757-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="64757-148">**tooconfigure Azure AD single sign-on avec ICIMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64757-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="64757-149">Bonjour portail Azure, sur hello **ICIMS** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="64757-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="64757-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="64757-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="64757-153">Sur hello **ICIMS domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="64757-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans ICIMS Domain and URLs (Domaine et URL ICIMS)](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="64757-155">a.</span><span class="sxs-lookup"><span data-stu-id="64757-155">a.</span></span> <span data-ttu-id="64757-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="64757-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="64757-157">b.</span><span class="sxs-lookup"><span data-stu-id="64757-157">b.</span></span> <span data-ttu-id="64757-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="64757-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64757-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="64757-159">These values are not real.</span></span> <span data-ttu-id="64757-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="64757-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="64757-161">Contact [équipe de support Client de ICIMS](https://www.icims.com/contact-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="64757-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="64757-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="64757-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="64757-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="64757-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64757-166">Sur hello **ICIMS Configuration** , cliquez sur **ICIMS de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="64757-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="64757-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="64757-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="64757-169">tooconfigure l’authentification unique sur **ICIMS** côté, vous devez hello toosend téléchargé **Metadata XML**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop [ICIMS l’équipe de support](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="64757-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="64757-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="64757-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="64757-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="64757-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64757-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="64757-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64757-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64757-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="64757-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-174">Create an Azure AD test user</span></span>
<span data-ttu-id="64757-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="64757-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="64757-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64757-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64757-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="64757-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64757-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="64757-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64757-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="64757-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64757-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="64757-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64757-186">a.</span><span class="sxs-lookup"><span data-stu-id="64757-186">a.</span></span> <span data-ttu-id="64757-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64757-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64757-188">b.</span><span class="sxs-lookup"><span data-stu-id="64757-188">b.</span></span> <span data-ttu-id="64757-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="64757-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64757-190">c.</span><span class="sxs-lookup"><span data-stu-id="64757-190">c.</span></span> <span data-ttu-id="64757-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="64757-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="64757-192">d.</span><span class="sxs-lookup"><span data-stu-id="64757-192">d.</span></span> <span data-ttu-id="64757-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="64757-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="64757-194">Créer un utilisateur de test ICIMS</span><span class="sxs-lookup"><span data-stu-id="64757-194">Create an ICIMS test user</span></span>

<span data-ttu-id="64757-195">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64757-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="64757-196">Travailler avec [ICIMS l’équipe de support](https://www.icims.com/contact-us) utilisateurs hello tooadd hello compte ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64757-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="64757-197">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="64757-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="64757-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooICIMS.</span><span class="sxs-lookup"><span data-stu-id="64757-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Attribuer le rôle d’utilisateur hello][200]

<span data-ttu-id="64757-200">**tooassign Britta Simon tooICIMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64757-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="64757-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="64757-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="64757-203">Dans la liste des applications hello, sélectionnez **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="64757-203">In hello applications list, select **ICIMS**.</span></span>

    ![lien ICIMS Hello dans la liste des Applications hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="64757-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="64757-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="64757-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64757-207">Click **Add** button.</span></span> <span data-ttu-id="64757-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="64757-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="64757-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="64757-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64757-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="64757-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64757-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="64757-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="64757-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="64757-213">Test single sign-on</span></span>

<span data-ttu-id="64757-214">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="64757-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="64757-215">Lorsque vous cliquez sur hello ICIMS vignette dans le volet d’accès de hello, vous devez obtenir l’application de ICIMS tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="64757-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64757-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="64757-216">Additional resources</span></span>

* [<span data-ttu-id="64757-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64757-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64757-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="64757-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

