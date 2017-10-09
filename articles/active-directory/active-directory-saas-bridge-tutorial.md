---
title: "Didacticiel : Intégration d’Azure Active Directory avec Bridge | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de pont."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 85e1917de63356a86aa87a0f82621391733ab2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="cfafa-103">Didacticiel : Intégration d’Azure Active Directory avec Bridge</span><span class="sxs-lookup"><span data-stu-id="cfafa-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="cfafa-104">Dans ce didacticiel, vous apprendrez comment toointegrate pont avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfafa-104">In this tutorial, you learn how toointegrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfafa-105">Intégration de pont à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cfafa-105">Integrating Bridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfafa-106">Vous pouvez contrôler dans Azure AD qui a accès tooBridge</span><span class="sxs-lookup"><span data-stu-id="cfafa-106">You can control in Azure AD who has access tooBridge</span></span>
- <span data-ttu-id="cfafa-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBridge (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-107">You can enable your users tooautomatically get signed-on tooBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfafa-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cfafa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cfafa-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfafa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfafa-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cfafa-110">Prerequisites</span></span>

<span data-ttu-id="cfafa-111">tooconfigure intégration d’Azure AD avec pont, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cfafa-111">tooconfigure Azure AD integration with Bridge, you need hello following items:</span></span>

- <span data-ttu-id="cfafa-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfafa-113">Un abonnement Bridge pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="cfafa-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfafa-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cfafa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfafa-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="cfafa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfafa-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cfafa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfafa-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfafa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfafa-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cfafa-118">Scenario description</span></span>
<span data-ttu-id="cfafa-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cfafa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfafa-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="cfafa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfafa-121">Ajout de pont à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cfafa-121">Adding Bridge from hello gallery</span></span>
2. <span data-ttu-id="cfafa-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-hello-gallery"></a><span data-ttu-id="cfafa-123">Ajout de pont à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cfafa-123">Adding Bridge from hello gallery</span></span>
<span data-ttu-id="cfafa-124">tooconfigure hello intégration de pont dans Azure AD, vous devez tooadd pont à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cfafa-124">tooconfigure hello integration of Bridge into Azure AD, you need tooadd Bridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfafa-125">**Pont tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cfafa-125">**tooadd Bridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfafa-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cfafa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfafa-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfafa-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cfafa-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cfafa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cfafa-133">Dans la zone de recherche de hello, tapez **pont**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-133">In hello search box, type **Bridge**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="cfafa-135">Dans le volet de résultats hello, sélectionnez **pont**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cfafa-135">In hello results panel, select **Bridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfafa-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfafa-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bridge avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cfafa-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cfafa-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le pont est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfafa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bridge is tooa user in Azure AD.</span></span> <span data-ttu-id="cfafa-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans le pont doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="cfafa-140">In other words, a link relationship between an Azure AD user and hello related user in Bridge needs toobe established.</span></span>

