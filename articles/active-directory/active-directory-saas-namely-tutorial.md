---
title: "Didacticiel : Intégration d’Azure Active Directory à Namely | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory, à savoir."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="d7fb6-103">Didacticiel : Intégration d’Azure Active Directory à Namely</span><span class="sxs-lookup"><span data-stu-id="d7fb6-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="d7fb6-104">Dans ce didacticiel, vous apprendrez comment toointegrate à savoir avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7fb6-105">Intégration à savoir à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7fb6-106">Vous pouvez contrôler dans Azure AD qui a accès tooNamely</span><span class="sxs-lookup"><span data-stu-id="d7fb6-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="d7fb6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNamely (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7fb6-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7fb6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d7fb6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7fb6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7fb6-110">Prerequisites</span></span>

<span data-ttu-id="d7fb6-111">intégration tooconfigure Azure AD avec, à savoir, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="d7fb6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7fb6-113">Un abonnement Namely pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d7fb6-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7fb6-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7fb6-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7fb6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7fb6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7fb6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d7fb6-118">Scenario description</span></span>
<span data-ttu-id="d7fb6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7fb6-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7fb6-121">Ajout à savoir à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d7fb6-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="d7fb6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="d7fb6-123">Ajout à savoir à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d7fb6-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="d7fb6-124">tooconfigure hello intégration d’à savoir dans Azure AD, vous devez tooadd à savoir à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7fb6-125">**tooadd, à savoir à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7fb6-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7fb6-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d7fb6-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d7fb6-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d7fb6-133">Dans la zone de recherche de hello, tapez **à savoir**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-133">In hello search box, type **Namely**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="d7fb6-135">Dans le volet de résultats hello, sélectionnez **à savoir**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7fb6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7fb6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Namely, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d7fb6-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7fb6-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello est à savoir tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="d7fb6-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans hello doit à savoir toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="d7fb6-141">Dans, à savoir, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d7fb6-142">tooconfigure et test Azure AD l’authentification unique avec, à savoir, vous doivent hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7fb6-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7fb6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7fb6-145">**[Création d’un utilisateur de test à savoir](#creating-a-namely-test-user)**  -toohave un homologue de Britta Simon dans à savoir qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7fb6-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7fb6-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7fb6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7fb6-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application à savoir.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="d7fb6-150">**tooconfigure Azure AD single sign-on avec, à savoir, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7fb6-151">Bonjour portail Azure, sur hello **à savoir** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d7fb6-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="d7fb6-155">Sur hello **à savoir le domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="d7fb6-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-157">a.</span></span> <span data-ttu-id="d7fb6-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="d7fb6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="d7fb6-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-159">b.</span></span> <span data-ttu-id="d7fb6-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="d7fb6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7fb6-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-161">These values are not real.</span></span> <span data-ttu-id="d7fb6-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d7fb6-163">Contact [équipe de support Client à savoir](https://www.namely.com/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="d7fb6-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="d7fb6-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d7fb6-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7fb6-168">Sur hello **à savoir Configuration** , cliquez sur **configurer à savoir** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d7fb6-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="d7fb6-171">Dans une autre fenêtre de navigateur, connectez-vous tooyour à savoir site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="d7fb6-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="d7fb6-174">Cliquez sur hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-174">Click hello **Settings** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="d7fb6-176">Cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-176">Click **SAML**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="d7fb6-178">Sur hello **paramètres SAML** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="d7fb6-180">a.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-180">a.</span></span> <span data-ttu-id="d7fb6-181">Cliquez sur **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="d7fb6-182">b.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-182">b.</span></span> <span data-ttu-id="d7fb6-183">Bonjour **url SSO fournisseur d’identité** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d7fb6-184">c.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-184">c.</span></span> <span data-ttu-id="d7fb6-185">Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu et le coller ensuite dans hello **certificat de fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="d7fb6-186">d.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-186">d.</span></span> <span data-ttu-id="d7fb6-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d7fb6-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d7fb6-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d7fb6-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d7fb6-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7fb6-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7fb6-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d7fb6-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7fb6-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7fb6-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7fb6-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7fb6-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7fb6-203">a.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-203">a.</span></span> <span data-ttu-id="d7fb6-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7fb6-205">b.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-205">b.</span></span> <span data-ttu-id="d7fb6-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7fb6-207">c.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-207">c.</span></span> <span data-ttu-id="d7fb6-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d7fb6-209">d.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-209">d.</span></span> <span data-ttu-id="d7fb6-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="d7fb6-211">Création d’un utilisateur de test Namely</span><span class="sxs-lookup"><span data-stu-id="d7fb6-211">Creating a Namely test user</span></span>

<span data-ttu-id="d7fb6-212">objectif Hello de cette section est toocreate un utilisateur nommé Britta Simon dans, à savoir.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="d7fb6-213">**toocreate un utilisateur nommé Britta Simon dans, à savoir, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7fb6-214">À savoir authentification tooyour l'entreprise site en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="d7fb6-215">Dans la barre d’outils de hello en haut de hello, cliquez sur **personnes**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="d7fb6-217">Cliquez sur hello **répertoire** onglet.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-217">Click hello **Directory** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="d7fb6-219">Cliquez sur **Add New Person**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-219">Click **Add New Person**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="d7fb6-221">Sur hello **ajouter une nouvelle personne** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7fb6-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="d7fb6-222">a.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-222">a.</span></span> <span data-ttu-id="d7fb6-223">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="d7fb6-224">b.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-224">b.</span></span> <span data-ttu-id="d7fb6-225">Bonjour **nom** zone de texte, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="d7fb6-226">c.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-226">c.</span></span> <span data-ttu-id="d7fb6-227">Bonjour **messagerie** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7fb6-228">d.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-228">d.</span></span> <span data-ttu-id="d7fb6-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d7fb6-230">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7fb6-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d7fb6-231">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNamely.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d7fb6-233">**tooassign Britta Simon tooNamely, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7fb6-234">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d7fb6-236">Dans la liste des applications hello, sélectionnez **à savoir**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-236">In hello applications list, select **Namely**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="d7fb6-238">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d7fb6-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-240">Click **Add** button.</span></span> <span data-ttu-id="d7fb6-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d7fb6-243">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d7fb6-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7fb6-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7fb6-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d7fb6-246">Testing single sign-on</span></span>

<span data-ttu-id="d7fb6-247">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7fb6-248">Lorsque vous cliquez sur hello à savoir vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour à savoir application</span><span class="sxs-lookup"><span data-stu-id="d7fb6-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7fb6-249">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d7fb6-249">Additional resources</span></span>

* [<span data-ttu-id="d7fb6-250">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7fb6-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7fb6-251">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d7fb6-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

