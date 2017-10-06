---
title: "Didacticiel : Intégration d’Azure Active Directory dans Asana | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="4739c-103">Didacticiel : Intégration d’Azure Active Directory dans Asana</span><span class="sxs-lookup"><span data-stu-id="4739c-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="4739c-104">Dans ce didacticiel, vous apprendrez comment toointegrate Asana avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4739c-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4739c-105">Intégration Asana à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4739c-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4739c-106">Vous pouvez contrôler dans Azure AD qui a accès tooAsana</span><span class="sxs-lookup"><span data-stu-id="4739c-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="4739c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAsana (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4739c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4739c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4739c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4739c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4739c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4739c-110">Prerequisites</span></span>

<span data-ttu-id="4739c-111">tooconfigure intégration d’Azure AD avec Asana, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4739c-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="4739c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4739c-113">Un abonnement Asana avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="4739c-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4739c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4739c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4739c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4739c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4739c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4739c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4739c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4739c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4739c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4739c-118">Scenario description</span></span>
<span data-ttu-id="4739c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4739c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4739c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4739c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4739c-121">Ajout de Asana à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4739c-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="4739c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="4739c-123">Ajout de Asana à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4739c-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="4739c-124">intégration de hello tooconfigure de Asana dans Azure AD, vous devez tooadd Asana à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4739c-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4739c-125">**tooadd Asana à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4739c-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4739c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4739c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="4739c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4739c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4739c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4739c-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="4739c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4739c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="4739c-133">Dans la zone de recherche de hello, tapez **Asana**, sélectionnez **Asana** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4739c-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4739c-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4739c-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Asana, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4739c-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4739c-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Asana est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4739c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="4739c-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Asana doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4739c-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="4739c-139">Dans Asana, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4739c-140">tooconfigure et test Azure AD l’authentification unique avec Asana, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4739c-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4739c-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4739c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4739c-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4739c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4739c-143">**[Créer un utilisateur de test Asana](#create-an-asana-test-user)**  -toohave un équivalent de Britta Simon dans Asana est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4739c-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4739c-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4739c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4739c-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4739c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4739c-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4739c-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Asana.</span><span class="sxs-lookup"><span data-stu-id="4739c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="4739c-148">**tooconfigure Azure AD single sign-on avec Asana, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4739c-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="4739c-149">Bonjour portail Azure, sur hello **Asana** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4739c-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4739c-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4739c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="4739c-153">Sur hello **Asana domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4739c-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="4739c-155">a.</span><span class="sxs-lookup"><span data-stu-id="4739c-155">a.</span></span> <span data-ttu-id="4739c-156">Bonjour **URL de connexion** zone de texte, tapez l’URL :`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="4739c-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="4739c-157">b.</span><span class="sxs-lookup"><span data-stu-id="4739c-157">b.</span></span> <span data-ttu-id="4739c-158">Bonjour **identificateur** zone de texte, valeur de type :`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="4739c-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="4739c-159">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4739c-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="4739c-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4739c-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4739c-163">Sur hello **Asana Configuration** , cliquez sur **Asana de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4739c-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4739c-164">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4739c-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="4739c-166">Dans une autre fenêtre de navigateur, l’authentification tooyour Asana application.</span><span class="sxs-lookup"><span data-stu-id="4739c-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="4739c-167">tooconfigure SSO dans Asana, les paramètres d’espace de travail accès hello en cliquant sur le nom d’espace de travail hello sur hello coin supérieur droit de l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="4739c-168">Ensuite, cliquez sur le **\<nom de votre espace de travail\> Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="4739c-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Paramètre d’authentification unique Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="4739c-170">Sur hello **paramètres de l’organisation** fenêtre, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="4739c-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="4739c-171">Ensuite, cliquez sur **membres doivent se connecter via SAML** configuration de SSO tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="4739c-172">Hello effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4739c-172">hello perform hello following steps:</span></span>
   
    ![Configurer les paramètres d’authentification unique](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="4739c-174">a.</span><span class="sxs-lookup"><span data-stu-id="4739c-174">a.</span></span> <span data-ttu-id="4739c-175">Bonjour **URL de la page connexion** zone de texte, collez hello **SAML Sign-On URL du Service unique**.</span><span class="sxs-lookup"><span data-stu-id="4739c-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="4739c-176">b.</span><span class="sxs-lookup"><span data-stu-id="4739c-176">b.</span></span> <span data-ttu-id="4739c-177">Cliquez avec le bouton droit sur le certificat hello téléchargé à partir du portail Azure, puis ouvrir le fichier de certificat hello à l’aide du bloc-notes ou votre éditeur de texte préféré.</span><span class="sxs-lookup"><span data-stu-id="4739c-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="4739c-178">Copier le contenu entre hello hello commencer et hello titre de certificat de fin et le coller dans hello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4739c-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="4739c-179">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4739c-179">Click **Save**.</span></span> <span data-ttu-id="4739c-180">Accédez trop[guide Asana pour configurer l’authentification unique](https://asana.com/guide/help/premium/authentication#gl-saml) si vous avez besoin d’aide.</span><span class="sxs-lookup"><span data-stu-id="4739c-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="4739c-181">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4739c-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4739c-182">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4739c-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4739c-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4739c-184">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-184">Create an Azure AD test user</span></span>

<span data-ttu-id="4739c-185">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4739c-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="4739c-187">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4739c-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4739c-188">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4739c-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4739c-190">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4739c-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4739c-192">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4739c-194">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4739c-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4739c-196">a.</span><span class="sxs-lookup"><span data-stu-id="4739c-196">a.</span></span> <span data-ttu-id="4739c-197">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4739c-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4739c-198">b.</span><span class="sxs-lookup"><span data-stu-id="4739c-198">b.</span></span> <span data-ttu-id="4739c-199">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4739c-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4739c-200">c.</span><span class="sxs-lookup"><span data-stu-id="4739c-200">c.</span></span> <span data-ttu-id="4739c-201">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4739c-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4739c-202">d.</span><span class="sxs-lookup"><span data-stu-id="4739c-202">d.</span></span> <span data-ttu-id="4739c-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4739c-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="4739c-204">Créer un utilisateur de test Asana</span><span class="sxs-lookup"><span data-stu-id="4739c-204">Create an Asana test user</span></span>

<span data-ttu-id="4739c-205">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Asana.</span><span class="sxs-lookup"><span data-stu-id="4739c-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="4739c-206">Sur **Asana**, accédez toohello **équipes** section sur le panneau gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="4739c-207">Cliquez sur hello ainsi que le bouton de connexion.</span><span class="sxs-lookup"><span data-stu-id="4739c-207">Click hello plus sign button.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="4739c-209">Tapez par courrier électronique hello britta.simon@contoso.com dans hello de zone de texte, puis sélectionnez **inviter**.</span><span class="sxs-lookup"><span data-stu-id="4739c-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="4739c-210">Cliquez sur **Send Invite**(Envoyer l’invitation).</span><span class="sxs-lookup"><span data-stu-id="4739c-210">Click **Send Invite**.</span></span> <span data-ttu-id="4739c-211">nouvel utilisateur de Hello recevront un message électronique dans son compte de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4739c-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="4739c-212">Elle sera peut-être toocreate et valider le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4739c-213">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4739c-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4739c-214">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAsana.</span><span class="sxs-lookup"><span data-stu-id="4739c-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Attribuer le rôle d’utilisateur hello][200]

<span data-ttu-id="4739c-216">**tooassign Britta Simon tooAsana, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4739c-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="4739c-217">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4739c-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4739c-219">Dans la liste des applications hello, sélectionnez **Asana**.</span><span class="sxs-lookup"><span data-stu-id="4739c-219">In hello applications list, select **Asana**.</span></span>

    ![lien de Asana Hello dans la liste des Applications hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="4739c-221">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4739c-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="4739c-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4739c-223">Click **Add** button.</span></span> <span data-ttu-id="4739c-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4739c-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="4739c-226">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4739c-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4739c-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4739c-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4739c-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4739c-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4739c-229">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4739c-229">Test single sign-on</span></span>

<span data-ttu-id="4739c-230">objectif Hello de cette section est tootest votre Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4739c-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="4739c-231">Atteindre la page de connexion tooAsana.</span><span class="sxs-lookup"><span data-stu-id="4739c-231">Go tooAsana login page.</span></span> <span data-ttu-id="4739c-232">Dans la zone de texte adresse de messagerie hello, insérer l’adresse de messagerie hello britta.simon@contoso.com. Zone de texte de mot de passe hello vides et cliquez sur **journal dans**.</span><span class="sxs-lookup"><span data-stu-id="4739c-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="4739c-233">Vous serez redirigé tooAzure AD de page de connexion.</span><span class="sxs-lookup"><span data-stu-id="4739c-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="4739c-234">Entrez vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4739c-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="4739c-235">Vous êtes maintenant connecté à Asana.</span><span class="sxs-lookup"><span data-stu-id="4739c-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4739c-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4739c-236">Additional resources</span></span>

* [<span data-ttu-id="4739c-237">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4739c-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4739c-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4739c-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
