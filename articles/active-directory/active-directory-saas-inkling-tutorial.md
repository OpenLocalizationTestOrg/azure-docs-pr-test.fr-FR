---
title: "Didacticiel : intégration d’Azure Active Directory à Inkling | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="28b3d-103">Didacticiel : Intégration d’Azure Active Directory avec Inkling</span><span class="sxs-lookup"><span data-stu-id="28b3d-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="28b3d-104">Dans ce didacticiel, vous apprendrez comment toointegrate Inkling avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28b3d-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28b3d-105">Intégration Inkling à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="28b3d-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28b3d-106">Vous pouvez contrôler dans Azure AD qui a accès tooInkling</span><span class="sxs-lookup"><span data-stu-id="28b3d-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="28b3d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooInkling (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28b3d-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="28b3d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="28b3d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28b3d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28b3d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="28b3d-110">Prerequisites</span></span>

<span data-ttu-id="28b3d-111">tooconfigure intégration d’Azure AD avec Inkling, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="28b3d-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="28b3d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28b3d-113">Un abonnement Inkling pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="28b3d-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="28b3d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="28b3d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="28b3d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="28b3d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28b3d-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="28b3d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="28b3d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28b3d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="28b3d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="28b3d-118">Scenario description</span></span>
<span data-ttu-id="28b3d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="28b3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28b3d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="28b3d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28b3d-121">Ajout de Inkling à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="28b3d-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="28b3d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="28b3d-123">Ajout de Inkling à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="28b3d-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="28b3d-124">intégration de hello tooconfigure de Inkling dans Azure AD, vous devez tooadd Inkling à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="28b3d-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28b3d-125">**tooadd Inkling à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28b3d-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28b3d-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="28b3d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28b3d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28b3d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="28b3d-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="28b3d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="28b3d-133">Dans la zone de recherche de hello, tapez **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-133">In hello search box, type **Inkling**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="28b3d-135">Dans le volet de résultats hello, sélectionnez **Inkling**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="28b3d-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28b3d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28b3d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Inkling avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="28b3d-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28b3d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Inkling est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28b3d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="28b3d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Inkling doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="28b3d-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="28b3d-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Inkling.</span><span class="sxs-lookup"><span data-stu-id="28b3d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="28b3d-142">tooconfigure et test Azure AD l’authentification unique avec Inkling, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="28b3d-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28b3d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="28b3d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28b3d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28b3d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28b3d-145">**[Création d’un utilisateur de test Inkling](#creating-an-inkling-test-user)**  -toohave de Britta Simon dans Inkling qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="28b3d-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="28b3d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28b3d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28b3d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="28b3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28b3d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28b3d-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Inkling.</span><span class="sxs-lookup"><span data-stu-id="28b3d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="28b3d-150">**tooconfigure Azure AD single sign-on avec Inkling, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28b3d-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="28b3d-151">Dans le portail de gestion Azure hello, sur hello **Inkling** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="28b3d-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28b3d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="28b3d-155">Sur hello **Inkling domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28b3d-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="28b3d-157">a.</span><span class="sxs-lookup"><span data-stu-id="28b3d-157">a.</span></span> <span data-ttu-id="28b3d-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="28b3d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="28b3d-159">b.</span><span class="sxs-lookup"><span data-stu-id="28b3d-159">b.</span></span> <span data-ttu-id="28b3d-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="28b3d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28b3d-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="28b3d-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="28b3d-162">Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="28b3d-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="28b3d-163">Contact [équipe de support Inkling](mailto:press@inkling.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="28b3d-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="28b3d-164">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="28b3d-166">Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="28b3d-167">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-167">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="28b3d-169">Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="28b3d-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="28b3d-171">Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="28b3d-173">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="28b3d-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="28b3d-175">tooget l’authentification unique configurée pour votre application, contactez [équipe de support Inkling](mailto:press@inkling.com) et les fournir avec téléchargé **métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28b3d-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="28b3d-177">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28b3d-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="28b3d-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28b3d-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28b3d-180">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="28b3d-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28b3d-182">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="28b3d-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28b3d-184">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="28b3d-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28b3d-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28b3d-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28b3d-188">a.</span><span class="sxs-lookup"><span data-stu-id="28b3d-188">a.</span></span> <span data-ttu-id="28b3d-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28b3d-190">b.</span><span class="sxs-lookup"><span data-stu-id="28b3d-190">b.</span></span> <span data-ttu-id="28b3d-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28b3d-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28b3d-192">c.</span><span class="sxs-lookup"><span data-stu-id="28b3d-192">c.</span></span> <span data-ttu-id="28b3d-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28b3d-194">d.</span><span class="sxs-lookup"><span data-stu-id="28b3d-194">d.</span></span> <span data-ttu-id="28b3d-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="28b3d-196">Création d’un utilisateur de test Inkling</span><span class="sxs-lookup"><span data-stu-id="28b3d-196">Creating an Inkling test user</span></span>

<span data-ttu-id="28b3d-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Inkling.</span><span class="sxs-lookup"><span data-stu-id="28b3d-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="28b3d-198">Collaborez avec [équipe de support Inkling](mailto:press@inkling.com) tooadd les utilisateurs de hello dans la plateforme de Inkling hello.</span><span class="sxs-lookup"><span data-stu-id="28b3d-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="28b3d-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28b3d-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="28b3d-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooInkling de son accès.</span><span class="sxs-lookup"><span data-stu-id="28b3d-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="28b3d-202">**tooassign Britta Simon tooInkling, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28b3d-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="28b3d-203">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="28b3d-205">Dans la liste des applications hello, sélectionnez **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-205">In hello applications list, select **Inkling**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="28b3d-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="28b3d-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-209">Click **Add** button.</span></span> <span data-ttu-id="28b3d-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="28b3d-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="28b3d-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28b3d-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28b3d-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="28b3d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="28b3d-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="28b3d-215">Testing single sign-on</span></span>

<span data-ttu-id="28b3d-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="28b3d-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="28b3d-217">Lorsque vous cliquez sur mosaïque Inkling hello hello volet d’accès, vous devez obtenir l’application de Inkling automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="28b3d-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="28b3d-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="28b3d-218">Additional resources</span></span>

* [<span data-ttu-id="28b3d-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28b3d-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28b3d-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="28b3d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png