---
title: "Didacticiel : Intégration d’Azure Active Directory avec SECURE DELIVER - Secure | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de sécuriser la remise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 13699a9abb8be24054b0810a8178cd5ef170c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="34474-103">Didacticiel : Intégration de SECURE DELIVER à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34474-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="34474-104">Dans ce didacticiel, vous apprendrez comment sécuriser des toointegrate livrer avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34474-104">In this tutorial, you learn how toointegrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34474-105">Intégration de sécuriser les remettre à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="34474-105">Integrating SECURE DELIVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34474-106">Vous pouvez contrôler dans Azure AD qui a accès tooSECURE remise</span><span class="sxs-lookup"><span data-stu-id="34474-106">You can control in Azure AD who has access tooSECURE DELIVER</span></span>
- <span data-ttu-id="34474-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSECURE livrer (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-107">You can enable your users tooautomatically get signed-on tooSECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34474-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="34474-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34474-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34474-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34474-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="34474-110">Prerequisites</span></span>

<span data-ttu-id="34474-111">tooconfigure intégration d’Azure AD avec sécuriser la remise, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="34474-111">tooconfigure Azure AD integration with SECURE DELIVER, you need hello following items:</span></span>

- <span data-ttu-id="34474-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34474-113">Un abonnement SECURE DELIVER pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="34474-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34474-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="34474-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34474-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="34474-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34474-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="34474-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34474-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34474-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34474-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="34474-118">Scenario description</span></span>
<span data-ttu-id="34474-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="34474-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34474-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="34474-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34474-121">Ajout de sécuriser les remettre à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="34474-121">Adding SECURE DELIVER from hello gallery</span></span>
2. <span data-ttu-id="34474-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-hello-gallery"></a><span data-ttu-id="34474-123">Ajout de sécuriser les remettre à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="34474-123">Adding SECURE DELIVER from hello gallery</span></span>
<span data-ttu-id="34474-124">tooconfigure hello intégration de sécuriser les remettre dans Azure AD, vous devez tooadd SECURE remettre à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="34474-124">tooconfigure hello integration of SECURE DELIVER into Azure AD, you need tooadd SECURE DELIVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34474-125">**tooadd sécurisé remettre à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34474-125">**tooadd SECURE DELIVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34474-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="34474-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34474-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="34474-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34474-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="34474-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="34474-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="34474-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="34474-133">Dans la zone de recherche de hello, tapez **SECURE remettre**.</span><span class="sxs-lookup"><span data-stu-id="34474-133">In hello search box, type **SECURE DELIVER**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_search.png)

5. <span data-ttu-id="34474-135">Dans le volet de résultats hello, sélectionnez **SECURE remettre**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="34474-135">In hello results panel, select **SECURE DELIVER**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34474-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34474-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SECURE DELIVER sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="34474-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34474-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello sécuriser la remise est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34474-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SECURE DELIVER is tooa user in Azure AD.</span></span> <span data-ttu-id="34474-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SECURE remettre doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="34474-140">In other words, a link relationship between an Azure AD user and hello related user in SECURE DELIVER needs toobe established.</span></span>

<span data-ttu-id="34474-141">Dans SECURE remettre, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="34474-141">In SECURE DELIVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34474-142">tooconfigure et test Azure AD l’authentification unique avec sécuriser la remise, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="34474-142">tooconfigure and test Azure AD single sign-on with SECURE DELIVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34474-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="34474-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34474-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34474-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34474-145">**[Création d’un utilisateur de test sécurisé remettre](#creating-a-secure-deliver-test-user)**  -toohave un équivalent de Britta Simon dans SECURE remettre qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34474-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - toohave a counterpart of Britta Simon in SECURE DELIVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34474-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="34474-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34474-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="34474-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34474-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34474-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de sécuriser la remise.</span><span class="sxs-lookup"><span data-stu-id="34474-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="34474-150">**tooconfigure Azure AD single sign-on avec SECURE remettre, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34474-150">**tooconfigure Azure AD single sign-on with SECURE DELIVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="34474-151">Bonjour portail Azure, sur hello **SECURE remettre** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="34474-151">In hello Azure portal, on hello **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="34474-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="34474-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

