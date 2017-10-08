---
title: "Didacticiel : Intégration d’Azure Active Directory à Teamwork | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le travail d’équipe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="0c3d0-103">Didacticiel : Intégration d’Azure Active Directory à Teamwork</span><span class="sxs-lookup"><span data-stu-id="0c3d0-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="0c3d0-104">Dans ce didacticiel, vous apprendrez comment toointegrate le travail d’équipe avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c3d0-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c3d0-105">Intégration d’équipe à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0c3d0-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0c3d0-106">Vous pouvez contrôler dans Azure AD qui a accès tooTeamwork</span><span class="sxs-lookup"><span data-stu-id="0c3d0-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="0c3d0-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTeamwork (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c3d0-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="0c3d0-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0c3d0-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c3d0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c3d0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c3d0-110">Prerequisites</span></span>

<span data-ttu-id="0c3d0-111">tooconfigure intégration d’Azure AD avec le travail d’équipe, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0c3d0-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="0c3d0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c3d0-113">Un abonnement Teamwork pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0c3d0-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="0c3d0-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0c3d0-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="0c3d0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c3d0-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0c3d0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c3d0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0c3d0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0c3d0-118">Scenario description</span></span>
<span data-ttu-id="0c3d0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c3d0-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="0c3d0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c3d0-121">Ajout d’équipe à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0c3d0-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="0c3d0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="0c3d0-123">Ajout d’équipe à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0c3d0-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="0c3d0-124">tooconfigure hello intégration d’équipe dans Azure AD, vous devez tooadd le travail d’équipe à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0c3d0-125">**tooadd le travail d’équipe à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c3d0-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c3d0-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0c3d0-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0c3d0-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0c3d0-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0c3d0-133">Dans la zone de recherche de hello, tapez **équipe**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-133">In hello search box, type **Teamwork**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="0c3d0-135">Dans le volet de résultats hello, sélectionnez **équipe**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c3d0-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c3d0-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Teamwork au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0c3d0-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0c3d0-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le travail d’équipe est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="0c3d0-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans le travail d’équipe doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="0c3d0-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le travail d’équipe.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="0c3d0-142">tooconfigure et test Azure AD l’authentification unique avec le travail d’équipe, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="0c3d0-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0c3d0-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0c3d0-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c3d0-145">**[Création d’un utilisateur de test équipe](#creating-a-teamwork-test-user)**  -toohave de Britta Simon dans le travail d’équipe qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0c3d0-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c3d0-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c3d0-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c3d0-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="0c3d0-150">**tooconfigure Azure AD authentification unique avec le travail d’équipe, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c3d0-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c3d0-151">Dans le portail de gestion Azure hello, sur hello **équipe** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0c3d0-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="0c3d0-155">Sur hello **URL et le domaine de l’équipe** section hello **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="0c3d0-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="0c3d0-157">Notez qu’il ne s’agit pas de la valeur réelle hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="0c3d0-158">Vous avez tooupdate URL de connexion cette valeur avec hello réel.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="0c3d0-159">Contact [équipe de prise en charge de travail en équipe](mailto:support@teamwork.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="0c3d0-160">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="0c3d0-162">Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="0c3d0-163">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-163">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="0c3d0-165">Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="0c3d0-167">Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0c3d0-169">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="0c3d0-171">tooget l’authentification unique configurée pour votre application, contactez [équipe de prise en charge de travail en équipe](mailto:support@teamwork.com) et fournissez-leur hello téléchargé **métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c3d0-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c3d0-173">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0c3d0-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c3d0-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c3d0-176">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0c3d0-178">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0c3d0-180">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0c3d0-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c3d0-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c3d0-184">a.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-184">a.</span></span> <span data-ttu-id="0c3d0-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c3d0-186">b.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-186">b.</span></span> <span data-ttu-id="0c3d0-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c3d0-188">c.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-188">c.</span></span> <span data-ttu-id="0c3d0-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0c3d0-190">d.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-190">d.</span></span> <span data-ttu-id="0c3d0-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="0c3d0-192">Création d’un utilisateur de test Teamwork</span><span class="sxs-lookup"><span data-stu-id="0c3d0-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="0c3d0-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Teamwork.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="0c3d0-194">Collaborez avec [équipe de prise en charge de travail en équipe](mailto:support@teamwork.com) tooadd les utilisateurs de hello dans la plateforme de travail en équipe hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0c3d0-195">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3d0-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0c3d0-196">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooTeamwork de son accès.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0c3d0-198">**tooassign Britta Simon tooTeamwork, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c3d0-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c3d0-199">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0c3d0-201">Dans la liste des applications hello, sélectionnez **équipe**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-201">In hello applications list, select **Teamwork**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="0c3d0-203">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0c3d0-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-205">Click **Add** button.</span></span> <span data-ttu-id="0c3d0-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0c3d0-208">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0c3d0-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c3d0-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="0c3d0-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0c3d0-211">Testing single sign-on</span></span>

<span data-ttu-id="0c3d0-212">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0c3d0-213">Lorsque vous cliquez sur mosaïque équipe hello hello volet d’accès, vous devez obtenir l’application d’équipe automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="0c3d0-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0c3d0-214">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0c3d0-214">Additional resources</span></span>

* [<span data-ttu-id="0c3d0-215">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c3d0-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c3d0-216">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0c3d0-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png