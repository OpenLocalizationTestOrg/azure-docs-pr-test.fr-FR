---
title: "Didacticiel : Intégration d’Azure Active Directory avec Voyance | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="37dab-103">Didacticiel : Intégration d’Azure Active Directory à Voyance</span><span class="sxs-lookup"><span data-stu-id="37dab-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="37dab-104">Dans ce didacticiel, vous apprendrez comment toointegrate Voyance avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37dab-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37dab-105">Intégration Voyance à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="37dab-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="37dab-106">Vous pouvez contrôler dans Azure AD qui a accès tooVoyance</span><span class="sxs-lookup"><span data-stu-id="37dab-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="37dab-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooVoyance (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37dab-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="37dab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="37dab-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37dab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37dab-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37dab-110">Prerequisites</span></span>

<span data-ttu-id="37dab-111">tooconfigure intégration d’Azure AD avec Voyance, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="37dab-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="37dab-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37dab-113">Un abonnement Voyance pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="37dab-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37dab-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="37dab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37dab-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="37dab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37dab-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="37dab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37dab-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37dab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37dab-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="37dab-118">Scenario description</span></span>
<span data-ttu-id="37dab-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="37dab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37dab-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="37dab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37dab-121">Ajout de Voyance à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="37dab-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="37dab-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="37dab-123">Ajout de Voyance à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="37dab-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="37dab-124">intégration de hello tooconfigure de Voyance dans Azure AD, vous devez tooadd Voyance à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="37dab-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37dab-125">**tooadd Voyance à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37dab-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37dab-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="37dab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="37dab-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="37dab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="37dab-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37dab-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="37dab-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="37dab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="37dab-133">Dans la zone de recherche de hello, tapez **Voyance**, sélectionnez **Voyance** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="37dab-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance dans la liste des résultats hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="37dab-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="37dab-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Voyance avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="37dab-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37dab-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Voyance est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37dab-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="37dab-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Voyance doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="37dab-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="37dab-139">Dans Voyance, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="37dab-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="37dab-140">tooconfigure et test Azure AD l’authentification unique avec Voyance, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="37dab-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37dab-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="37dab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37dab-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37dab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37dab-143">**[Créer un utilisateur de test Voyance](#create-a-voyance-test-user)**  -toohave un équivalent de Britta Simon dans Voyance est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="37dab-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="37dab-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37dab-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37dab-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="37dab-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="37dab-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="37dab-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Voyance.</span><span class="sxs-lookup"><span data-stu-id="37dab-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="37dab-148">**tooconfigure Azure AD single sign-on avec Voyance, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37dab-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="37dab-149">Bonjour portail Azure, sur hello **Voyance** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="37dab-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="37dab-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37dab-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="37dab-153">Sur hello **Voyance domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="37dab-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Voyance pour IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="37dab-155">a.</span><span class="sxs-lookup"><span data-stu-id="37dab-155">a.</span></span> <span data-ttu-id="37dab-156">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="37dab-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="37dab-157">b.</span><span class="sxs-lookup"><span data-stu-id="37dab-157">b.</span></span> <span data-ttu-id="37dab-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="37dab-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="37dab-159">Vérifiez **afficher les paramètres d’URL avancés** et effectuer hello suivant l’étape si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="37dab-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Voyance pour SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="37dab-161">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="37dab-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="37dab-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="37dab-162">These values are not real.</span></span> <span data-ttu-id="37dab-163">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="37dab-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="37dab-164">Contact [équipe de support Client de Voyance](mailto:support@nyansa.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="37dab-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="37dab-165">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="37dab-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="37dab-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="37dab-167">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="37dab-169">Sur hello **Voyance Configuration** , cliquez sur **Voyance de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="37dab-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="37dab-170">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="37dab-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="37dab-172">Dans une fenêtre de navigateur web, client de Voyance tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="37dab-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="37dab-173">Toohello coin supérieur droit de la barre de navigation hello, cliquez sur hello déroulante indiquant que «**Acme University**».</span><span class="sxs-lookup"><span data-stu-id="37dab-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Configurer l’authentification unique côté application - Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="37dab-175">Cliquez sur **Paramètres d’administration**.</span><span class="sxs-lookup"><span data-stu-id="37dab-175">Click "**Admin Settings**".</span></span>

    ![Configurer l’authentification unique côté application - Paramètres d’administration](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="37dab-177">Cliquez sur l’onglet **Accès utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="37dab-177">Click "**User Access**" tab.</span></span>

    ![Configurer l’authentification unique côté application - Accès utilisateur](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="37dab-179">Cliquez sur hello »**SSO est désactivé**« bouton tooconfigure Azure AD en tant qu’un IdP à l’aide de SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="37dab-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurer l’authentification unique côté application - Bouton SSO désactivée](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="37dab-181">Accédez trop**SAML v2** section et suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="37dab-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Configurer l’authentification unique côté application - SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="37dab-183">a.</span><span class="sxs-lookup"><span data-stu-id="37dab-183">a.</span></span> <span data-ttu-id="37dab-184">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="37dab-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="37dab-185">b.</span><span class="sxs-lookup"><span data-stu-id="37dab-185">b.</span></span> <span data-ttu-id="37dab-186">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL de connexion IdP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="37dab-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="37dab-187">c.</span><span class="sxs-lookup"><span data-stu-id="37dab-187">c.</span></span> <span data-ttu-id="37dab-188">Ouvrez votre certificat codé en Base64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **IdP Cert** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="37dab-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="37dab-189">d.</span><span class="sxs-lookup"><span data-stu-id="37dab-189">d.</span></span> <span data-ttu-id="37dab-190">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="37dab-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="37dab-191">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="37dab-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="37dab-192">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="37dab-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="37dab-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37dab-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="37dab-194">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-194">Create an Azure AD test user</span></span>

<span data-ttu-id="37dab-195">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="37dab-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="37dab-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37dab-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37dab-198">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="37dab-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37dab-200">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="37dab-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37dab-202">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="37dab-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37dab-204">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="37dab-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37dab-206">a.</span><span class="sxs-lookup"><span data-stu-id="37dab-206">a.</span></span> <span data-ttu-id="37dab-207">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37dab-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37dab-208">b.</span><span class="sxs-lookup"><span data-stu-id="37dab-208">b.</span></span> <span data-ttu-id="37dab-209">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37dab-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37dab-210">c.</span><span class="sxs-lookup"><span data-stu-id="37dab-210">c.</span></span> <span data-ttu-id="37dab-211">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="37dab-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="37dab-212">d.</span><span class="sxs-lookup"><span data-stu-id="37dab-212">d.</span></span> <span data-ttu-id="37dab-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="37dab-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="37dab-214">Créer un utilisateur de test Voyance</span><span class="sxs-lookup"><span data-stu-id="37dab-214">Create a Voyance test user</span></span>

<span data-ttu-id="37dab-215">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Voyance.</span><span class="sxs-lookup"><span data-stu-id="37dab-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="37dab-216">Voyance prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="37dab-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="37dab-217">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="37dab-217">There is no action item for you in this section.</span></span> <span data-ttu-id="37dab-218">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Voyance s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="37dab-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="37dab-219">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact [équipe de support Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="37dab-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="37dab-220">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="37dab-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="37dab-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooVoyance.</span><span class="sxs-lookup"><span data-stu-id="37dab-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Attribuer le rôle d’utilisateur hello][200]

<span data-ttu-id="37dab-223">**tooassign Britta Simon tooVoyance, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37dab-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="37dab-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37dab-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="37dab-226">Dans la liste des applications hello, sélectionnez **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="37dab-226">In hello applications list, select **Voyance**.</span></span>

    ![lien de Voyance Hello dans la liste des Applications hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="37dab-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37dab-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="37dab-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="37dab-230">Click **Add** button.</span></span> <span data-ttu-id="37dab-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37dab-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="37dab-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="37dab-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="37dab-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37dab-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37dab-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37dab-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="37dab-236">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="37dab-236">Test single sign-on</span></span>

<span data-ttu-id="37dab-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="37dab-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="37dab-238">Lorsque vous cliquez sur mosaïque Voyance hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Voyance application.</span><span class="sxs-lookup"><span data-stu-id="37dab-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37dab-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="37dab-239">Additional resources</span></span>

* [<span data-ttu-id="37dab-240">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37dab-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37dab-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="37dab-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

