---
title: "Didacticiel : Intégration d’Azure Active Directory à FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et FirmPlay - préconisation employé de recrutement."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="d7c10-103">Didacticiel : Intégration d’Azure Active Directory à FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="d7c10-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="d7c10-104">Dans ce didacticiel, vous apprendrez comment toointegrate FirmPlay - préconisation employé pour recrutement avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7c10-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7c10-105">Intégration FirmPlay - préconisation employé pour recrutement avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d7c10-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7c10-106">Vous pouvez contrôler dans Azure AD qui a accès tooFirmPlay - préconisation employé de recrutement</span><span class="sxs-lookup"><span data-stu-id="d7c10-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="d7c10-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFirmPlay - préconisation employé pour recrutement (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7c10-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="d7c10-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d7c10-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7c10-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7c10-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7c10-110">Prerequisites</span></span>

<span data-ttu-id="d7c10-111">tooconfigure intégration d’Azure AD avec FirmPlay - préconisation employé de recrutement, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d7c10-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="d7c10-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7c10-113">Un abonnement FirmPlay - Employee Advocacy for Recruiting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d7c10-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d7c10-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d7c10-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d7c10-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d7c10-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7c10-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d7c10-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d7c10-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7c10-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d7c10-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d7c10-118">Scenario description</span></span>
<span data-ttu-id="d7c10-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d7c10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7c10-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d7c10-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7c10-121">Ajout de FirmPlay - préconisation employé pour recrutement à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d7c10-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="d7c10-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="d7c10-123">Ajout de FirmPlay - préconisation employé pour recrutement à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d7c10-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="d7c10-124">intégration de hello tooconfigure de FirmPlay - préconisation employé pour recrutement dans Azure AD, vous devez tooadd FirmPlay - préconisation employé pour recrutement à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d7c10-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7c10-125">**tooadd FirmPlay - préconisation employé pour recrutement à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7c10-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7c10-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d7c10-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7c10-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d7c10-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d7c10-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d7c10-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d7c10-133">Dans la zone de recherche de hello, tapez **FirmPlay - préconisation employé pour recrutement**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="d7c10-135">Dans le volet de résultats hello, sélectionnez **FirmPlay - préconisation employé pour recrutement**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d7c10-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7c10-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7c10-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FirmPlay - Employee Advocacy for Recruiting avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d7c10-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7c10-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FirmPlay - préconisation employé pour recrutement est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7c10-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="d7c10-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FirmPlay - préconisation employé pour recrutement doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d7c10-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="d7c10-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans FirmPlay - préconisation employé de recrutement.</span><span class="sxs-lookup"><span data-stu-id="d7c10-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="d7c10-142">tooconfigure et test Azure AD l’authentification unique avec FirmPlay - préconisation employé de recrutement, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d7c10-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7c10-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d7c10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7c10-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7c10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7c10-145">**[Création d’un FirmPlay - préconisation employé pour l’utilisateur de test de recrutement](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave un équivalent de Britta Simon dans FirmPlay : préconisation employé pour recrutement qui est liée de sa représentation sous forme de toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7c10-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d7c10-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d7c10-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7c10-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d7c10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7c10-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7c10-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre FirmPlay - préconisation employé pour les applications de recrutement.</span><span class="sxs-lookup"><span data-stu-id="d7c10-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="d7c10-150">**tooconfigure Azure AD l’authentification unique avec FirmPlay - préconisation employé pour recrutement, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7c10-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7c10-151">Dans le portail de gestion Azure hello, sur hello **FirmPlay - préconisation employé pour recrutement** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d7c10-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d7c10-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="d7c10-155">Sur hello **FirmPlay - préconisation employé pour le domaine de recrutement et URL** section hello **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="d7c10-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="d7c10-157">Notez qu’il ne s’agit pas de la valeur réelle hello.</span><span class="sxs-lookup"><span data-stu-id="d7c10-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="d7c10-158">Vous avez tooupdate URL de connexion cette valeur avec hello réel.</span><span class="sxs-lookup"><span data-stu-id="d7c10-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="d7c10-159">Contact [FirmPlay - préconisation employé pour l’équipe de support technique de recrutement](mailto:engineering@firmplay.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="d7c10-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="d7c10-160">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="d7c10-162">Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="d7c10-163">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-163">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="d7c10-165">Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="d7c10-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="d7c10-167">Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d7c10-169">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d7c10-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="d7c10-171">Sur hello **FirmPlay - préconisation employé pour la Configuration de recrutement** , cliquez sur **FirmPlay configurer - préconisation employé pour recrutement** tooopen **configurer l’authentification**boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d7c10-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="d7c10-174">tooget l’authentification unique configurée pour votre application, contactez [FirmPlay - préconisation employé pour l’équipe de support technique de recrutement](mailto:engineering@firmplay.com) et leur fournir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="d7c10-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="d7c10-175">hello • téléchargé **fichier de certificat**</span><span class="sxs-lookup"><span data-stu-id="d7c10-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="d7c10-176">• hello **SAML Sign-On URL du Service unique**</span><span class="sxs-lookup"><span data-stu-id="d7c10-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="d7c10-177">• hello **ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="d7c10-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="d7c10-178">• hello **URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="d7c10-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7c10-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7c10-180">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7c10-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d7c10-182">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7c10-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7c10-183">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d7c10-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7c10-185">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d7c10-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7c10-187">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d7c10-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7c10-189">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7c10-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7c10-191">a.</span><span class="sxs-lookup"><span data-stu-id="d7c10-191">a.</span></span> <span data-ttu-id="d7c10-192">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7c10-193">b.</span><span class="sxs-lookup"><span data-stu-id="d7c10-193">b.</span></span> <span data-ttu-id="d7c10-194">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d7c10-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7c10-195">c.</span><span class="sxs-lookup"><span data-stu-id="d7c10-195">c.</span></span> <span data-ttu-id="d7c10-196">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d7c10-197">d.</span><span class="sxs-lookup"><span data-stu-id="d7c10-197">d.</span></span> <span data-ttu-id="d7c10-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="d7c10-199">Création d’un utilisateur de test FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="d7c10-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="d7c10-200">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="d7c10-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="d7c10-201">Collaborez avec [FirmPlay - préconisation employé pour l’équipe de support technique de recrutement](mailto:engineering@firmplay.com) utilisateurs hello tooadd hello FirmPlay - préconisation employé pour la plateforme de recrutement.</span><span class="sxs-lookup"><span data-stu-id="d7c10-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d7c10-202">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7c10-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d7c10-203">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooFirmPlay accès - préconisation employé de recrutement.</span><span class="sxs-lookup"><span data-stu-id="d7c10-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d7c10-205">**tooassign Britta Simon tooFirmPlay - préconisation employé pour recrutement, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d7c10-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7c10-206">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d7c10-208">Dans la liste des applications hello, sélectionnez **FirmPlay - préconisation employé pour recrutement**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="d7c10-210">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d7c10-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-212">Click **Add** button.</span></span> <span data-ttu-id="d7c10-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d7c10-215">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d7c10-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d7c10-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7c10-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d7c10-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d7c10-218">Testing single sign-on</span></span>

<span data-ttu-id="d7c10-219">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d7c10-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7c10-220">Lorsque vous cliquez sur hello FirmPlay - préconisation employé pour la vignette de recrutement Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour FirmPlay - préconisation employé pour les applications de recrutement.</span><span class="sxs-lookup"><span data-stu-id="d7c10-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d7c10-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d7c10-221">Additional resources</span></span>

* [<span data-ttu-id="d7c10-222">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7c10-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7c10-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d7c10-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png