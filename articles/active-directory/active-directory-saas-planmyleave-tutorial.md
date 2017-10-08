---
title: "Didacticiel : Intégration d’Azure Active Directory à PlanMyLeave | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="1c4dc-103">Didacticiel : Intégration de PlanMyLeave à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c4dc-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="1c4dc-104">Dans ce didacticiel, vous apprendrez comment toointegrate PlanMyLeave avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c4dc-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c4dc-105">Intégration PlanMyLeave à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c4dc-106">Vous pouvez contrôler dans Azure AD qui a accès tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="1c4dc-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="1c4dc-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPlanMyLeave (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c4dc-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="1c4dc-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="1c4dc-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c4dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c4dc-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1c4dc-110">Prerequisites</span></span>

<span data-ttu-id="1c4dc-111">tooconfigure intégration d’Azure AD avec PlanMyLeave, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="1c4dc-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c4dc-113">Un abonnement PlanMyLeave pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1c4dc-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="1c4dc-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1c4dc-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c4dc-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1c4dc-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c4dc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1c4dc-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1c4dc-118">Scenario description</span></span>
<span data-ttu-id="1c4dc-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c4dc-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c4dc-121">Ajout de PlanMyLeave à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1c4dc-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="1c4dc-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="1c4dc-123">Ajout de PlanMyLeave à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1c4dc-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="1c4dc-124">intégration de hello tooconfigure de PlanMyLeave dans Azure AD, vous devez tooadd PlanMyLeave à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c4dc-125">**tooadd PlanMyLeave à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c4dc-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4dc-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c4dc-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c4dc-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1c4dc-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1c4dc-133">Dans la zone de recherche de hello, tapez **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="1c4dc-135">Dans le volet de résultats hello, sélectionnez **PlanMyLeave**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c4dc-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c4dc-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PlanMyLeave avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1c4dc-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c4dc-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PlanMyLeave est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="1c4dc-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PlanMyLeave doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="1c4dc-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="1c4dc-142">tooconfigure et test Azure AD l’authentification unique avec PlanMyLeave, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c4dc-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c4dc-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c4dc-145">**[Création d’un utilisateur de test PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave de Britta Simon dans PlanMyLeave qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1c4dc-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c4dc-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c4dc-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c4dc-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="1c4dc-150">**tooconfigure Azure AD single sign-on avec PlanMyLeave, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c4dc-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4dc-151">Dans le portail de gestion Azure hello, sur hello **PlanMyLeave** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1c4dc-153">Sur hello **l’authentification unique** page de boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="1c4dc-155">Sur hello **PlanMyLeave domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="1c4dc-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-157">a.</span></span> <span data-ttu-id="1c4dc-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="1c4dc-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="1c4dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-159">b.</span></span> <span data-ttu-id="1c4dc-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="1c4dc-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c4dc-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="1c4dc-162">Vous avez tooupdate ces valeurs avec hello réel connectent URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="1c4dc-163">Contact [équipe de support PlanMyLeave](mailto:support@planmyleave.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="1c4dc-164">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="1c4dc-166">Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="1c4dc-167">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-167">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="1c4dc-169">Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="1c4dc-171">Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1c4dc-173">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="1c4dc-175">Sur hello **PlanMyLeave Configuration** , cliquez sur **PlanMyLeave de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="1c4dc-178">Dans une autre fenêtre de navigateur web, connectez-vous à votre locataire PlanMyLeave en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="1c4dc-179">Accédez trop**le programme d’installation du système**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-179">Go too**System Setup**.</span></span> <span data-ttu-id="1c4dc-180">Puis sur hello **gestion de la sécurité** cliquez sur la section **paramètres SAML de l’entreprise** .</span><span class="sxs-lookup"><span data-stu-id="1c4dc-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="1c4dc-182">Sur hello **paramètres SAML** , cliquez sur icône de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="1c4dc-184">Sur hello **mise à jour les paramètres SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="1c4dc-186">a.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-186">a.</span></span>  <span data-ttu-id="1c4dc-187">Bonjour **URL de connexion** zone de texte, placez la valeur hello **SAML Sign-On URL du Service unique** à partir de la fenêtre de configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="1c4dc-188">b.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-188">b.</span></span>  <span data-ttu-id="1c4dc-189">Ouvrez votre fichier de certificat téléchargé dans le bloc-notes, copiez uniquement hello contenu entre hello---Begin Certificate---et---End certificate---de celui-ci dans le Presse-papiers et collez-la toohello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="1c4dc-190">c.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-190">c.</span></span> <span data-ttu-id="1c4dc-191">Définissez »**est activé**« trop »**Oui**».</span><span class="sxs-lookup"><span data-stu-id="1c4dc-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="1c4dc-192">d.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-192">d.</span></span> <span data-ttu-id="1c4dc-193">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c4dc-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c4dc-195">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1c4dc-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c4dc-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4dc-198">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c4dc-200">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c4dc-202">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c4dc-204">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c4dc-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c4dc-206">a.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-206">a.</span></span> <span data-ttu-id="1c4dc-207">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c4dc-208">b.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-208">b.</span></span> <span data-ttu-id="1c4dc-209">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c4dc-210">c.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-210">c.</span></span> <span data-ttu-id="1c4dc-211">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c4dc-212">d.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-212">d.</span></span> <span data-ttu-id="1c4dc-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="1c4dc-214">Création d’un utilisateur de test PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="1c4dc-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="1c4dc-215">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="1c4dc-216">PlanMyLeave prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1c4dc-217">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-217">There is no action item for you in this section.</span></span> <span data-ttu-id="1c4dc-218">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess PlanMyLeave s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="1c4dc-219">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact [équipe de support PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="1c4dc-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c4dc-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4dc-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c4dc-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooPlanMyLeave de son accès.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1c4dc-223">**tooassign Britta Simon tooPlanMyLeave, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c4dc-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4dc-224">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1c4dc-226">Dans la liste des applications hello, sélectionnez **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="1c4dc-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1c4dc-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-230">Click **Add** button.</span></span> <span data-ttu-id="1c4dc-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1c4dc-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c4dc-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c4dc-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="1c4dc-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1c4dc-236">Testing single sign-on</span></span>

<span data-ttu-id="1c4dc-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1c4dc-238">Lorsque vous cliquez sur mosaïque PlanMyLeave hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour PlanMyLeave application.</span><span class="sxs-lookup"><span data-stu-id="1c4dc-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1c4dc-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1c4dc-239">Additional resources</span></span>

* [<span data-ttu-id="1c4dc-240">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c4dc-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c4dc-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1c4dc-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png