---
title: "Didacticiel : Intégration d’Azure Active Directory avec BC Bonjour Cloud | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et BC dans hello Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="393ee-103">Didacticiel : Intégration d’Azure Active Directory avec BC Bonjour Cloud</span><span class="sxs-lookup"><span data-stu-id="393ee-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="393ee-104">Dans ce didacticiel, vous découvrez comment toointegrate BC dans hello Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="393ee-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="393ee-105">Intégration BC Bonjour Cloud avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="393ee-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="393ee-106">Vous pouvez contrôler dans Azure AD qui a accès tooBC Bonjour Cloud</span><span class="sxs-lookup"><span data-stu-id="393ee-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="393ee-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBC Bonjour Cloud (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="393ee-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="393ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="393ee-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="393ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="393ee-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="393ee-110">Prerequisites</span></span>

<span data-ttu-id="393ee-111">tooconfigure intégration d’Azure AD avec BC Bonjour Cloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="393ee-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="393ee-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="393ee-113">Un BC Bonjour Cloud l’authentification unique sur abonnement activé</span><span class="sxs-lookup"><span data-stu-id="393ee-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="393ee-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="393ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="393ee-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="393ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="393ee-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="393ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="393ee-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="393ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="393ee-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="393ee-118">Scenario description</span></span>
<span data-ttu-id="393ee-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="393ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="393ee-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="393ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="393ee-121">Ajout de BC Bonjour Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="393ee-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="393ee-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="393ee-123">Ajout de BC Bonjour Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="393ee-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="393ee-124">intégration de hello tooconfigure de BC Bonjour Cloud dans Azure AD, vous devez tooadd BC Bonjour Cloud à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="393ee-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="393ee-125">**tooadd BC Bonjour Cloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="393ee-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="393ee-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="393ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="393ee-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="393ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="393ee-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="393ee-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="393ee-131">tooadd nouvelle application, cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="393ee-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="393ee-133">Dans la zone de recherche de hello, tapez **BC Bonjour Cloud**.</span><span class="sxs-lookup"><span data-stu-id="393ee-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="393ee-135">Dans le volet de résultats hello, sélectionnez **BC Bonjour Cloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="393ee-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="393ee-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="393ee-138">Cette section, vous allez configurer et tester Azure AD single sign-on avec BC Bonjour que cloud basé sur un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="393ee-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="393ee-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel hello utilisateur équivalent dans BC Bonjour Cloud est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="393ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="393ee-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans BC Bonjour Cloud doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="393ee-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="393ee-141">Imaginons Bonjour Cloud, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="393ee-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="393ee-142">tooconfigure et test Azure AD l’authentification unique avec BC Bonjour Cloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="393ee-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="393ee-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="393ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="393ee-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="393ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="393ee-145">**[Création d’un BC dans utilisateur de test Cloud hello](#creating-a-bc-in-the-cloud-test-user)**  -toohave un équivalent de Britta Simon dans BC Bonjour Cloud qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="393ee-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="393ee-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="393ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="393ee-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="393ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="393ee-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="393ee-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre BC dans l’application hello dans le Cloud.</span><span class="sxs-lookup"><span data-stu-id="393ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="393ee-150">**tooconfigure Azure AD single sign-on avec BC Bonjour Cloud, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="393ee-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="393ee-151">Bonjour portail Azure, sur hello **BC Bonjour Cloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="393ee-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="393ee-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="393ee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="393ee-155">Sur hello **BC hello domaine Cloud et URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="393ee-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="393ee-157">a.</span><span class="sxs-lookup"><span data-stu-id="393ee-157">a.</span></span> <span data-ttu-id="393ee-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="393ee-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="393ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="393ee-159">b.</span></span> <span data-ttu-id="393ee-160">Bonjour **identificateur** zone de texte, tapez une URL en tant que :`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="393ee-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="393ee-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="393ee-161">This value is not real.</span></span> <span data-ttu-id="393ee-162">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="393ee-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="393ee-163">Contact [BC dans l’équipe de support Client de Cloud hello](https://www.bcinthecloud.com/supportcenter/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="393ee-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="393ee-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="393ee-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="393ee-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="393ee-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="393ee-168">tooconfigure l’authentification unique sur **BC Bonjour Cloud** côté, vous devez hello toosend téléchargé **Metadata XML** trop[BC dans l’équipe de support technique du Cloud hello](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="393ee-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="393ee-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="393ee-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="393ee-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="393ee-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="393ee-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="393ee-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="393ee-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="393ee-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="393ee-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="393ee-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="393ee-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="393ee-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="393ee-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="393ee-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="393ee-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="393ee-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="393ee-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="393ee-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="393ee-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="393ee-184">a.</span><span class="sxs-lookup"><span data-stu-id="393ee-184">a.</span></span> <span data-ttu-id="393ee-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="393ee-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="393ee-186">b.</span><span class="sxs-lookup"><span data-stu-id="393ee-186">b.</span></span> <span data-ttu-id="393ee-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="393ee-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="393ee-188">c.</span><span class="sxs-lookup"><span data-stu-id="393ee-188">c.</span></span> <span data-ttu-id="393ee-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="393ee-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="393ee-190">d.</span><span class="sxs-lookup"><span data-stu-id="393ee-190">d.</span></span> <span data-ttu-id="393ee-191">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="393ee-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="393ee-192">Création d’un BC dans utilisateur de test hello Cloud</span><span class="sxs-lookup"><span data-stu-id="393ee-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="393ee-193">Dans cette section, vous créez un utilisateur appelé Britta Simon dans BC Bonjour Cloud.</span><span class="sxs-lookup"><span data-stu-id="393ee-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="393ee-194">Travailler avec [BC dans l’équipe de support Client de Cloud hello](https://www.bcinthecloud.com/supportcenter/) pour ajouter des utilisateurs de hello Bonjour BC Bonjour application Cloud.</span><span class="sxs-lookup"><span data-stu-id="393ee-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="393ee-195">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="393ee-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="393ee-196">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="393ee-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="393ee-197">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooBC accès Bonjour Cloud.</span><span class="sxs-lookup"><span data-stu-id="393ee-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="393ee-199">**tooassign tooBC Britta Simon Bonjour nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="393ee-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="393ee-200">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="393ee-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="393ee-202">Dans la liste des applications hello, sélectionnez **BC Bonjour Cloud**.</span><span class="sxs-lookup"><span data-stu-id="393ee-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="393ee-204">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="393ee-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="393ee-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="393ee-206">Click **Add** button.</span></span> <span data-ttu-id="393ee-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="393ee-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="393ee-209">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="393ee-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="393ee-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="393ee-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="393ee-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="393ee-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="393ee-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="393ee-212">Testing single sign-on</span></span>

<span data-ttu-id="393ee-213">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="393ee-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="393ee-214">Lorsque vous cliquez sur hello BC dans la vignette de Cloud hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour BC Bonjour application Cloud.</span><span class="sxs-lookup"><span data-stu-id="393ee-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="393ee-215">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="393ee-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="393ee-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="393ee-216">Additional resources</span></span>

* [<span data-ttu-id="393ee-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="393ee-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="393ee-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="393ee-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