3. <span data-ttu-id="34474-155">Sur hello **sécuriser le domaine de fournir et URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="34474-155">On hello **SECURE DELIVER Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="34474-157">a.</span><span class="sxs-lookup"><span data-stu-id="34474-157">a.</span></span> <span data-ttu-id="34474-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="34474-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="34474-159">b.</span><span class="sxs-lookup"><span data-stu-id="34474-159">b.</span></span> <span data-ttu-id="34474-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="34474-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34474-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="34474-161">These values are not real.</span></span> <span data-ttu-id="34474-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="34474-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="34474-163">Contact [équipe de support technique de sécuriser le Client de remettre](mailto:iw-sd-support@fujifilm.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="34474-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="34474-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="34474-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

5. <span data-ttu-id="34474-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="34474-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-securedeliver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34474-168">Sur hello **sécuriser la Configuration remettre** , cliquez sur **configurer SECURE remettre** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="34474-168">On hello **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="34474-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="34474-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_configure.png) 

7. <span data-ttu-id="34474-171">tooconfigure l’authentification unique sur **SECURE remettre** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[sécurisée de fournir une équipe de support](mailto:iw-sd-support@fujifilm.com).</span><span class="sxs-lookup"><span data-stu-id="34474-171">tooconfigure single sign-on on **SECURE DELIVER** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="34474-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="34474-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="34474-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="34474-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34474-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="34474-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34474-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34474-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34474-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="34474-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="34474-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="34474-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34474-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34474-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="34474-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34474-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="34474-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34474-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="34474-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34474-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="34474-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34474-188">a.</span><span class="sxs-lookup"><span data-stu-id="34474-188">a.</span></span> <span data-ttu-id="34474-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34474-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34474-190">b.</span><span class="sxs-lookup"><span data-stu-id="34474-190">b.</span></span> <span data-ttu-id="34474-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34474-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34474-192">c.</span><span class="sxs-lookup"><span data-stu-id="34474-192">c.</span></span> <span data-ttu-id="34474-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="34474-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34474-194">d.</span><span class="sxs-lookup"><span data-stu-id="34474-194">d.</span></span> <span data-ttu-id="34474-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="34474-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="34474-196">Création d’un utilisateur de test SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="34474-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="34474-197">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans SECURE remettre.</span><span class="sxs-lookup"><span data-stu-id="34474-197">hello objective of this section is toocreate a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="34474-198">Travailler avec [sécurisée de fournir une équipe de support](mailto:iw-sd-support@fujifilm.com) utilisateurs hello tooadd hello sécurisée de fournir un compte.</span><span class="sxs-lookup"><span data-stu-id="34474-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) tooadd hello users in hello SECURE DELIVER account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34474-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="34474-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34474-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSECURE livrer.</span><span class="sxs-lookup"><span data-stu-id="34474-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSECURE DELIVER.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="34474-202">**tooassign Britta Simon tooSECURE remettre, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="34474-202">**tooassign Britta Simon tooSECURE DELIVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="34474-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="34474-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="34474-205">Dans la liste des applications hello, sélectionnez **SECURE remettre**.</span><span class="sxs-lookup"><span data-stu-id="34474-205">In hello applications list, select **SECURE DELIVER**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_app.png) 

3. <span data-ttu-id="34474-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="34474-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="34474-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="34474-209">Click **Add** button.</span></span> <span data-ttu-id="34474-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="34474-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="34474-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="34474-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34474-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="34474-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34474-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="34474-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34474-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="34474-215">Testing single sign-on</span></span>

<span data-ttu-id="34474-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="34474-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="34474-217">Lorsque vous cliquez sur hello sécuriser la remise de vignette dans hello volet d’accès, vous devez obtenir l’application de sécuriser les remettre automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="34474-217">When you click hello SECURE DELIVER tile in hello Access Panel, you should get automatically signed-on tooyour SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34474-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="34474-218">Additional resources</span></span>

* [<span data-ttu-id="34474-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34474-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34474-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="34474-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png