<span data-ttu-id="cfafa-141">Dans le pont, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="cfafa-141">In Bridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfafa-142">tooconfigure et test Azure AD l’authentification unique avec pont, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="cfafa-142">tooconfigure and test Azure AD single sign-on with Bridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfafa-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cfafa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfafa-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfafa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfafa-145">**[Création d’un utilisateur de test de pont](#creating-a-bridge-test-user)**  -toohave un équivalent de Britta Simon dans le pont est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cfafa-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - toohave a counterpart of Britta Simon in Bridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfafa-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cfafa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfafa-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="cfafa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfafa-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfafa-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de pont.</span><span class="sxs-lookup"><span data-stu-id="cfafa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="cfafa-150">**tooconfigure Azure AD single sign-on avec pont, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cfafa-150">**tooconfigure Azure AD single sign-on with Bridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfafa-151">Bonjour portail Azure, sur hello **pont** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-151">In hello Azure portal, on hello **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cfafa-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cfafa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="cfafa-155">Sur hello **URL et le domaine du pont** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cfafa-155">On hello **Bridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="cfafa-157">a.</span><span class="sxs-lookup"><span data-stu-id="cfafa-157">a.</span></span> <span data-ttu-id="cfafa-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="cfafa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="cfafa-159">b.</span><span class="sxs-lookup"><span data-stu-id="cfafa-159">b.</span></span> <span data-ttu-id="cfafa-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="cfafa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cfafa-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="cfafa-161">These values are not real.</span></span> <span data-ttu-id="cfafa-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="cfafa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cfafa-163">Contact [équipe de support Client de pont](https://community.bridgeapp.com/community/help) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="cfafa-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="cfafa-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cfafa-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="cfafa-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cfafa-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cfafa-168">Sur hello **Configuration du pont** , cliquez sur **configurer pont** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="cfafa-168">On hello **Bridge Configuration** section, click **Configure Bridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cfafa-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="cfafa-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="cfafa-171">tooconfigure l’authentification unique sur **pont** côté, vous devez hello toosend téléchargé **Certificate(Raw)** et **ID d’entité SAML SAML Sign-On URL du Service unique et URL de déconnexion**trop[équipe de support technique de pont](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="cfafa-171">tooconfigure single sign-on on **Bridge** side, you need toosend hello downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** too[Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="cfafa-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="cfafa-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfafa-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="cfafa-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfafa-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfafa-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfafa-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfafa-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="cfafa-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cfafa-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cfafa-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfafa-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cfafa-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfafa-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfafa-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="cfafa-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfafa-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cfafa-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfafa-187">a.</span><span class="sxs-lookup"><span data-stu-id="cfafa-187">a.</span></span> <span data-ttu-id="cfafa-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfafa-189">b.</span><span class="sxs-lookup"><span data-stu-id="cfafa-189">b.</span></span> <span data-ttu-id="cfafa-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cfafa-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfafa-191">c.</span><span class="sxs-lookup"><span data-stu-id="cfafa-191">c.</span></span> <span data-ttu-id="cfafa-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cfafa-193">d.</span><span class="sxs-lookup"><span data-stu-id="cfafa-193">d.</span></span> <span data-ttu-id="cfafa-194">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="cfafa-195">Création d’un utilisateur de test Bridge</span><span class="sxs-lookup"><span data-stu-id="cfafa-195">Creating a Bridge test user</span></span>

<span data-ttu-id="cfafa-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Bridge.</span><span class="sxs-lookup"><span data-stu-id="cfafa-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="cfafa-197">Travailler avec [équipe de support Client de pont](https://community.bridgeapp.com/community/help) toocreate un utilisateur dans la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="cfafa-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) toocreate a user in hello platform.</span></span> <span data-ttu-id="cfafa-198">Vous pouvez augmenter le ticket de support hello avec pont de <a href="https://community.bridgeapp.com/community/help">ici</a> tooadd les utilisateurs de hello dans la plateforme de pont hello.</span><span class="sxs-lookup"><span data-stu-id="cfafa-198">You can raise hello support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> tooadd hello users in hello Bridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cfafa-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfafa-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cfafa-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBridge.</span><span class="sxs-lookup"><span data-stu-id="cfafa-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBridge.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cfafa-202">**tooassign Britta Simon tooBridge, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cfafa-202">**tooassign Britta Simon tooBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfafa-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cfafa-205">Dans la liste des applications hello, sélectionnez **pont**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-205">In hello applications list, select **Bridge**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="cfafa-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cfafa-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-209">Click **Add** button.</span></span> <span data-ttu-id="cfafa-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cfafa-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="cfafa-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfafa-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfafa-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cfafa-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfafa-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cfafa-215">Testing single sign-on</span></span>

<span data-ttu-id="cfafa-216">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="cfafa-216">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="cfafa-217">Lorsque vous cliquez sur mosaïque de pont hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur l’application tooyour pont.</span><span class="sxs-lookup"><span data-stu-id="cfafa-217">When you click hello Bridge tile in hello Access Panel, you should get automatically signed-on tooyour Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfafa-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cfafa-218">Additional resources</span></span>

* [<span data-ttu-id="cfafa-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfafa-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfafa-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cfafa-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

