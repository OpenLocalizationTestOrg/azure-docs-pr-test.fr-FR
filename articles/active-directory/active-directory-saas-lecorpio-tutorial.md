---
title: "Didacticiel : Intégration d’Azure Active Directory à Lecorpio | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Lecorpio."
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
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="41217-103">Didacticiel : Intégration d’Azure Active Directory à Lecorpio</span><span class="sxs-lookup"><span data-stu-id="41217-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="41217-104">Dans ce didacticiel, vous apprendrez comment toointegrate Lecorpio avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41217-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41217-105">Intégration Lecorpio à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="41217-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="41217-106">Vous pouvez contrôler dans Azure AD qui a accès tooLecorpio</span><span class="sxs-lookup"><span data-stu-id="41217-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="41217-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLecorpio (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41217-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="41217-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="41217-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41217-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41217-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="41217-110">Prerequisites</span></span>

<span data-ttu-id="41217-111">tooconfigure intégration d’Azure AD avec Lecorpio, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="41217-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="41217-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41217-113">Un abonnement Lecorpio pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="41217-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41217-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="41217-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41217-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="41217-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41217-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="41217-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41217-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41217-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41217-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="41217-118">Scenario description</span></span>
<span data-ttu-id="41217-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="41217-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41217-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="41217-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41217-121">Ajout de Lecorpio à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="41217-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="41217-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="41217-123">Ajout de Lecorpio à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="41217-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="41217-124">intégration de hello tooconfigure de Lecorpio dans Azure AD, vous devez tooadd Lecorpio à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="41217-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="41217-125">**tooadd Lecorpio à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41217-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="41217-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="41217-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41217-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="41217-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="41217-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="41217-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="41217-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="41217-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="41217-133">Dans la zone de recherche de hello, tapez **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="41217-133">In hello search box, type **Lecorpio**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="41217-135">Dans le volet de résultats hello, sélectionnez **Lecorpio**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="41217-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41217-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41217-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lecorpio pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="41217-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="41217-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Lecorpio est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41217-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="41217-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Lecorpio doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="41217-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="41217-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="41217-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="41217-142">tooconfigure et test Azure AD l’authentification unique avec Lecorpio, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="41217-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="41217-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="41217-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="41217-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41217-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41217-145">**[Création d’un utilisateur de test Lecorpio](#creating-a-lecorpio-test-user)**  -toohave un équivalent de Britta Simon dans Lecorpio est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41217-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="41217-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="41217-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41217-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="41217-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41217-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41217-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="41217-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="41217-150">**tooconfigure Azure AD single sign-on avec Lecorpio, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41217-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="41217-151">Bonjour portail Azure, sur hello **Lecorpio** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="41217-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="41217-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="41217-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="41217-155">Sur hello **Lecorpio domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="41217-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="41217-157">a.</span><span class="sxs-lookup"><span data-stu-id="41217-157">a.</span></span> <span data-ttu-id="41217-158">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="41217-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="41217-159">b.</span><span class="sxs-lookup"><span data-stu-id="41217-159">b.</span></span> <span data-ttu-id="41217-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="41217-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41217-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="41217-161">These values are not hello real.</span></span> <span data-ttu-id="41217-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="41217-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="41217-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="41217-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="41217-164">Contact [équipe de support Client de Lecorpio](mailto:info@lecorpio.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="41217-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="41217-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="41217-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="41217-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="41217-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41217-169">tooconfigure l’authentification unique sur **Lecorpio** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="41217-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="41217-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="41217-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="41217-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="41217-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="41217-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41217-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41217-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="41217-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="41217-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="41217-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41217-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="41217-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="41217-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41217-179">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="41217-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41217-181">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="41217-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41217-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="41217-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41217-185">a.</span><span class="sxs-lookup"><span data-stu-id="41217-185">a.</span></span> <span data-ttu-id="41217-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41217-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41217-187">b.</span><span class="sxs-lookup"><span data-stu-id="41217-187">b.</span></span> <span data-ttu-id="41217-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="41217-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41217-189">c.</span><span class="sxs-lookup"><span data-stu-id="41217-189">c.</span></span> <span data-ttu-id="41217-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="41217-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="41217-191">d.</span><span class="sxs-lookup"><span data-stu-id="41217-191">d.</span></span> <span data-ttu-id="41217-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="41217-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="41217-193">Création d’un utilisateur de test Lecorpio</span><span class="sxs-lookup"><span data-stu-id="41217-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="41217-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="41217-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="41217-195">Contact [équipe de support Client de Lecorpio](mailto:info@lecorpio.com) utilisateurs hello tooadd hello Lecorpio application.</span><span class="sxs-lookup"><span data-stu-id="41217-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="41217-196">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="41217-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="41217-197">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLecorpio.</span><span class="sxs-lookup"><span data-stu-id="41217-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="41217-199">**tooassign Britta Simon tooLecorpio, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41217-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="41217-200">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="41217-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="41217-202">Dans la liste des applications hello, sélectionnez **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="41217-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="41217-204">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="41217-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="41217-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="41217-206">Click **Add** button.</span></span> <span data-ttu-id="41217-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="41217-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="41217-209">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="41217-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="41217-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="41217-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41217-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="41217-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41217-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="41217-212">Testing single sign-on</span></span>

<span data-ttu-id="41217-213">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="41217-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="41217-214">Lorsque vous cliquez sur mosaïque Lecorpio hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Lecorpio application.</span><span class="sxs-lookup"><span data-stu-id="41217-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41217-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="41217-215">Additional resources</span></span>

* [<span data-ttu-id="41217-216">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41217-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41217-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="41217-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

