---
title: "Didacticiel : Intégration d’Azure Active Directory à Velpic SAML | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="9e055-103">Didacticiel : Intégration d’Azure Active Directory à Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9e055-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="9e055-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAML Velpic avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e055-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e055-105">Intégration Velpic SAML avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9e055-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9e055-106">Vous pouvez contrôler dans Azure AD qui a accès tooVelpic SAML</span><span class="sxs-lookup"><span data-stu-id="9e055-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="9e055-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooVelpic SAML (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e055-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="9e055-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9e055-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e055-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e055-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9e055-110">Prerequisites</span></span>

<span data-ttu-id="9e055-111">tooconfigure intégration d’Azure AD avec Velpic SAML, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9e055-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="9e055-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e055-113">Un abonnement Velpic SAML pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9e055-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e055-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9e055-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e055-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9e055-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e055-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9e055-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9e055-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e055-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e055-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9e055-118">Scenario description</span></span>
<span data-ttu-id="9e055-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9e055-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e055-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9e055-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e055-121">Ajout de Velpic SAML à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9e055-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="9e055-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="9e055-123">Ajout de Velpic SAML à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9e055-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="9e055-124">intégration de hello tooconfigure de Velpic SAML dans Azure AD, vous devez tooadd Velpic SAML à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9e055-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9e055-125">**tooadd SAML Velpic à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e055-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e055-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9e055-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e055-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9e055-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9e055-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9e055-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9e055-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9e055-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9e055-133">Dans la zone de recherche de hello, tapez **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e055-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="9e055-135">Dans le volet de résultats hello, sélectionnez **Velpic SAML**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9e055-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e055-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e055-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Velpic SAML avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9e055-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e055-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Velpic SAML est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e055-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="9e055-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Velpic SAML doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9e055-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="9e055-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9e055-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="9e055-142">tooconfigure et test Azure AD l’authentification unique avec Velpic SAML, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9e055-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9e055-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9e055-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9e055-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e055-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e055-145">**[Création d’un utilisateur de test Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave de Britta Simon dans Velpic SAML qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="9e055-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9e055-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9e055-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e055-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9e055-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e055-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e055-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9e055-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="9e055-150">**tooconfigure Azure AD single sign-on avec Velpic SAML, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e055-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e055-151">Dans le portail de gestion Azure hello, sur hello **Velpic SAML** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9e055-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9e055-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9e055-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="9e055-155">Entrez les détails de hello Bonjour **Velpic SAML domaine et les URL** section -</span><span class="sxs-lookup"><span data-stu-id="9e055-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="9e055-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e055-157">a.</span></span> <span data-ttu-id="9e055-158">Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="9e055-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="9e055-159">b.</span><span class="sxs-lookup"><span data-stu-id="9e055-159">b.</span></span> <span data-ttu-id="9e055-160">Bonjour **identificateur** zone de texte, collez hello **'Single sign on URL'** valeur`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="9e055-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9e055-161">Veuillez noter que hello l’URL de connexion est fournie par hello équipe de Velpic SAML et valeur d’identificateur seront disponible lorsque vous configurez hello plug-in de SSO côté Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9e055-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="9e055-162">Vous devez toocopy à partir de la page d’application Velpic SAML et collez-le ici.</span><span class="sxs-lookup"><span data-stu-id="9e055-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="9e055-163">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9e055-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="9e055-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9e055-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e055-167">Sur la section de Configuration de SAML Velpic de hello, cliquez sur fenêtre Configurer les SAML Velpic tooopen configurer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="9e055-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="9e055-168">Copiez hello SAML de l’entité à partir de la section de référence rapide de hello.</span><span class="sxs-lookup"><span data-stu-id="9e055-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="9e055-169">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Velpic SAML en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9e055-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="9e055-170">Cliquez sur **gérer** onglet et accédez trop**intégration** section où vous avez besoin de tooclick sur **plug-ins** bouton toocreate nouveau plug-in pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="9e055-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="9e055-172">Cliquez sur hello **'Ajouter le plug-in'** bouton.</span><span class="sxs-lookup"><span data-stu-id="9e055-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="9e055-174">Cliquez sur hello **SAML** vignette dans la page Ajouter un plug-in de hello.</span><span class="sxs-lookup"><span data-stu-id="9e055-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="9e055-176">Tapez hello du plug-in SAML nouvelle hello et cliquez sur hello **'Add'** bouton.</span><span class="sxs-lookup"><span data-stu-id="9e055-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="9e055-178">Entrez les détails de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e055-178">Enter hello details as follows:</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="9e055-180">a.</span><span class="sxs-lookup"><span data-stu-id="9e055-180">a.</span></span> <span data-ttu-id="9e055-181">Bonjour **nom** zone de texte, nom du type hello du plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="9e055-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="9e055-182">b.</span><span class="sxs-lookup"><span data-stu-id="9e055-182">b.</span></span> <span data-ttu-id="9e055-183">Bonjour **URL de l’émetteur** zone de texte, collez hello **ID d’entité SAML** vous avez copié à partir de hello **configurer l’authentification** fenêtre Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e055-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="9e055-184">c.</span><span class="sxs-lookup"><span data-stu-id="9e055-184">c.</span></span> <span data-ttu-id="9e055-185">Bonjour **fournisseur de métadonnées Config** télécharger hello fichier Metadata XML que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e055-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="9e055-186">d.</span><span class="sxs-lookup"><span data-stu-id="9e055-186">d.</span></span> <span data-ttu-id="9e055-187">Vous pouvez également choisir tooenable SAML configuration en temps en activant hello **'Automatiquement créer de nouveaux utilisateurs'** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="9e055-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="9e055-188">Si un utilisateur n’existe pas dans Velpic et cet indicateur n’est pas activé, la connexion hello à partir d’Azure échoue.</span><span class="sxs-lookup"><span data-stu-id="9e055-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="9e055-189">Si l’indicateur de hello est activé hello utilisateur sera automatiquement les configurer dans Velpic au moment de hello de connexion.</span><span class="sxs-lookup"><span data-stu-id="9e055-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="9e055-190">e.</span><span class="sxs-lookup"><span data-stu-id="9e055-190">e.</span></span> <span data-ttu-id="9e055-191">Hello de copie **URL de l’authentification unique** à partir de la zone de texte hello et les coller dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e055-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="9e055-192">f.</span><span class="sxs-lookup"><span data-stu-id="9e055-192">f.</span></span> <span data-ttu-id="9e055-193">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="9e055-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e055-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e055-195">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e055-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9e055-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e055-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e055-198">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9e055-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e055-200">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9e055-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e055-202">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e055-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e055-204">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e055-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e055-206">a.</span><span class="sxs-lookup"><span data-stu-id="9e055-206">a.</span></span> <span data-ttu-id="9e055-207">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e055-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e055-208">b.</span><span class="sxs-lookup"><span data-stu-id="9e055-208">b.</span></span> <span data-ttu-id="9e055-209">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e055-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e055-210">c.</span><span class="sxs-lookup"><span data-stu-id="9e055-210">c.</span></span> <span data-ttu-id="9e055-211">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9e055-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9e055-212">d.</span><span class="sxs-lookup"><span data-stu-id="9e055-212">d.</span></span> <span data-ttu-id="9e055-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9e055-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="9e055-214">Création d’un utilisateur de test Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9e055-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="9e055-215">Cette étape n’est généralement pas nécessaire que prend en charge de l’application hello juste-à-temps l’approvisionnement des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9e055-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="9e055-216">Si le provisionnement utilisateur automatique hello n’est pas activé la création manuelle de l’utilisateur peut faite comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9e055-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="9e055-217">Connectez-vous au site de votre entreprise Velpic SAML en tant qu’administrateur et effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e055-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="9e055-218">Cliquez sur l’onglet gérer accédez tooUsers section, puis cliquez sur nouveaux utilisateurs tooadd de bouton.</span><span class="sxs-lookup"><span data-stu-id="9e055-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![ajouter un utilisateur](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="9e055-220">Sur hello **« Créer un nouvel utilisateur »** boîte de dialogue de page, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="9e055-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="9e055-222">a.</span><span class="sxs-lookup"><span data-stu-id="9e055-222">a.</span></span> <span data-ttu-id="9e055-223">Bonjour **prénom** zone de texte, type hello prénom Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e055-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="9e055-224">b.</span><span class="sxs-lookup"><span data-stu-id="9e055-224">b.</span></span> <span data-ttu-id="9e055-225">Bonjour **nom** zone de texte, tapez nom de famille hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e055-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="9e055-226">c.</span><span class="sxs-lookup"><span data-stu-id="9e055-226">c.</span></span> <span data-ttu-id="9e055-227">Bonjour **nom d’utilisateur** zone de texte, nom d’utilisateur de type hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e055-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="9e055-228">d.</span><span class="sxs-lookup"><span data-stu-id="9e055-228">d.</span></span> <span data-ttu-id="9e055-229">Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e055-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="9e055-230">e.</span><span class="sxs-lookup"><span data-stu-id="9e055-230">e.</span></span> <span data-ttu-id="9e055-231">Autres informations de hello est facultatif, que vous pouvez le remplir si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9e055-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="9e055-232">f.</span><span class="sxs-lookup"><span data-stu-id="9e055-232">f.</span></span> <span data-ttu-id="9e055-233">Cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="9e055-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9e055-234">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e055-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9e055-235">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooVelpic accès SAML.</span><span class="sxs-lookup"><span data-stu-id="9e055-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9e055-237">**tooassign Britta Simon tooVelpic SAML, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e055-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e055-238">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9e055-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9e055-240">Dans la liste des applications hello, sélectionnez **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e055-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="9e055-242">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9e055-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9e055-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9e055-244">Click **Add** button.</span></span> <span data-ttu-id="9e055-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9e055-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9e055-247">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9e055-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9e055-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9e055-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e055-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9e055-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e055-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9e055-250">Testing single sign-on</span></span>

<span data-ttu-id="9e055-251">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9e055-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="9e055-252">Lorsque vous cliquez sur hello Velpic SAML vignette Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application de Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9e055-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="9e055-253">Vous devez voir hello **« Ouvrir une session avec Azure AD »** bouton sur la page de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="9e055-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="9e055-255">Cliquez sur hello **« Ouvrir une session avec Azure AD »** toolog de bouton dans tooVelpic à l’aide de votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e055-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9e055-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9e055-256">Additional resources</span></span>

* [<span data-ttu-id="9e055-257">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e055-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e055-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9e055-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

