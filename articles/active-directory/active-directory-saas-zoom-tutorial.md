---
title: "Didacticiel : Intégration d’Azure Active Directory à Zoom | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zoom."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="dba3b-103">Didacticiel : Intégration d’Azure Active Directory à Zoom</span><span class="sxs-lookup"><span data-stu-id="dba3b-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="dba3b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zoom avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dba3b-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dba3b-105">Intégration de Zoom à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dba3b-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dba3b-106">Vous pouvez contrôler dans Azure AD qui a accès tooZoom.</span><span class="sxs-lookup"><span data-stu-id="dba3b-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="dba3b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZoom (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dba3b-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dba3b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dba3b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="dba3b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dba3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dba3b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dba3b-110">Prerequisites</span></span>

<span data-ttu-id="dba3b-111">intégration de tooconfigure Azure AD à Zoom, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dba3b-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="dba3b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dba3b-113">Un abonnement Zoom pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dba3b-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dba3b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dba3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dba3b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dba3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dba3b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dba3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dba3b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dba3b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dba3b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dba3b-118">Scenario description</span></span>
<span data-ttu-id="dba3b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dba3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dba3b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dba3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dba3b-121">Ajout de Zoom à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dba3b-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="dba3b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="dba3b-123">Ajout de Zoom à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dba3b-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="dba3b-124">intégration de hello tooconfigure de Zoom dans Azure AD, vous devez tooadd Zoom à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dba3b-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dba3b-125">**tooadd Zoom à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dba3b-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dba3b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dba3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="dba3b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dba3b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="dba3b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dba3b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="dba3b-133">Dans la zone de recherche de hello, tapez **Zoom**, sélectionnez **Zoom** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dba3b-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Effectuer un zoom avant dans la liste des résultats hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dba3b-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba3b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dba3b-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zoom avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dba3b-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dba3b-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zoom est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dba3b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="dba3b-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zoom besoins toobe est établie.</span><span class="sxs-lookup"><span data-stu-id="dba3b-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="dba3b-139">Dans la zone de Zoom, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="dba3b-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dba3b-140">tooconfigure et test Azure AD l’authentification unique sur Zoom, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dba3b-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dba3b-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dba3b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dba3b-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dba3b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dba3b-143">**[Créer un utilisateur de test de Zoom](#create-a-zoom-test-user)**  -toohave un équivalent de Britta Simon dans Zoom qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dba3b-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dba3b-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dba3b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dba3b-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dba3b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dba3b-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba3b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dba3b-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Zoom.</span><span class="sxs-lookup"><span data-stu-id="dba3b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="dba3b-148">**tooconfigure Azure AD l’authentification unique sur Zoom, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dba3b-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="dba3b-149">Bonjour portail Azure, sur hello **Zoom** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="dba3b-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dba3b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="dba3b-153">Sur hello **Zoom sur le domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dba3b-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="dba3b-155">a.</span><span class="sxs-lookup"><span data-stu-id="dba3b-155">a.</span></span> <span data-ttu-id="dba3b-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="dba3b-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="dba3b-157">b.</span><span class="sxs-lookup"><span data-stu-id="dba3b-157">b.</span></span> <span data-ttu-id="dba3b-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="dba3b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dba3b-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="dba3b-159">These values are not real.</span></span> <span data-ttu-id="dba3b-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="dba3b-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dba3b-161">Contact [équipe de support Client de Zoom](https://support.zoom.us/hc) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="dba3b-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="dba3b-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dba3b-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="dba3b-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dba3b-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dba3b-166">Sur hello **effectuer un zoom avant la Configuration** , cliquez sur **configurer Zoom** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dba3b-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dba3b-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dba3b-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="dba3b-169">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Zoom tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dba3b-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="dba3b-170">Cliquez sur hello **Single Sign-On** onglet.</span><span class="sxs-lookup"><span data-stu-id="dba3b-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="dba3b-171">![Onglet Single Sign-On](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="dba3b-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="dba3b-172">Cliquez sur hello **contrôle de sécurité** onglet et passez toohello **Single Sign-On** paramètres.</span><span class="sxs-lookup"><span data-stu-id="dba3b-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="dba3b-173">Bonjour section Single Sign-On, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dba3b-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dba3b-174">![Section Single Sign-On](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="dba3b-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="dba3b-175">a.</span><span class="sxs-lookup"><span data-stu-id="dba3b-175">a.</span></span> <span data-ttu-id="dba3b-176">Bonjour **URL de la page connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dba3b-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="dba3b-177">b.</span><span class="sxs-lookup"><span data-stu-id="dba3b-177">b.</span></span> <span data-ttu-id="dba3b-178">Bonjour **URL de la page de déconnexion** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dba3b-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="dba3b-179">c.</span><span class="sxs-lookup"><span data-stu-id="dba3b-179">c.</span></span> <span data-ttu-id="dba3b-180">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dba3b-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="dba3b-181">d.</span><span class="sxs-lookup"><span data-stu-id="dba3b-181">d.</span></span> <span data-ttu-id="dba3b-182">Bonjour **émetteur** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dba3b-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="dba3b-183">e.</span><span class="sxs-lookup"><span data-stu-id="dba3b-183">e.</span></span> <span data-ttu-id="dba3b-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dba3b-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="dba3b-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dba3b-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dba3b-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dba3b-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dba3b-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dba3b-188">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba3b-188">Create an Azure AD test user</span></span>

<span data-ttu-id="dba3b-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="dba3b-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="dba3b-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dba3b-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dba3b-192">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="dba3b-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="dba3b-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="dba3b-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dba3b-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="dba3b-198">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dba3b-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dba3b-200">a.</span><span class="sxs-lookup"><span data-stu-id="dba3b-200">a.</span></span> <span data-ttu-id="dba3b-201">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dba3b-202">b.</span><span class="sxs-lookup"><span data-stu-id="dba3b-202">b.</span></span> <span data-ttu-id="dba3b-203">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dba3b-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="dba3b-204">c.</span><span class="sxs-lookup"><span data-stu-id="dba3b-204">c.</span></span> <span data-ttu-id="dba3b-205">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="dba3b-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="dba3b-206">d.</span><span class="sxs-lookup"><span data-stu-id="dba3b-206">d.</span></span> <span data-ttu-id="dba3b-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="dba3b-208">Créer un utilisateur de test Zoom</span><span class="sxs-lookup"><span data-stu-id="dba3b-208">Create a Zoom test user</span></span>

<span data-ttu-id="dba3b-209">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooZoom, vous devez les configurer dans Zoom.</span><span class="sxs-lookup"><span data-stu-id="dba3b-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="dba3b-210">Dans les cas de hello de Zoom, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="dba3b-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="dba3b-211">tooprovision un compte d’utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dba3b-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="dba3b-212">Connectez-vous à tooyour **Zoom** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dba3b-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="dba3b-213">Cliquez sur hello **la gestion des comptes** onglet, puis cliquez sur **gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="dba3b-214">Bonjour section User Management, cliquez sur **ajouter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="dba3b-215">![Gestion des utilisateurs](./media/active-directory-saas-zoom-tutorial/IC784703.png "gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="dba3b-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="dba3b-216">Sur hello **ajouter des utilisateurs** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dba3b-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="dba3b-217">![Ajouter des utilisateurs](./media/active-directory-saas-zoom-tutorial/IC784704.png "Ajouter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="dba3b-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="dba3b-218">a.</span><span class="sxs-lookup"><span data-stu-id="dba3b-218">a.</span></span> <span data-ttu-id="dba3b-219">Comme **User Type**, sélectionnez **Basic**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="dba3b-220">b.</span><span class="sxs-lookup"><span data-stu-id="dba3b-220">b.</span></span> <span data-ttu-id="dba3b-221">Bonjour **E-mails** zone de texte, tapez Bonjour adresse de messagerie d’un Azure valide compte AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="dba3b-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="dba3b-222">c.</span><span class="sxs-lookup"><span data-stu-id="dba3b-222">c.</span></span> <span data-ttu-id="dba3b-223">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="dba3b-224">Vous pouvez utiliser n’importe quel autre Zoom utilisateur compte outil de création ou API fournie par Zoom tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dba3b-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="dba3b-225">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba3b-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="dba3b-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZoom.</span><span class="sxs-lookup"><span data-stu-id="dba3b-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="dba3b-228">**tooassign Britta Simon tooZoom, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dba3b-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="dba3b-229">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dba3b-231">Dans la liste des applications hello, sélectionnez **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-231">In hello applications list, select **Zoom**.</span></span>

    ![lien de Zoom Hello dans la liste des Applications hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="dba3b-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="dba3b-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-235">Click **Add** button.</span></span> <span data-ttu-id="dba3b-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="dba3b-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dba3b-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dba3b-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dba3b-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dba3b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dba3b-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dba3b-241">Test single sign-on</span></span>

<span data-ttu-id="dba3b-242">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dba3b-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dba3b-243">Lorsque vous cliquez sur mosaïque de Zoom hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Zoom application.</span><span class="sxs-lookup"><span data-stu-id="dba3b-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dba3b-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dba3b-244">Additional resources</span></span>

* [<span data-ttu-id="dba3b-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dba3b-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dba3b-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dba3b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

