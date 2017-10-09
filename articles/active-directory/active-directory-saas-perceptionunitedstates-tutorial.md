---
title: "Didacticiel : Intégration d’Azure Active Directory à Perception United States (Non-UltiPro) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la Perception United States (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="8a218-103">Didacticiel : Intégration d’Azure Active Directory à Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="8a218-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="8a218-104">Dans ce didacticiel, vous apprendrez comment toointegrate Perception United States (Non-UltiPro) avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a218-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a218-105">Intégration Perception United States (Non-UltiPro) à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8a218-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a218-106">Vous pouvez contrôler dans Azure AD qui a accès tooPerception États-Unis (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="8a218-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="8a218-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPerception États-Unis (Non-UltiPro) (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a218-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8a218-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8a218-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8a218-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a218-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a218-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8a218-110">Prerequisites</span></span>

<span data-ttu-id="8a218-111">tooconfigure intégration d’Azure AD avec Perception États-Unis (Non-UltiPro), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8a218-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="8a218-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a218-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a218-113">Un abonnement Perception United States (Non-UltiPro) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8a218-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a218-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8a218-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a218-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8a218-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a218-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8a218-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a218-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a218-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a218-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8a218-118">Scenario description</span></span>
<span data-ttu-id="8a218-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8a218-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a218-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8a218-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a218-121">Ajout de Perception United States (Non-UltiPro) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8a218-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="8a218-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a218-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="8a218-123">Ajout de Perception United States (Non-UltiPro) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8a218-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="8a218-124">intégration de hello tooconfigure de Perception États-Unis (Non-UltiPro) dans Azure AD, vous devez tooadd Perception United States (Non-UltiPro) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8a218-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a218-125">**tooadd Perception United States (Non-UltiPro) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a218-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a218-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8a218-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="8a218-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8a218-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a218-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a218-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="8a218-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8a218-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="8a218-133">Dans la zone de recherche de hello, tapez **Perception United States (Non-UltiPro)**, sélectionnez **Perception United States (Non-UltiPro)** à partir du volet de résultats, puis sur **ajouter** tooadd de bouton application Hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Perception United States (Non-UltiPro) dans la liste des résultats hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8a218-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a218-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8a218-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Perception United States (Non-UltiPro) grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8a218-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a218-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Perception États-Unis (Non-UltiPro) est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a218-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="8a218-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Perception États-Unis (Non-UltiPro) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8a218-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="8a218-139">Dans Perception États-Unis (Non-UltiPro), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a218-140">tooconfigure et test Azure AD l’authentification unique avec Perception États-Unis (Non-UltiPro), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8a218-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a218-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8a218-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a218-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a218-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a218-143">**[Créer un utilisateur de test Perception United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave un équivalent de Britta Simon dans Perception États-Unis (Non-UltiPro) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a218-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a218-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a218-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a218-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8a218-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8a218-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a218-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8a218-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="8a218-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="8a218-148">**tooconfigure Azure AD de l’authentification unique avec Perception États-Unis (Non-UltiPro), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a218-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="8a218-149">Bonjour portail Azure, sur hello **Perception United States (Non-UltiPro)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8a218-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="8a218-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a218-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="8a218-153">Sur hello **Perception United States (Non-UltiPro) domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a218-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification Domaine et URL Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="8a218-155">a.</span><span class="sxs-lookup"><span data-stu-id="8a218-155">a.</span></span> <span data-ttu-id="8a218-156">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="8a218-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="8a218-157">b.</span><span class="sxs-lookup"><span data-stu-id="8a218-157">b.</span></span> <span data-ttu-id="8a218-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="8a218-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a218-159">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="8a218-159">hello value is not real.</span></span> <span data-ttu-id="8a218-160">Vous mettrez à jour la valeur de hello avec l’URL de réponse réelle hello, qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="8a218-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8a218-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="8a218-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8a218-163">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a218-165">Sur hello **Perception United States (Non-UltiPro) Configuration** , cliquez sur **configurer Perception États-Unis (Non-UltiPro)** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8a218-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8a218-166">Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8a218-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="8a218-167">a.</span><span class="sxs-lookup"><span data-stu-id="8a218-167">a.</span></span> <span data-ttu-id="8a218-168">Hello **Perception United States (Non-UltiPro)** requiert l’application hello **ID d’entité SAML** toobe uri de valeur, qui vous avez copié, encodé.</span><span class="sxs-lookup"><span data-stu-id="8a218-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="8a218-169">lien de suivant de hello utilisation tooget valeur de l’uri encodé hello, :**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="8a218-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="8a218-170">b.</span><span class="sxs-lookup"><span data-stu-id="8a218-170">b.</span></span> <span data-ttu-id="8a218-171">Après obtention d’uri de hello valeur encodée associer hello **URL de réponse** comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8a218-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="8a218-172">c.</span><span class="sxs-lookup"><span data-stu-id="8a218-172">c.</span></span> <span data-ttu-id="8a218-173">Hello Coller au-dessus de la valeur Bonjour **URL de réponse** zone de texte dans **Perception United States (Non-UltiPro) domaine et les URL** section.</span><span class="sxs-lookup"><span data-stu-id="8a218-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Configuration de Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="8a218-175">Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour Perception United States (Non-UltiPro) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8a218-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="8a218-176">Dans la barre d’outils principale hello, cliquez sur **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="8a218-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Utilisateur Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="8a218-178">Sur hello **les paramètres de compte** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a218-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Utilisateur Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="8a218-180">a.</span><span class="sxs-lookup"><span data-stu-id="8a218-180">a.</span></span> <span data-ttu-id="8a218-181">Bonjour **nom de la société** zone de texte, nom du type hello Hello **entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8a218-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="8a218-182">b.</span><span class="sxs-lookup"><span data-stu-id="8a218-182">b.</span></span> <span data-ttu-id="8a218-183">Bonjour **nom de compte** zone de texte, nom du type hello Hello **compte**.</span><span class="sxs-lookup"><span data-stu-id="8a218-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="8a218-184">c.</span><span class="sxs-lookup"><span data-stu-id="8a218-184">c.</span></span> <span data-ttu-id="8a218-185">Dans **réponse par défaut-tooEmail** zone de texte, hello type valide **E-mail**.</span><span class="sxs-lookup"><span data-stu-id="8a218-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="8a218-186">d.</span><span class="sxs-lookup"><span data-stu-id="8a218-186">d.</span></span> <span data-ttu-id="8a218-187">Sélectionnez le **fournisseur d’identité d’authentification unique** **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="8a218-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="8a218-188">Sur hello **Configuration SSO** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a218-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Configuration de l’authentification unique Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="8a218-190">a.</span><span class="sxs-lookup"><span data-stu-id="8a218-190">a.</span></span> <span data-ttu-id="8a218-191">Sélectionnez le **type de NameID SAML** **E-MAIL**.</span><span class="sxs-lookup"><span data-stu-id="8a218-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="8a218-192">b.</span><span class="sxs-lookup"><span data-stu-id="8a218-192">b.</span></span> <span data-ttu-id="8a218-193">Bonjour **nom de Configuration de l’authentification unique** nom hello du type de zone de texte votre **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="8a218-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="8a218-194">c.</span><span class="sxs-lookup"><span data-stu-id="8a218-194">c.</span></span> <span data-ttu-id="8a218-195">Dans **nom de fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8a218-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="8a218-196">d.</span><span class="sxs-lookup"><span data-stu-id="8a218-196">d.</span></span> <span data-ttu-id="8a218-197">Dans **SAML domaine textbox**, entrez le domaine hello comme  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="8a218-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="8a218-198">e.</span><span class="sxs-lookup"><span data-stu-id="8a218-198">e.</span></span> <span data-ttu-id="8a218-199">Cliquez sur **télécharger à nouveau** hello de tooupload **Metadata XML** fichier.</span><span class="sxs-lookup"><span data-stu-id="8a218-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="8a218-200">f.</span><span class="sxs-lookup"><span data-stu-id="8a218-200">f.</span></span> <span data-ttu-id="8a218-201">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="8a218-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="8a218-202">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8a218-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a218-203">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a218-204">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a218-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8a218-205">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a218-205">Create an Azure AD test user</span></span>

<span data-ttu-id="8a218-206">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8a218-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="8a218-208">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a218-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a218-209">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="8a218-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8a218-211">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8a218-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8a218-213">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8a218-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8a218-215">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a218-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8a218-217">a.</span><span class="sxs-lookup"><span data-stu-id="8a218-217">a.</span></span> <span data-ttu-id="8a218-218">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a218-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a218-219">b.</span><span class="sxs-lookup"><span data-stu-id="8a218-219">b.</span></span> <span data-ttu-id="8a218-220">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a218-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8a218-221">c.</span><span class="sxs-lookup"><span data-stu-id="8a218-221">c.</span></span> <span data-ttu-id="8a218-222">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="8a218-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8a218-223">d.</span><span class="sxs-lookup"><span data-stu-id="8a218-223">d.</span></span> <span data-ttu-id="8a218-224">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a218-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="8a218-225">Créer un utilisateur de test Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="8a218-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="8a218-226">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="8a218-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="8a218-227">Travailler avec [équipe de support Perception United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd les utilisateurs de hello dans la plateforme de Perception United States (Non-UltiPro) hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8a218-228">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a218-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8a218-229">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPerception États-Unis (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="8a218-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="8a218-231">**tooassign tooPerception Britta Simon États-Unis (Non-UltiPro), exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a218-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="8a218-232">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a218-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8a218-234">Dans la liste des applications hello, sélectionnez **Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="8a218-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![lien de Perception United States (Non-UltiPro) Hello dans la liste des Applications hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="8a218-236">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a218-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="8a218-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8a218-238">Click **Add** button.</span></span> <span data-ttu-id="8a218-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a218-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="8a218-241">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a218-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a218-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a218-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a218-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8a218-244">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8a218-244">Test single sign-on</span></span>

<span data-ttu-id="8a218-245">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8a218-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a218-246">Lorsque vous cliquez sur mosaïque Perception United States (Non-UltiPro) hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Perception United States (Non-UltiPro) application.</span><span class="sxs-lookup"><span data-stu-id="8a218-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="8a218-247">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a218-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8a218-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8a218-248">Additional resources</span></span>

* [<span data-ttu-id="8a218-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a218-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a218-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8a218-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

