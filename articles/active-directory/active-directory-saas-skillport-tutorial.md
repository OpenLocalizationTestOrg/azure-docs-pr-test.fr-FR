---
title: "Didacticiel : Intégration d’Azure Active Directory avec Skillport | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="b0773-103">Didacticiel : Intégration d’Azure AD avec Skillport</span><span class="sxs-lookup"><span data-stu-id="b0773-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="b0773-104">Dans ce didacticiel, vous apprendrez comment toointegrate Skillport avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0773-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0773-105">Intégration Skillport à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b0773-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0773-106">Vous pouvez contrôler dans Azure AD qui a accès tooSkillport</span><span class="sxs-lookup"><span data-stu-id="b0773-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="b0773-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSkillport (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0773-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b0773-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0773-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0773-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0773-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b0773-110">Prerequisites</span></span>

<span data-ttu-id="b0773-111">tooconfigure intégration d’Azure AD avec Skillport, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b0773-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="b0773-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0773-113">Un abonnement Skillport pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b0773-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0773-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b0773-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0773-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b0773-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0773-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b0773-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0773-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0773-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0773-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b0773-118">Scenario description</span></span>
<span data-ttu-id="b0773-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b0773-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0773-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b0773-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0773-121">Ajout de Skillport à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b0773-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="b0773-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="b0773-123">Ajout de Skillport à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b0773-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="b0773-124">intégration de hello tooconfigure de Skillport dans Azure AD, vous devez tooadd Skillport à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b0773-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0773-125">**tooadd Skillport à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0773-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0773-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b0773-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0773-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b0773-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0773-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b0773-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b0773-131">Cliquez sur **nouvelle Application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="b0773-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b0773-133">Dans la zone de recherche de hello, tapez **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="b0773-133">In hello search box, type **Skillport**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="b0773-135">Dans le volet de résultats hello, sélectionnez **Skillport**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0773-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0773-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0773-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Skillport avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b0773-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0773-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Skillport est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0773-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="b0773-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Skillport doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="b0773-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="b0773-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Skillport.</span><span class="sxs-lookup"><span data-stu-id="b0773-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="b0773-142">tooconfigure et test Azure AD l’authentification unique avec Skillport, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="b0773-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0773-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b0773-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0773-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0773-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0773-145">**[Création d’un utilisateur de test Skillport](#creating-a-skillport-test-user)**  -toohave un équivalent de Britta Simon dans Skillport est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b0773-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0773-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b0773-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0773-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="b0773-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0773-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0773-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Skillport.</span><span class="sxs-lookup"><span data-stu-id="b0773-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="b0773-150">**tooconfigure Azure AD single sign-on avec Skillport, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0773-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0773-151">Bonjour portail Azure, sur hello **Skillport** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b0773-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b0773-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b0773-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="b0773-155">Sur hello **Skillport domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b0773-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="b0773-157">a.</span><span class="sxs-lookup"><span data-stu-id="b0773-157">a.</span></span> <span data-ttu-id="b0773-158">Bonjour **URL de connexion** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b0773-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="b0773-159">Centre de données Europe : `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="b0773-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="b0773-160">Centre de données États-Unis : `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="b0773-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="b0773-161">b.</span><span class="sxs-lookup"><span data-stu-id="b0773-161">b.</span></span> <span data-ttu-id="b0773-162">Bonjour **URL de réponse** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b0773-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="b0773-163">Centre de données Europe : `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="b0773-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="b0773-164">Centre de données États-Unis : `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="b0773-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0773-165">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="b0773-165">These values are not hello real.</span></span> <span data-ttu-id="b0773-166">Mettre à jour ces valeurs avec l’URL de réponse réelle hello et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="b0773-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b0773-167">Contact [équipe de support Client de Skillport](https://www.skillsoft.com/contact.asp) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="b0773-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="b0773-168">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b0773-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="b0773-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b0773-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0773-172">tooconfigure l’authentification unique sur **Skillport** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="b0773-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="b0773-173">Ils seront configurer toohave hello connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="b0773-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0773-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0773-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="b0773-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b0773-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0773-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0773-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b0773-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0773-180">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b0773-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0773-182">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b0773-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0773-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b0773-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0773-186">a.</span><span class="sxs-lookup"><span data-stu-id="b0773-186">a.</span></span> <span data-ttu-id="b0773-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0773-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0773-188">b.</span><span class="sxs-lookup"><span data-stu-id="b0773-188">b.</span></span> <span data-ttu-id="b0773-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0773-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0773-190">c.</span><span class="sxs-lookup"><span data-stu-id="b0773-190">c.</span></span> <span data-ttu-id="b0773-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b0773-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0773-192">d.</span><span class="sxs-lookup"><span data-stu-id="b0773-192">d.</span></span> <span data-ttu-id="b0773-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0773-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="b0773-194">Création d’un utilisateur de test Skillport</span><span class="sxs-lookup"><span data-stu-id="b0773-194">Creating a Skillport test user</span></span>

<span data-ttu-id="b0773-195">Dans l’ordre toocreate Skillport tester un utilisateur, vous devez toocontact [équipe de support Skillport](https://www.skillsoft.com/contact.asp) d’avoir plusieurs scénarios d’entreprise selon la spécification toohello pour utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="b0773-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="b0773-196">Ils seront configurer après discussion avec les utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b0773-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0773-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0773-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0773-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSkillport.</span><span class="sxs-lookup"><span data-stu-id="b0773-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b0773-200">**tooassign Britta Simon tooSkillport, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0773-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0773-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b0773-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b0773-203">Dans la liste des applications hello, sélectionnez **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="b0773-203">In hello applications list, select **Skillport**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="b0773-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b0773-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b0773-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b0773-207">Click **Add** button.</span></span> <span data-ttu-id="b0773-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b0773-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b0773-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b0773-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0773-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b0773-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0773-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b0773-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0773-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b0773-213">Testing single sign-on</span></span>

<span data-ttu-id="b0773-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b0773-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0773-215">Lorsque vous cliquez sur mosaïque Skillport hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Skillport application.</span><span class="sxs-lookup"><span data-stu-id="b0773-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="b0773-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b0773-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b0773-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b0773-217">Additional resources</span></span>

* [<span data-ttu-id="b0773-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0773-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0773-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b0773-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

