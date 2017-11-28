---
title: "Didacticiel : Intégration d’Azure Active Directory dans 360 Online | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et 360 en ligne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 413e4e2c41336f99e1999857c788c5dac15be4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="8c96b-103">Didacticiel : Intégration d’Azure Active Directory à 360 Online</span><span class="sxs-lookup"><span data-stu-id="8c96b-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="8c96b-104">Dans ce didacticiel, vous apprendrez comment toointegrate 360 en ligne avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c96b-104">In this tutorial, you learn how toointegrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c96b-105">Intégration de 360 Online avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8c96b-105">Integrating 360 Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c96b-106">Vous pouvez contrôler dans Azure AD qui a accès too360 en ligne</span><span class="sxs-lookup"><span data-stu-id="8c96b-106">You can control in Azure AD who has access too360 Online</span></span>
- <span data-ttu-id="8c96b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté too360 en ligne (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-107">You can enable your users tooautomatically get signed-on too360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c96b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8c96b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8c96b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c96b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c96b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8c96b-110">Prerequisites</span></span>

<span data-ttu-id="8c96b-111">tooconfigure intégration d’Azure AD avec l’option Online 360, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8c96b-111">tooconfigure Azure AD integration with 360 Online, you need hello following items:</span></span>

- <span data-ttu-id="8c96b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c96b-113">Un abonnement 360 Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8c96b-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c96b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8c96b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c96b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8c96b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c96b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8c96b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c96b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c96b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c96b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8c96b-118">Scenario description</span></span>
<span data-ttu-id="8c96b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8c96b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c96b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8c96b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c96b-121">Ajout de 360 en ligne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8c96b-121">Adding 360 Online from hello gallery</span></span>
2. <span data-ttu-id="8c96b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-hello-gallery"></a><span data-ttu-id="8c96b-123">Ajout de 360 en ligne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8c96b-123">Adding 360 Online from hello gallery</span></span>
<span data-ttu-id="8c96b-124">intégration de hello tooconfigure de 360 en ligne dans Azure AD, vous devez tooadd 360 en ligne à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8c96b-124">tooconfigure hello integration of 360 Online into Azure AD, you need tooadd 360 Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c96b-125">**tooadd 360 à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c96b-125">**tooadd 360 Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c96b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8c96b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c96b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c96b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8c96b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8c96b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8c96b-133">Dans la zone de recherche de hello, tapez **Online 360**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-133">In hello search box, type **360 Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="8c96b-135">Dans le volet de résultats hello, sélectionnez **Online 360**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8c96b-135">In hello results panel, select **360 Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c96b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c96b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 360 Online, avec un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8c96b-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8c96b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello 360 en ligne est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c96b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 360 Online is tooa user in Azure AD.</span></span> <span data-ttu-id="8c96b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans 360 Online doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8c96b-140">In other words, a link relationship between an Azure AD user and hello related user in 360 Online needs toobe established.</span></span>

<span data-ttu-id="8c96b-141">Dans la ligne 360, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8c96b-141">In 360 Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8c96b-142">tooconfigure et test Azure AD l’authentification unique avec l’option Online 360, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8c96b-142">tooconfigure and test Azure AD single sign-on with 360 Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c96b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8c96b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c96b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c96b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c96b-145">**[Création d’un utilisateur de test en ligne 360](#creating-a-360-online-test-user)**  -toohave un équivalent de Britta Simon dans 360 en ligne qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c96b-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - toohave a counterpart of Britta Simon in 360 Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c96b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8c96b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c96b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8c96b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c96b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c96b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application en ligne 360.</span><span class="sxs-lookup"><span data-stu-id="8c96b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="8c96b-150">**tooconfigure Azure AD authentification unique avec l’option Online 360, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c96b-150">**tooconfigure Azure AD single sign-on with 360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c96b-151">Bonjour portail Azure, sur hello **Online 360** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-151">In hello Azure portal, on hello **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8c96b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8c96b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="8c96b-155">Sur hello **360 domaine en ligne et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c96b-155">On hello **360 Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="8c96b-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="8c96b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8c96b-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="8c96b-158">hello value is not real.</span></span> <span data-ttu-id="8c96b-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="8c96b-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8c96b-160">Contact [équipe de support Client en ligne 360](mailto:360online@software-innovation.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="8c96b-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="8c96b-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8c96b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="8c96b-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8c96b-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8c96b-165">tooconfigure l’authentification unique sur **Online 360** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique en ligne de 360](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="8c96b-165">tooconfigure single sign-on on **360 Online** side, you need toosend hello downloaded **Metadata XML** too[360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8c96b-166">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8c96b-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c96b-167">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8c96b-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c96b-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c96b-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c96b-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c96b-170">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8c96b-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8c96b-172">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c96b-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c96b-173">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8c96b-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c96b-175">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c96b-177">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8c96b-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c96b-179">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c96b-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c96b-181">a.</span><span class="sxs-lookup"><span data-stu-id="8c96b-181">a.</span></span> <span data-ttu-id="8c96b-182">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c96b-183">b.</span><span class="sxs-lookup"><span data-stu-id="8c96b-183">b.</span></span> <span data-ttu-id="8c96b-184">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c96b-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c96b-185">c.</span><span class="sxs-lookup"><span data-stu-id="8c96b-185">c.</span></span> <span data-ttu-id="8c96b-186">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8c96b-187">d.</span><span class="sxs-lookup"><span data-stu-id="8c96b-187">d.</span></span> <span data-ttu-id="8c96b-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="8c96b-189">Création d’un utilisateur de test 360 Online</span><span class="sxs-lookup"><span data-stu-id="8c96b-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="8c96b-190">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8c96b-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="8c96b-191">Vous devez toocontact [équipe de support technique en ligne de 360](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="8c96b-191">you need toocontact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8c96b-192">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c96b-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8c96b-193">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant too360 accès en ligne.</span><span class="sxs-lookup"><span data-stu-id="8c96b-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too360 Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8c96b-195">**tooassign Britta Simon too360 Online, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c96b-195">**tooassign Britta Simon too360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c96b-196">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8c96b-198">Dans la liste des applications hello, sélectionnez **Online 360**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-198">In hello applications list, select **360 Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="8c96b-200">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8c96b-202">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-202">Click **Add** button.</span></span> <span data-ttu-id="8c96b-203">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8c96b-205">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8c96b-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c96b-206">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c96b-207">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8c96b-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c96b-208">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8c96b-208">Testing single sign-on</span></span>

<span data-ttu-id="8c96b-209">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8c96b-209">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c96b-210">Lorsque vous cliquez sur hello 360 vignette Bonjour volet d’accès, vous devez obtenir l’application en ligne de tooyour automatiquement signé sur 360.</span><span class="sxs-lookup"><span data-stu-id="8c96b-210">When you click hello 360 Online tile in hello Access Panel, you should get automatically signed-on tooyour 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8c96b-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8c96b-211">Additional resources</span></span>

* [<span data-ttu-id="8c96b-212">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c96b-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c96b-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8c96b-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png

