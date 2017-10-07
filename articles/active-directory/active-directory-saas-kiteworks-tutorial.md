---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kiteworks | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="cb880-103">Didacticiel : Intégration d’Azure Active Directory à Kiteworks</span><span class="sxs-lookup"><span data-stu-id="cb880-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="cb880-104">Dans ce didacticiel, vous apprendrez comment toointegrate Kiteworks avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb880-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb880-105">Intégration Kiteworks à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cb880-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb880-106">Vous pouvez contrôler dans Azure AD qui a accès tooKiteworks</span><span class="sxs-lookup"><span data-stu-id="cb880-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="cb880-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKiteworks (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb880-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cb880-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb880-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb880-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb880-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cb880-110">Prerequisites</span></span>

<span data-ttu-id="cb880-111">tooconfigure intégration d’Azure AD avec Kiteworks, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cb880-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="cb880-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb880-113">Un abonnement Kiteworks pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="cb880-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb880-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cb880-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb880-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="cb880-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb880-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cb880-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb880-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb880-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb880-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cb880-118">Scenario description</span></span>
<span data-ttu-id="cb880-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cb880-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb880-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="cb880-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb880-121">Ajout de Kiteworks à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cb880-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="cb880-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="cb880-123">Ajout de Kiteworks à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cb880-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="cb880-124">intégration de hello tooconfigure de Kiteworks dans Azure AD, vous devez tooadd Kiteworks à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cb880-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb880-125">**tooadd Kiteworks à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb880-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb880-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cb880-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb880-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cb880-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb880-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cb880-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cb880-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cb880-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cb880-133">Dans la zone de recherche de hello, tapez **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="cb880-133">In hello search box, type **Kiteworks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="cb880-135">Dans le volet de résultats hello, sélectionnez **Kiteworks**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cb880-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb880-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb880-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kiteworks avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cb880-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb880-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Kiteworks est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb880-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="cb880-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Kiteworks doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="cb880-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="cb880-141">Dans Kiteworks, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="cb880-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cb880-142">tooconfigure et test Azure AD l’authentification unique avec Kiteworks, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="cb880-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb880-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cb880-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb880-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb880-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb880-145">**[Création d’un utilisateur de test Kiteworks](#creating-a-kiteworks-test-user)**  -toohave un équivalent de Britta Simon dans Kiteworks est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cb880-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb880-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cb880-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb880-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="cb880-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb880-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb880-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="cb880-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="cb880-150">**tooconfigure Azure AD single sign-on avec Kiteworks, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb880-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb880-151">Bonjour portail Azure, sur hello **Kiteworks** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cb880-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cb880-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cb880-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="cb880-155">Sur hello **Kiteworks domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb880-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="cb880-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb880-157">a.</span></span> <span data-ttu-id="cb880-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="cb880-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="cb880-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb880-159">b.</span></span> <span data-ttu-id="cb880-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="cb880-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb880-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="cb880-161">These values are not real.</span></span> <span data-ttu-id="cb880-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="cb880-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cb880-163">Contact [équipe de support Client de Kiteworks](http://accellion.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="cb880-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="cb880-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cb880-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="cb880-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cb880-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb880-168">Sur hello **Kiteworks Configuration** , cliquez sur **Kiteworks de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="cb880-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb880-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="cb880-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="cb880-171">Site d’entreprise tooyour Kiteworks ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cb880-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="cb880-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="cb880-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="cb880-174">Bonjour **authentification et autorisation** , cliquez sur **le programme d’installation de l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cb880-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="cb880-176">Sur la page de configuration de l’authentification unique de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb880-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="cb880-178">a.</span><span class="sxs-lookup"><span data-stu-id="cb880-178">a.</span></span> <span data-ttu-id="cb880-179">Sélectionnez **Authenticate via SSO**.</span><span class="sxs-lookup"><span data-stu-id="cb880-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="cb880-180">b.</span><span class="sxs-lookup"><span data-stu-id="cb880-180">b.</span></span> <span data-ttu-id="cb880-181">Sélectionnez **Initiate AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="cb880-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="cb880-182">c.</span><span class="sxs-lookup"><span data-stu-id="cb880-182">c.</span></span> <span data-ttu-id="cb880-183">Bonjour **IDP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cb880-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="cb880-184">d.</span><span class="sxs-lookup"><span data-stu-id="cb880-184">d.</span></span> <span data-ttu-id="cb880-185">Bonjour **unique Sign-On URL du Service** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cb880-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb880-186">e.</span><span class="sxs-lookup"><span data-stu-id="cb880-186">e.</span></span> <span data-ttu-id="cb880-187">Bonjour **URL de Service de déconnexion unique** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cb880-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb880-188">f.</span><span class="sxs-lookup"><span data-stu-id="cb880-188">f.</span></span> <span data-ttu-id="cb880-189">Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu et le coller ensuite dans hello **certificat de clé publique RSA** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="cb880-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="cb880-190">g.</span><span class="sxs-lookup"><span data-stu-id="cb880-190">g.</span></span> <span data-ttu-id="cb880-191">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cb880-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cb880-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="cb880-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb880-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="cb880-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb880-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb880-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb880-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb880-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="cb880-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cb880-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb880-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb880-199">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cb880-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb880-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cb880-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb880-203">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="cb880-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb880-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb880-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb880-207">a.</span><span class="sxs-lookup"><span data-stu-id="cb880-207">a.</span></span> <span data-ttu-id="cb880-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb880-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb880-209">b.</span><span class="sxs-lookup"><span data-stu-id="cb880-209">b.</span></span> <span data-ttu-id="cb880-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb880-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb880-211">c.</span><span class="sxs-lookup"><span data-stu-id="cb880-211">c.</span></span> <span data-ttu-id="cb880-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cb880-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb880-213">d.</span><span class="sxs-lookup"><span data-stu-id="cb880-213">d.</span></span> <span data-ttu-id="cb880-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb880-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="cb880-215">Création d’un utilisateur de test Kiteworks</span><span class="sxs-lookup"><span data-stu-id="cb880-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="cb880-216">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="cb880-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="cb880-217">Kiteworks prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="cb880-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="cb880-218">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="cb880-218">There is no action item for you in this section.</span></span> <span data-ttu-id="cb880-219">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Kitewors s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="cb880-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="cb880-220">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [Kiteworks l’équipe de support](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="cb880-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb880-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb880-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb880-222">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKiteworks.</span><span class="sxs-lookup"><span data-stu-id="cb880-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cb880-224">**tooassign Britta Simon tooKiteworks, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cb880-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb880-225">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cb880-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cb880-227">Dans la liste des applications hello, sélectionnez **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="cb880-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="cb880-229">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cb880-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cb880-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cb880-231">Click **Add** button.</span></span> <span data-ttu-id="cb880-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cb880-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cb880-234">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="cb880-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb880-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cb880-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb880-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cb880-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb880-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cb880-237">Testing single sign-on</span></span>

<span data-ttu-id="cb880-238">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="cb880-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="cb880-239">Lorsque vous cliquez sur hello Kiteworks vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Kiteworks application.</span><span class="sxs-lookup"><span data-stu-id="cb880-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb880-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cb880-240">Additional resources</span></span>

* [<span data-ttu-id="cb880-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb880-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb880-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cb880-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

