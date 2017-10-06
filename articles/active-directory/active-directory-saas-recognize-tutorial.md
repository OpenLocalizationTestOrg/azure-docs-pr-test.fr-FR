---
title: "Didacticiel : intégration d’Azure Active Directory à Recognize | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de reconnaissance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="c4916-103">Didacticiel : Intégration d’Azure Active Directory à Recognize</span><span class="sxs-lookup"><span data-stu-id="c4916-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="c4916-104">Dans ce didacticiel, vous apprendrez comment toointegrate reconnaître avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4916-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4916-105">Intégration de reconnaître à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c4916-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4916-106">Vous pouvez contrôler dans Azure AD qui a accès tooRecognize</span><span class="sxs-lookup"><span data-stu-id="c4916-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="c4916-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRecognize (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4916-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c4916-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4916-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4916-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4916-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c4916-110">Prerequisites</span></span>

<span data-ttu-id="c4916-111">intégration d’Azure AD de tooconfigure avec reconnaissance, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c4916-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="c4916-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4916-113">Un abonnement Recognize pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c4916-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4916-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c4916-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4916-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c4916-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4916-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c4916-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4916-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4916-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4916-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c4916-118">Scenario description</span></span>
<span data-ttu-id="c4916-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c4916-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4916-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c4916-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4916-121">Ajout de reconnaître à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c4916-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="c4916-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="c4916-123">Ajout de reconnaître à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c4916-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="c4916-124">tooconfigure hello intégration de reconnaître dans Azure AD, vous devez tooadd reconnaître à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c4916-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4916-125">**tooadd reconnaître à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4916-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4916-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c4916-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4916-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c4916-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4916-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c4916-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c4916-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c4916-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c4916-133">Dans la zone de recherche de hello, tapez **reconnaître**.</span><span class="sxs-lookup"><span data-stu-id="c4916-133">In hello search box, type **Recognize**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="c4916-135">Dans le volet de résultats hello, sélectionnez **reconnaître**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c4916-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4916-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4916-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Recognize sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c4916-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4916-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello reconnaître est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4916-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="c4916-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de reconnaître hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c4916-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="c4916-141">Dans le reconnaître, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c4916-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4916-142">tooconfigure et test Azure AD sur l’authentification unique avec reconnaissance, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c4916-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4916-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c4916-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4916-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4916-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4916-145">**[Création d’un utilisateur de test de reconnaître](#creating-a-recognize-test-user)**  -toohave un équivalent de Britta Simon dans reconnaître est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c4916-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4916-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c4916-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4916-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c4916-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4916-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4916-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de reconnaître.</span><span class="sxs-lookup"><span data-stu-id="c4916-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="c4916-150">**tooconfigure Azure AD single sign-on avec reconnaissance, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4916-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4916-151">Bonjour portail Azure, sur hello **reconnaître** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c4916-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c4916-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c4916-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="c4916-155">Sur hello **reconnaît le domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4916-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="c4916-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4916-157">a.</span></span> <span data-ttu-id="c4916-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="c4916-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="c4916-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4916-159">b.</span></span> <span data-ttu-id="c4916-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="c4916-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4916-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c4916-161">These values are not real.</span></span> <span data-ttu-id="c4916-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="c4916-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4916-163">Contact [équipe de support Client de reconnaître](mailto:support@recognizeapp.com) pour obtenir l’URL de connexion et que vous pouvez obtenir valeur de l’identificateur en ouvrant hello URL du Service fournisseur de métadonnées à partir de la section de paramètres d’authentification unique est expliquée plus loin dans le didacticiel de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="c4916-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="c4916-164">.</span><span class="sxs-lookup"><span data-stu-id="c4916-164">.</span></span> 
 
4. <span data-ttu-id="c4916-165">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c4916-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="c4916-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c4916-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4916-169">Sur hello **reconnaître une Configuration** , cliquez sur **configurer reconnaît** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c4916-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4916-170">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c4916-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="c4916-172">Dans une fenêtre de navigateur web, client de reconnaître tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c4916-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="c4916-173">Dans le coin supérieur droit hello, cliquez sur **Menu**.</span><span class="sxs-lookup"><span data-stu-id="c4916-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="c4916-174">Accédez trop**administrateur de l’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c4916-174">Go too**Company Admin**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="c4916-176">Dans le volet de navigation gauche hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c4916-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="c4916-178">Effectuer hello comme suit **paramètres d’authentification unique** section.</span><span class="sxs-lookup"><span data-stu-id="c4916-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="c4916-180">a.</span><span class="sxs-lookup"><span data-stu-id="c4916-180">a.</span></span> <span data-ttu-id="c4916-181">Pour **Activer l’authentification unique**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="c4916-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="c4916-182">b.</span><span class="sxs-lookup"><span data-stu-id="c4916-182">b.</span></span> <span data-ttu-id="c4916-183">Bonjour **IDP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4916-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c4916-184">c.</span><span class="sxs-lookup"><span data-stu-id="c4916-184">c.</span></span> <span data-ttu-id="c4916-185">Bonjour **url cible de l’authentification unique** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4916-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c4916-186">d.</span><span class="sxs-lookup"><span data-stu-id="c4916-186">d.</span></span> <span data-ttu-id="c4916-187">Bonjour **Slo cible url** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4916-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="c4916-188">e.</span><span class="sxs-lookup"><span data-stu-id="c4916-188">e.</span></span> <span data-ttu-id="c4916-189">Ouvrez votre téléchargé **certificat (Base64)** dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez-la toohello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c4916-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="c4916-190">f.</span><span class="sxs-lookup"><span data-stu-id="c4916-190">f.</span></span> <span data-ttu-id="c4916-191">Cliquez sur hello **enregistrer les paramètres** bouton.</span><span class="sxs-lookup"><span data-stu-id="c4916-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="c4916-192">En regard de hello **paramètres d’authentification unique** section, copiez l’URL hello sous **url des métadonnées de fournisseur de Service**.</span><span class="sxs-lookup"><span data-stu-id="c4916-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="c4916-194">Ouvrez hello **lien URL de métadonnées** sous un document de métadonnées de navigateur vide toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="c4916-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="c4916-195">Puis copiez hello EntityDescriptor value(entityID) du fichier de hello et collez-le dans **identificateur** zone de texte dans **section reconnaît le domaine et les URL** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4916-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="c4916-197">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c4916-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4916-198">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c4916-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4916-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4916-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4916-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4916-201">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c4916-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c4916-203">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4916-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4916-204">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c4916-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4916-206">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c4916-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4916-208">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c4916-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4916-210">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4916-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4916-212">a.</span><span class="sxs-lookup"><span data-stu-id="c4916-212">a.</span></span> <span data-ttu-id="c4916-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4916-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4916-214">b.</span><span class="sxs-lookup"><span data-stu-id="c4916-214">b.</span></span> <span data-ttu-id="c4916-215">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4916-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4916-216">c.</span><span class="sxs-lookup"><span data-stu-id="c4916-216">c.</span></span> <span data-ttu-id="c4916-217">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c4916-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4916-218">d.</span><span class="sxs-lookup"><span data-stu-id="c4916-218">d.</span></span> <span data-ttu-id="c4916-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4916-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="c4916-220">Création d’un utilisateur de test Recognize</span><span class="sxs-lookup"><span data-stu-id="c4916-220">Creating a Recognize test user</span></span>

<span data-ttu-id="c4916-221">Dans l’ordre tooenable Azure AD les utilisateurs toolog à reconnaître, vous devez les configurer dans reconnaître.</span><span class="sxs-lookup"><span data-stu-id="c4916-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="c4916-222">Dans les cas de hello de reconnaître, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c4916-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="c4916-223">Cette application ne prend pas en charge l’approvisionnement SCIM, mais inclut une autre synchronisation de l’autre utilisateur qui approvisionne les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c4916-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="c4916-224">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4916-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4916-225">Connectez-vous à votre site d’entreprise Recognize en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c4916-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="c4916-226">Dans le coin supérieur droit hello, cliquez sur **Menu**.</span><span class="sxs-lookup"><span data-stu-id="c4916-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="c4916-227">Accédez trop**administrateur de l’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c4916-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="c4916-228">Dans le volet de navigation gauche hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c4916-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="c4916-229">Effectuer hello comme suit **synchronisation utilisateur** section.</span><span class="sxs-lookup"><span data-stu-id="c4916-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="c4916-230">![Nouvel utilisateur](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="c4916-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="c4916-231">a.</span><span class="sxs-lookup"><span data-stu-id="c4916-231">a.</span></span> <span data-ttu-id="c4916-232">Pour l’option **Synchronisation activée**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="c4916-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="c4916-233">b.</span><span class="sxs-lookup"><span data-stu-id="c4916-233">b.</span></span> <span data-ttu-id="c4916-234">Pour **Choisir le fournisseur de synchronisation**, sélectionnez **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="c4916-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="c4916-235">c.</span><span class="sxs-lookup"><span data-stu-id="c4916-235">c.</span></span> <span data-ttu-id="c4916-236">Cliquez sur **Run User Sync (Exécuter la synchronisation des utilisateurs)**.</span><span class="sxs-lookup"><span data-stu-id="c4916-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4916-237">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4916-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4916-238">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRecognize.</span><span class="sxs-lookup"><span data-stu-id="c4916-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c4916-240">**tooassign Britta Simon tooRecognize, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4916-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4916-241">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c4916-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c4916-243">Dans la liste des applications hello, sélectionnez **reconnaître**.</span><span class="sxs-lookup"><span data-stu-id="c4916-243">In hello applications list, select **Recognize**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="c4916-245">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c4916-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c4916-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c4916-247">Click **Add** button.</span></span> <span data-ttu-id="c4916-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c4916-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c4916-250">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c4916-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4916-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c4916-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4916-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c4916-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4916-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c4916-253">Testing single sign-on</span></span>

<span data-ttu-id="c4916-254">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c4916-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4916-255">Lorsque vous cliquez sur mosaïque de reconnaître hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour reconnaître application.</span><span class="sxs-lookup"><span data-stu-id="c4916-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="c4916-256">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4916-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4916-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c4916-257">Additional resources</span></span>

* [<span data-ttu-id="c4916-258">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4916-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4916-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c4916-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

