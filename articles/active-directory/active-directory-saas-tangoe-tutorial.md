---
title: "Didacticiel : intégration d’Azure Active Directory à Tangoe Command Premium Mobile | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Tangoe commande Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="4f6eb-103">Didacticiel : Intégration d’Azure Active Directory à Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="4f6eb-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="4f6eb-104">Dans ce didacticiel, vous apprendrez comment toointegrate Tangoe commande Premium Mobile avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f6eb-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f6eb-105">Intégration Tangoe commande Premium Mobile auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4f6eb-106">Vous pouvez contrôler dans Azure AD qui a accès tooTangoe commande Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="4f6eb-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="4f6eb-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTangoe Mobile Premium de commande (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f6eb-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f6eb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4f6eb-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f6eb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f6eb-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4f6eb-110">Prerequisites</span></span>

<span data-ttu-id="4f6eb-111">tooconfigure intégration d’Azure AD avec Tangoe commande Premium Mobile, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="4f6eb-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f6eb-113">Un abonnement Tangoe Command Premium Mobile pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4f6eb-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f6eb-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f6eb-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f6eb-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f6eb-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f6eb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f6eb-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4f6eb-118">Scenario description</span></span>
<span data-ttu-id="4f6eb-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f6eb-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f6eb-121">Ajouter des Tangoe commande Premium Mobile à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4f6eb-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="4f6eb-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="4f6eb-123">Ajouter des Tangoe commande Premium Mobile à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4f6eb-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="4f6eb-124">intégration de hello tooconfigure de Tangoe commande Premium Mobile dans Azure AD, vous devez tooadd Tangoe commande Premium Mobile à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4f6eb-125">**tooadd Tangoe commande Premium Mobile à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f6eb-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f6eb-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4f6eb-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4f6eb-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4f6eb-133">Dans la zone de recherche de hello, tapez **Tangoe commande Premium Mobile**, sélectionnez **Tangoe commande Premium Mobile** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="4f6eb-134">Ajouter Tangoe Command Premium Mobile à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4f6eb-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4f6eb-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4f6eb-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tangoe Command Premium Mobile pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4f6eb-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f6eb-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Tangoe commande Premium Mobile est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="4f6eb-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Tangoe commande Premium Mobile doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="4f6eb-139">Dans Tangoe commande Premium Mobile, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4f6eb-140">tooconfigure et test Azure AD l’authentification unique avec Tangoe commande Premium Mobile, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4f6eb-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4f6eb-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f6eb-143">**[Créer un utilisateur de test Tangoe commande Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave un équivalent de Britta Simon dans Tangoe commande Premium Mobile qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f6eb-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f6eb-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4f6eb-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4f6eb-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Mobile de Tangoe commande Premium.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="4f6eb-148">**tooconfigure Azure AD l’authentification unique avec Tangoe commande Premium Mobile, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f6eb-149">Bonjour portail Azure, sur hello **Tangoe commande Premium Mobile** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4f6eb-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="4f6eb-153">Sur hello **Tangoe commande Premium Mobile domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Domaine et URL Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="4f6eb-155">a.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-155">a.</span></span> <span data-ttu-id="4f6eb-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="4f6eb-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="4f6eb-157">b.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-157">b.</span></span> <span data-ttu-id="4f6eb-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="4f6eb-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f6eb-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-159">These values are not real.</span></span> <span data-ttu-id="4f6eb-160">Mettre à jour ces valeurs avec l’URL de réponse réelle hello et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="4f6eb-161">Contact [équipe de support Premium Mobile Client Tangoe commande](https://www.tangoe.com/contact-2/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="4f6eb-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="4f6eb-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4f6eb-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4f6eb-166">Sur hello **Tangoe commande Premium Mobile Configuration** , cliquez sur **configurer Tangoe commande Premium Mobile** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4f6eb-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Section Configuration de Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="4f6eb-169">tooget l’authentification unique configurée pour votre application, contactez votre [équipe de support Premium Mobile Client Tangoe commande](https://www.tangoe.com/contact-2/) et fournir hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="4f6eb-170">fichier de métadonnées téléchargé Hello</span><span class="sxs-lookup"><span data-stu-id="4f6eb-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="4f6eb-171">Hello **ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="4f6eb-172">Hello **SAML Sign-On URL du Service unique**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="4f6eb-173">Hello **URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="4f6eb-174">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4f6eb-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4f6eb-175">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4f6eb-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f6eb-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4f6eb-177">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-177">Create an Azure AD test user</span></span>
<span data-ttu-id="4f6eb-178">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4f6eb-180">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f6eb-181">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f6eb-183">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes -> Tous les utilisateurs](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f6eb-185">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Ajouter un utilisateur](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f6eb-187">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f6eb-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f6eb-189">a.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-189">a.</span></span> <span data-ttu-id="4f6eb-190">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f6eb-191">b.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-191">b.</span></span> <span data-ttu-id="4f6eb-192">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f6eb-193">c.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-193">c.</span></span> <span data-ttu-id="4f6eb-194">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4f6eb-195">d.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-195">d.</span></span> <span data-ttu-id="4f6eb-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="4f6eb-197">Créer un utilisateur de test Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="4f6eb-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="4f6eb-198">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="4f6eb-199">Application Tangoe commande Premium Mobile doit tous les toobe d’utilisateurs hello configuré dans l’application hello avant de procéder à l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="4f6eb-200">Veuillez travail avec hello [équipe de support Premium Mobile Client Tangoe commande](https://www.tangoe.com/contact-2/) tooprovision tous ces utilisateurs dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4f6eb-201">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f6eb-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4f6eb-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTangoe commande Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4f6eb-204">**tooassign Britta Simon tooTangoe commande Premium Mobile, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f6eb-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f6eb-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4f6eb-207">Dans la liste des applications hello, sélectionnez **Tangoe commande Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile dans la liste des applications](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="4f6eb-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4f6eb-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-211">Click **Add** button.</span></span> <span data-ttu-id="4f6eb-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4f6eb-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4f6eb-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f6eb-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4f6eb-217">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4f6eb-217">Test single sign-on</span></span>

<span data-ttu-id="4f6eb-218">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4f6eb-219">Lorsque vous cliquez sur mosaïque Tangoe commande Premium Mobile hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Tangoe commande Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="4f6eb-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="4f6eb-220">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f6eb-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4f6eb-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4f6eb-221">Additional resources</span></span>

* [<span data-ttu-id="4f6eb-222">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f6eb-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f6eb-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4f6eb-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

