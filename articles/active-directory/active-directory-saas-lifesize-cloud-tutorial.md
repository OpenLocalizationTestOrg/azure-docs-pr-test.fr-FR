---
title: "Didacticiel : Intégration d’Azure Active Directory dans Lifesize Cloud | Documentation Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Lifesize Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="a98e7-103">Didacticiel : Intégration d’Azure Active Directory à Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="a98e7-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="a98e7-104">Dans ce didacticiel, vous apprendrez comment toointegrate Lifesize Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a98e7-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a98e7-105">Intégration Lifesize Cloud à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a98e7-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a98e7-106">Vous pouvez contrôler dans Azure AD qui a accès tooLifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="a98e7-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="a98e7-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLifesize Cloud (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a98e7-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a98e7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a98e7-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a98e7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98e7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a98e7-110">Prerequisites</span></span>

<span data-ttu-id="a98e7-111">tooconfigure intégration d’Azure AD avec Lifesize Cloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a98e7-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="a98e7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a98e7-113">Un abonnement Lifesize Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a98e7-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a98e7-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a98e7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a98e7-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a98e7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a98e7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a98e7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a98e7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a98e7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a98e7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a98e7-118">Scenario description</span></span>
<span data-ttu-id="a98e7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a98e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a98e7-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a98e7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a98e7-121">Ajout de Lifesize Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a98e7-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="a98e7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="a98e7-123">Ajout de Lifesize Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a98e7-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="a98e7-124">intégration de hello tooconfigure Lifesize cloud dans Azure AD, vous devez tooadd Lifesize Cloud à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a98e7-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a98e7-125">**tooadd Lifesize Cloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98e7-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a98e7-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a98e7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a98e7-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a98e7-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a98e7-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a98e7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a98e7-133">Dans la zone de recherche de hello, tapez **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="a98e7-135">Dans le volet de résultats hello, sélectionnez **Lifesize Cloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a98e7-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a98e7-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a98e7-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lifesize Cloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a98e7-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a98e7-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Lifesize Cloud est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a98e7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="a98e7-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Cloud de Lifesize hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a98e7-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="a98e7-141">Dans le Cloud de Lifesize, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a98e7-142">tooconfigure et test Azure AD l’authentification unique avec Lifesize Cloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a98e7-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a98e7-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a98e7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a98e7-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a98e7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a98e7-145">**[Création d’un utilisateur de test Lifesize Cloud](#creating-a-lifesize-cloud-test-user)**  -toohave un équivalent de Britta Simon dans Lifesize Cloud qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a98e7-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a98e7-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a98e7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a98e7-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a98e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a98e7-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a98e7-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="a98e7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="a98e7-150">**tooconfigure Azure AD single sign-on avec Lifesize nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98e7-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="a98e7-151">Bonjour portail Azure, sur hello **Lifesize Cloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a98e7-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a98e7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="a98e7-155">Sur hello **Lifesize Cloud domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a98e7-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="a98e7-157">a.</span><span class="sxs-lookup"><span data-stu-id="a98e7-157">a.</span></span> <span data-ttu-id="a98e7-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="a98e7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="a98e7-159">b.</span><span class="sxs-lookup"><span data-stu-id="a98e7-159">b.</span></span> <span data-ttu-id="a98e7-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="a98e7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="a98e7-161">Vérifiez **afficher les paramètres d’URL avancés**, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="a98e7-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="a98e7-163">Bonjour **état de relais** zone de texte, tapez une URL à l’aide de hello modèle :`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="a98e7-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="a98e7-164">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="a98e7-165">vous avez défini ces valeurs avec hello tooupdate réel URL de connexion, état du relais et d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="a98e7-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="a98e7-166">Contact [équipe de support Client de Cloud Lifesize](https://www.lifesize.com/support) tooget URL de connexion et les valeurs d’identificateur et vous pouvez obtenir la valeur d’état de relais à partir de la Configuration de l’authentification unique est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="a98e7-167">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a98e7-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="a98e7-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a98e7-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a98e7-171">Sur hello **Configuration du Cloud Lifesize** , cliquez sur **configurer le nuage Lifesize** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a98e7-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a98e7-172">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a98e7-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="a98e7-174">tooget l’authentification unique est configurée pour votre application, la connexion en hello application Lifesize Cloud avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a98e7-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="a98e7-175">En haut à droite hello sur votre nom, puis cliquez sur hello **paramètres avancés**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="a98e7-177">Bonjour, paramètres avancés cliquez maintenant sur hello **Configuration SSO** lien.</span><span class="sxs-lookup"><span data-stu-id="a98e7-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="a98e7-178">Il ouvre la page de Configuration SSO hello pour votre instance.</span><span class="sxs-lookup"><span data-stu-id="a98e7-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="a98e7-180">À présent configurer hello valeurs dans l’interface utilisateur de configuration de l’authentification unique hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="a98e7-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="a98e7-182">a.</span><span class="sxs-lookup"><span data-stu-id="a98e7-182">a.</span></span> <span data-ttu-id="a98e7-183">Dans **émetteur de fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a98e7-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a98e7-184">b.</span><span class="sxs-lookup"><span data-stu-id="a98e7-184">b.</span></span>  <span data-ttu-id="a98e7-185">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a98e7-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a98e7-186">c.</span><span class="sxs-lookup"><span data-stu-id="a98e7-186">c.</span></span> <span data-ttu-id="a98e7-187">Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a98e7-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="a98e7-188">d.</span><span class="sxs-lookup"><span data-stu-id="a98e7-188">d.</span></span> <span data-ttu-id="a98e7-189">Bonjour attribut SAML mappages pour la zone de texte hello prénom Entrez la valeur hello en tant que **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="a98e7-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="a98e7-190">e.</span><span class="sxs-lookup"><span data-stu-id="a98e7-190">e.</span></span> <span data-ttu-id="a98e7-191">Dans le mappage d’attribut SAML hello pour hello **nom** zone de texte Entrez la valeur hello en tant que **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="a98e7-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="a98e7-192">f.</span><span class="sxs-lookup"><span data-stu-id="a98e7-192">f.</span></span> <span data-ttu-id="a98e7-193">Dans le mappage d’attribut SAML hello pour hello **messagerie** zone de texte Entrez la valeur hello en tant que **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="a98e7-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="a98e7-194">configuration de hello toocheck vous pouvez cliquer sur hello **Test** bouton.</span><span class="sxs-lookup"><span data-stu-id="a98e7-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a98e7-195">Pour le test réussit, vous avez besoin d’Assistant de configuration toocomplete hello dans Azure AD et fournissent également des accès toousers ou des groupes autorisés à effectuer des tests de hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="a98e7-196">Activer hello SSO en vérifiant sur hello **activez SSO** bouton.</span><span class="sxs-lookup"><span data-stu-id="a98e7-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="a98e7-197">Cliquez maintenant sur hello **mise à jour** bouton afin que tous les paramètres de hello sont enregistrées.</span><span class="sxs-lookup"><span data-stu-id="a98e7-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="a98e7-198">Cette opération génère la valeur de RelayState hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="a98e7-199">Hello de copie RelayState valeur, qui est générée dans la zone de texte hello, collez-le dans hello **relais état** zone de texte sous **Lifesize Cloud domaine et les URL** section.</span><span class="sxs-lookup"><span data-stu-id="a98e7-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="a98e7-200">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a98e7-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a98e7-201">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a98e7-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a98e7-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a98e7-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="a98e7-204">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a98e7-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a98e7-206">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98e7-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a98e7-207">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a98e7-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a98e7-209">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a98e7-211">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a98e7-213">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a98e7-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a98e7-215">a.</span><span class="sxs-lookup"><span data-stu-id="a98e7-215">a.</span></span> <span data-ttu-id="a98e7-216">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a98e7-217">b.</span><span class="sxs-lookup"><span data-stu-id="a98e7-217">b.</span></span> <span data-ttu-id="a98e7-218">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a98e7-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a98e7-219">c.</span><span class="sxs-lookup"><span data-stu-id="a98e7-219">c.</span></span> <span data-ttu-id="a98e7-220">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a98e7-221">d.</span><span class="sxs-lookup"><span data-stu-id="a98e7-221">d.</span></span> <span data-ttu-id="a98e7-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="a98e7-223">Créer un utilisateur de test Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="a98e7-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="a98e7-224">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="a98e7-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="a98e7-225">Lifesize Cloud ne prend pas en charge l’approvisionnement automatique des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a98e7-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="a98e7-226">Après une authentification réussie à Azure AD, utilisateur de hello sera automatiquement configuré dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a98e7-227">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98e7-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a98e7-228">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="a98e7-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a98e7-230">**tooassign Britta Simon tooLifesize nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98e7-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="a98e7-231">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a98e7-233">Dans la liste des applications hello, sélectionnez **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="a98e7-235">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a98e7-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-237">Click **Add** button.</span></span> <span data-ttu-id="a98e7-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a98e7-240">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a98e7-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a98e7-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a98e7-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a98e7-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a98e7-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a98e7-243">Testing single sign-on</span></span>

<span data-ttu-id="a98e7-244">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a98e7-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a98e7-245">Lorsque vous cliquez sur hello Lifesize Cloud vignette Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="a98e7-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="a98e7-246">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a98e7-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a98e7-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a98e7-247">Additional resources</span></span>

* [<span data-ttu-id="a98e7-248">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a98e7-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a98e7-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a98e7-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

