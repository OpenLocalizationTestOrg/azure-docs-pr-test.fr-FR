---
title: "Didacticiel : Intégration d’Azure Active Directory à Adobe Creative Cloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Cloud créatifs d’Adobe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="09d6d-103">Didacticiel : Intégration d’Azure Active Directory à Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="09d6d-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="09d6d-104">Dans ce didacticiel, vous apprendrez comment toointegrate Adobe Creative Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09d6d-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09d6d-105">Intégration Cloud créatifs d’Adobe à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="09d6d-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="09d6d-106">Vous pouvez contrôler dans Azure AD qui a accès tooAdobe Cloud créatifs</span><span class="sxs-lookup"><span data-stu-id="09d6d-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="09d6d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAdobe Cloud créatifs (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09d6d-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="09d6d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="09d6d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09d6d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09d6d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="09d6d-110">Prerequisites</span></span>

<span data-ttu-id="09d6d-111">tooconfigure intégration d’Azure AD avec Cloud créatifs d’Adobe, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="09d6d-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="09d6d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09d6d-113">Un abonnement Adobe Creative Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="09d6d-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09d6d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="09d6d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09d6d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="09d6d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09d6d-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="09d6d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="09d6d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09d6d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09d6d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="09d6d-118">Scenario description</span></span>
<span data-ttu-id="09d6d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="09d6d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09d6d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="09d6d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09d6d-121">Ajout Cloud créatifs Adobe à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="09d6d-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="09d6d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="09d6d-123">Ajout Cloud créatifs Adobe à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="09d6d-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="09d6d-124">tooconfigure hello intégration de Cloud créatifs d’Adobe dans Azure AD, vous devez tooadd Cloud créatifs d’Adobe à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="09d6d-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="09d6d-125">**tooadd Adobe de Cloud créatifs à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="09d6d-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="09d6d-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="09d6d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="09d6d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="09d6d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="09d6d-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="09d6d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="09d6d-133">Dans la zone de recherche de hello, tapez **Cloud créatifs d’Adobe**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="09d6d-135">Dans le volet de résultats hello, sélectionnez **Cloud créatifs d’Adobe**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="09d6d-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="09d6d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="09d6d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Adobe Creative Cloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="09d6d-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09d6d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Cloud créatifs d’Adobe est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09d6d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="09d6d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Cloud de Creative Adobe hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="09d6d-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="09d6d-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le Cloud créatifs d’Adobe.</span><span class="sxs-lookup"><span data-stu-id="09d6d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="09d6d-142">tooconfigure et test Azure AD l’authentification unique avec Cloud créatifs d’Adobe, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="09d6d-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="09d6d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="09d6d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="09d6d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09d6d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09d6d-145">**[Création d’un utilisateur de test Cloud créatifs d’Adobe](#creating-an-adobe-creative-cloud-test-user)**  -toohave de Britta Simon dans Adobe Creative Cloud qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="09d6d-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="09d6d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="09d6d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09d6d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="09d6d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09d6d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="09d6d-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Cloud créatifs d’Adobe.</span><span class="sxs-lookup"><span data-stu-id="09d6d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="09d6d-150">**tooconfigure Azure AD l’authentification unique avec Cloud créatifs d’Adobe, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="09d6d-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="09d6d-151">Dans le portail de gestion Azure hello, sur hello **Cloud créatifs d’Adobe** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="09d6d-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="09d6d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="09d6d-155">Sur hello **Adobe Creative Cloud domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="09d6d-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="09d6d-157">a.</span><span class="sxs-lookup"><span data-stu-id="09d6d-157">a.</span></span> <span data-ttu-id="09d6d-158">Bonjour **identificateur** valeur hello de type en tant que zone de texte :`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="09d6d-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="09d6d-159">b.</span><span class="sxs-lookup"><span data-stu-id="09d6d-159">b.</span></span> <span data-ttu-id="09d6d-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="09d6d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="09d6d-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="09d6d-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="09d6d-162">Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="09d6d-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="09d6d-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="09d6d-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="09d6d-164">Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’équipe de support technique du Cloud créatifs d’Adobe toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="09d6d-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="09d6d-165">Sur hello **Adobe Creative Cloud domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="09d6d-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="09d6d-167">a.</span><span class="sxs-lookup"><span data-stu-id="09d6d-167">a.</span></span> <span data-ttu-id="09d6d-168">Cliquez sur hello **afficher les paramètres d’URL avancés** option</span><span class="sxs-lookup"><span data-stu-id="09d6d-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="09d6d-169">b.</span><span class="sxs-lookup"><span data-stu-id="09d6d-169">b.</span></span> <span data-ttu-id="09d6d-170">Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="09d6d-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="09d6d-171">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="09d6d-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="09d6d-173">Sur hello **Configuration du Cloud Creative Adobe** , cliquez sur **configurer le Cloud créatifs Adobe** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="09d6d-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="09d6d-174">Copiez hello **Id d’entité SAML** et **URL du Service SSO SAML** à partir de la section de référence rapide.</span><span class="sxs-lookup"><span data-stu-id="09d6d-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="09d6d-176">Dans une fenêtre de navigateur web, client de Cloud créatifs d’Adobe tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="09d6d-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="09d6d-177">Accédez trop**identité** hello du volet de navigation gauche et cliquez sur votre domaine.</span><span class="sxs-lookup"><span data-stu-id="09d6d-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="09d6d-178">Puis exécutez hello comme suit **l’authentification unique sur une Configuration requise** section.</span><span class="sxs-lookup"><span data-stu-id="09d6d-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="09d6d-179">![Paramètres](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="09d6d-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="09d6d-180">Cliquez sur **Parcourir** hello de tooupload téléchargé certificat auprès d’Azure AD trop**certificat IDP**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="09d6d-181">Bonjour **émetteur IDP** zone de texte, placez la valeur hello **Id d’entité SAML** que vous avez copié à partir de **configurer l’authentification** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="09d6d-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="09d6d-182">Bonjour **URL de connexion IDP** zone de texte, placez la valeur hello **URL du Service SSO SAML** que vous avez copié à partir de **configurer l’authentification** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="09d6d-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="09d6d-183">Sélectionnez **HTTP - Redirection** en tant que **Liaison IDP**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="09d6d-184">Sélectionnez **Adresse de messagerie** en tant que **Paramètre de connexion utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="09d6d-185">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="09d6d-185">Click **Save** button.</span></span>

15. <span data-ttu-id="09d6d-186">tableau de bord Hello présente maintenant hello XML **« Télécharger des métadonnées »** fichier.</span><span class="sxs-lookup"><span data-stu-id="09d6d-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="09d6d-187">Il contient les URL EntityDescriptor et AssertionConsumerService d’Adobe.</span><span class="sxs-lookup"><span data-stu-id="09d6d-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="09d6d-188">Veuillez ouvrir le fichier de hello et configurez-les dans hello application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09d6d-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="09d6d-191">a.</span><span class="sxs-lookup"><span data-stu-id="09d6d-191">a.</span></span> <span data-ttu-id="09d6d-192">Hello d’utilisation EntityDescriptor valeur Adobe fourni pour **identificateur** sur hello **configurer les paramètres de l’application** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="09d6d-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="09d6d-193">b.</span><span class="sxs-lookup"><span data-stu-id="09d6d-193">b.</span></span> <span data-ttu-id="09d6d-194">Hello d’utilisation AssertionConsumerService valeur Adobe fourni pour **URL de réponse** sur hello **configurer les paramètres de l’application** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="09d6d-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="09d6d-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="09d6d-196">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09d6d-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="09d6d-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="09d6d-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="09d6d-199">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="09d6d-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09d6d-201">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="09d6d-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09d6d-203">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="09d6d-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09d6d-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="09d6d-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09d6d-207">a.</span><span class="sxs-lookup"><span data-stu-id="09d6d-207">a.</span></span> <span data-ttu-id="09d6d-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09d6d-209">b.</span><span class="sxs-lookup"><span data-stu-id="09d6d-209">b.</span></span> <span data-ttu-id="09d6d-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="09d6d-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09d6d-211">c.</span><span class="sxs-lookup"><span data-stu-id="09d6d-211">c.</span></span> <span data-ttu-id="09d6d-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="09d6d-213">d.</span><span class="sxs-lookup"><span data-stu-id="09d6d-213">d.</span></span> <span data-ttu-id="09d6d-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="09d6d-215">Création d’un utilisateur d’Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="09d6d-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="09d6d-216">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans le Cloud créatifs d’Adobe, vous devez les configurer dans le Cloud créatifs d’Adobe.</span><span class="sxs-lookup"><span data-stu-id="09d6d-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="09d6d-217">Dans les cas de hello de Cloud créatifs d’Adobe, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="09d6d-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="09d6d-218">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="09d6d-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="09d6d-219">Ouvrez une session dans tooyour site d’entreprise Cloud créatifs d’Adobe en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="09d6d-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="09d6d-220">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-220">Click **People**.</span></span>

    <span data-ttu-id="09d6d-221">![Personnes](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="09d6d-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="09d6d-222">Cliquez sur **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-222">Click **Invite User**.</span></span>

    <span data-ttu-id="09d6d-223">![Inviter des utilisateurs](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "inviter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="09d6d-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="09d6d-224">Sur hello **inviter des personnes** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="09d6d-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="09d6d-225">![Inviter des personnes](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "inviter des personnes")</span><span class="sxs-lookup"><span data-stu-id="09d6d-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="09d6d-226">a.</span><span class="sxs-lookup"><span data-stu-id="09d6d-226">a.</span></span> <span data-ttu-id="09d6d-227">Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09d6d-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="09d6d-228">b.</span><span class="sxs-lookup"><span data-stu-id="09d6d-228">b.</span></span> <span data-ttu-id="09d6d-229">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="09d6d-230">titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="09d6d-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="09d6d-231">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="09d6d-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="09d6d-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooAdobe accès Cloud créatifs.</span><span class="sxs-lookup"><span data-stu-id="09d6d-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="09d6d-234">**tooassign Britta Simon tooAdobe Cloud créatifs, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="09d6d-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="09d6d-235">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="09d6d-237">Dans la liste des applications hello, sélectionnez **Cloud créatifs d’Adobe**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="09d6d-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="09d6d-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-241">Click **Add** button.</span></span> <span data-ttu-id="09d6d-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="09d6d-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="09d6d-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="09d6d-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09d6d-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="09d6d-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="09d6d-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="09d6d-247">Testing single sign-on</span></span>

<span data-ttu-id="09d6d-248">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="09d6d-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="09d6d-249">Lorsque vous cliquez sur mosaïque Cloud créatifs d’Adobe hello hello volet d’accès, vous devez obtenir l’application de Cloud créatifs d’Adobe tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="09d6d-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="09d6d-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="09d6d-250">Additional resources</span></span>

* [<span data-ttu-id="09d6d-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09d6d-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09d6d-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="09d6d-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png