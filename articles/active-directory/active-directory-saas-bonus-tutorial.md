---
title: "Didacticiel : Intégration d’Azure Active Directory avec Bonusly | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="e3317-103">Didacticiel : Intégration d’Azure Active Directory avec Bonusly</span><span class="sxs-lookup"><span data-stu-id="e3317-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="e3317-104">Dans ce didacticiel, vous apprendrez comment toointegrate Bonusly avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3317-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3317-105">Intégration Bonusly à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e3317-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e3317-106">Vous pouvez contrôler dans Azure AD qui a accès tooBonusly</span><span class="sxs-lookup"><span data-stu-id="e3317-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="e3317-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBonusly (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3317-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e3317-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e3317-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3317-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3317-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3317-110">Prerequisites</span></span>

<span data-ttu-id="e3317-111">tooconfigure intégration d’Azure AD avec Bonusly, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e3317-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="e3317-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3317-113">Un abonnement Bonusly pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e3317-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3317-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e3317-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3317-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e3317-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3317-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e3317-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3317-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3317-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3317-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e3317-118">Scenario description</span></span>
<span data-ttu-id="e3317-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e3317-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3317-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e3317-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3317-121">Ajout de Bonusly à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3317-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="e3317-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="e3317-123">Ajout de Bonusly à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3317-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="e3317-124">intégration de hello tooconfigure de Bonusly dans Azure AD, vous devez tooadd Bonusly à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e3317-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e3317-125">**tooadd Bonusly à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3317-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3317-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3317-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="e3317-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e3317-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e3317-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3317-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="e3317-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3317-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="e3317-133">Dans la zone de recherche de hello, tapez **Bonusly**, sélectionnez **Bonusly** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3317-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bonusly dans la liste des résultats hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e3317-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e3317-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bonusly avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e3317-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3317-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Bonusly est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3317-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="e3317-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Bonusly doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e3317-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="e3317-139">Dans Bonusly, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e3317-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e3317-140">tooconfigure et test Azure AD l’authentification unique avec Bonusly, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e3317-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e3317-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e3317-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e3317-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3317-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3317-143">**[Créer un utilisateur test Bonusly](#create-a-bonusly-test-user)**  -toohave un équivalent de Britta Simon dans Bonusly est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3317-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3317-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3317-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3317-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e3317-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e3317-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e3317-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Bonusly.</span><span class="sxs-lookup"><span data-stu-id="e3317-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="e3317-148">**tooconfigure Azure AD single sign-on avec Bonusly, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3317-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3317-149">Bonjour portail Azure, sur hello **Bonusly** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e3317-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e3317-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3317-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="e3317-153">Sur hello **Bonusly de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3317-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="e3317-155">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="e3317-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3317-156">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="e3317-156">hello value is not real.</span></span> <span data-ttu-id="e3317-157">Valeur de hello de mise à jour avec hello URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="e3317-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="e3317-158">Contact [équipe de support Bonusly](https://Bonusly/contact) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="e3317-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="e3317-159">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur à partir du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="e3317-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="e3317-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e3317-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3317-163">Sur hello **Configuration Bonusly** , cliquez sur **configurer Bonusly** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3317-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e3317-164">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e3317-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="e3317-166">Dans une autre fenêtre de navigateur, connectez-vous tooyour **Bonusly** client.</span><span class="sxs-lookup"><span data-stu-id="e3317-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="e3317-167">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis sélectionnez **intégrations et applications**.</span><span class="sxs-lookup"><span data-stu-id="e3317-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="e3317-168">![Section sociale Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="e3317-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="e3317-169">Sous **Single Sign-On**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e3317-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="e3317-170">Sur hello **SAML** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3317-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3317-171">![Page de boîte de dialogue Saml Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="e3317-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="e3317-172">a.</span><span class="sxs-lookup"><span data-stu-id="e3317-172">a.</span></span> <span data-ttu-id="e3317-173">Bonjour **URL cible de l’authentification unique IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3317-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e3317-174">b.</span><span class="sxs-lookup"><span data-stu-id="e3317-174">b.</span></span> <span data-ttu-id="e3317-175">Bonjour **émetteur IdP** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3317-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="e3317-176">c.</span><span class="sxs-lookup"><span data-stu-id="e3317-176">c.</span></span> <span data-ttu-id="e3317-177">Bonjour **URL de connexion IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3317-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e3317-178">d.</span><span class="sxs-lookup"><span data-stu-id="e3317-178">d.</span></span> <span data-ttu-id="e3317-179">Coller le **l’empreinte numérique** valeur copiée à partir du portail Azure dans hello **empreinte numérique du certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e3317-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="e3317-180">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e3317-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e3317-181">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e3317-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e3317-182">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e3317-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e3317-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3317-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e3317-184">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-184">Create an Azure AD test user</span></span>
<span data-ttu-id="e3317-185">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e3317-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="e3317-187">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3317-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3317-188">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3317-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3317-190">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e3317-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3317-192">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e3317-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3317-194">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3317-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3317-196">a.</span><span class="sxs-lookup"><span data-stu-id="e3317-196">a.</span></span> <span data-ttu-id="e3317-197">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3317-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3317-198">b.</span><span class="sxs-lookup"><span data-stu-id="e3317-198">b.</span></span> <span data-ttu-id="e3317-199">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e3317-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3317-200">c.</span><span class="sxs-lookup"><span data-stu-id="e3317-200">c.</span></span> <span data-ttu-id="e3317-201">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e3317-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e3317-202">d.</span><span class="sxs-lookup"><span data-stu-id="e3317-202">d.</span></span> <span data-ttu-id="e3317-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3317-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="e3317-204">Création d’un utilisateur de test Bonusly</span><span class="sxs-lookup"><span data-stu-id="e3317-204">Create a Bonusly test user</span></span>

<span data-ttu-id="e3317-205">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooBonusly, ils doivent être configurés dans Bonusly.</span><span class="sxs-lookup"><span data-stu-id="e3317-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="e3317-206">Dans les cas de hello de Bonusly, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e3317-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e3317-207">Vous pouvez utiliser n’importe quel autre outil de création de compte utilisateur Bonusly ou API fournie par tooprovision Bonusly AAD comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3317-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="e3317-208">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3317-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3317-209">Dans une fenêtre de navigateur web, ouvrez une session de client de Bonusly tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3317-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="e3317-210">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="e3317-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="e3317-211">![Paramètres](./media/active-directory-saas-bonus-tutorial/ic781041.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="e3317-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="e3317-212">Cliquez sur hello **utilisateurs et bonus** onglet.</span><span class="sxs-lookup"><span data-stu-id="e3317-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="e3317-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span><span class="sxs-lookup"><span data-stu-id="e3317-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="e3317-214">Cliquez sur **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="e3317-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="e3317-215">![Gestion des utilisateurs](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="e3317-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="e3317-216">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e3317-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="e3317-217">![Ajouter un utilisateur](./media/active-directory-saas-bonus-tutorial/ic781044.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="e3317-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="e3317-218">Sur hello **ajouter un utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3317-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3317-219">![Ajouter un utilisateur](./media/active-directory-saas-bonus-tutorial/ic781045.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="e3317-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="e3317-220">a.</span><span class="sxs-lookup"><span data-stu-id="e3317-220">a.</span></span> <span data-ttu-id="e3317-221">Bonjour **prénom** zone de texte, entrez hello premier nom d’utilisateur comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="e3317-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="e3317-222">b.</span><span class="sxs-lookup"><span data-stu-id="e3317-222">b.</span></span> <span data-ttu-id="e3317-223">Bonjour **nom** zone de texte, entrez le nom d’utilisateur comme hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e3317-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="e3317-224">c.</span><span class="sxs-lookup"><span data-stu-id="e3317-224">c.</span></span> <span data-ttu-id="e3317-225">Bonjour **messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e3317-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e3317-226">d.</span><span class="sxs-lookup"><span data-stu-id="e3317-226">d.</span></span> <span data-ttu-id="e3317-227">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e3317-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="e3317-228">titulaire du compte Azure AD Hello reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="e3317-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e3317-229">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3317-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e3317-230">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBonusly.</span><span class="sxs-lookup"><span data-stu-id="e3317-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="e3317-232">**tooassign Britta Simon tooBonusly, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3317-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3317-233">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3317-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e3317-235">Dans la liste des applications hello, sélectionnez **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="e3317-235">In hello applications list, select **Bonusly**.</span></span>

    ![Hello Bonusly lien dans la liste des Applications hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="e3317-237">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3317-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="e3317-239">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e3317-239">Click **Add** button.</span></span> <span data-ttu-id="e3317-240">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3317-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="e3317-242">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e3317-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e3317-243">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3317-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3317-244">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3317-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e3317-245">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e3317-245">Test single sign-on</span></span>

<span data-ttu-id="e3317-246">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e3317-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e3317-247">Lorsque vous cliquez sur la vignette de Bonusly hello dans hello volet d’accès, vous devez obtenir les applications Bonusly tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="e3317-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3317-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e3317-248">Additional resources</span></span>

* [<span data-ttu-id="e3317-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3317-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3317-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e3317-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

