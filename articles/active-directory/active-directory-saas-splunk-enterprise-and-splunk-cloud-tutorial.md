---
title: "Didacticiel : intégration d’Azure Active Directory à Splunk Enterprise et Splunk Cloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Splunk Enterprise et Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="1be36-103">Didacticiel : Intégration d’Azure Active Directory avec Splunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="1be36-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="1be36-104">Dans ce didacticiel, vous apprendrez comment toointegrate Splunk entreprise et Splunk Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1be36-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1be36-105">Intégration Splunk Enterprise et Splunk Cloud à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1be36-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1be36-106">Vous pouvez contrôler dans Azure AD qui a accès tooSplunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="1be36-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="1be36-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSplunk Enterprise et Splunk Cloud-session unique (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="1be36-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="1be36-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="1be36-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1be36-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1be36-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1be36-110">Prerequisites</span></span>

<span data-ttu-id="1be36-111">tooconfigure intégration d’Azure AD avec Splunk Enterprise et Splunk Cloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1be36-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="1be36-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1be36-113">Un abonnement Splunk Enterprise ou Splunk Cloud avec l’authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="1be36-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="1be36-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1be36-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="1be36-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="1be36-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1be36-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1be36-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1be36-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1be36-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1be36-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1be36-118">Scenario description</span></span>
<span data-ttu-id="1be36-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1be36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1be36-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1be36-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1be36-121">Ajout de Splunk Enterprise et Splunk Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1be36-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="1be36-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="1be36-123">Ajouter des Splunk Enterprise et Splunk Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1be36-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="1be36-124">tooconfigure hello intégration d’entreprise de Splunk et Splunk Cloud dans Azure AD, vous devez tooadd Splunk Enterprise Splunk Cloud de liste de tooyour hello galerie des applications et gérées SaaS.</span><span class="sxs-lookup"><span data-stu-id="1be36-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1be36-125">**tooadd Splunk entreprise et Splunk Cloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1be36-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1be36-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1be36-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="1be36-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="1be36-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="1be36-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="1be36-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="1be36-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="1be36-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="1be36-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="1be36-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="1be36-135">Dans la zone de recherche de hello, tapez **Splunk Enterprise ou Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1be36-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="1be36-137">Dans le volet de résultats hello, sélectionnez **Splunk Enterprise et Splunk Cloud**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1be36-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1be36-139">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1be36-140">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Splunk Enterprise et Splunk Cloud, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1be36-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1be36-141">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur hello équivalent Splunk Enterprise et Splunk Cloud est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1be36-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="1be36-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Splunk Enterprise et Splunk Cloud doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="1be36-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="1be36-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="1be36-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="1be36-144">tooconfigure et test Azure AD l’authentification unique avec Splunk Enterprise et Splunk Cloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="1be36-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1be36-145">**[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1be36-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1be36-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1be36-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1be36-147">**[Création d’un utilisateur de test Splunk Enterprise et Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave de Britta Simon dans Splunk entreprise et Splunk Cloud qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="1be36-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1be36-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1be36-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1be36-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="1be36-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1be36-150">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1be36-151">Dans cette section, vous activez l’authentification unique de Azure AD dans le portail classique de hello et configurez l’authentification unique dans votre application d’entreprise de Splunk et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="1be36-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="1be36-152">**tooconfigure Azure AD l’authentification unique avec Splunk Enterprise et Splunk nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1be36-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1be36-153">Dans le portail classique hello, sur hello **Splunk Enterprise et Splunk Cloud** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1be36-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurer l’authentification unique][6] 

2. <span data-ttu-id="1be36-155">Sur hello **Comment voulez-vous que toosign les utilisateurs sur tooSplunk Enterprise et Splunk Cloud** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="1be36-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="1be36-157">Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1be36-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="1be36-159">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour Splunk entreprise et votre application Splunk Cloud à l’aide de hello modèle :`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="1be36-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="1be36-160">Bonjour **identificateur** zone de texte, tapez l’URL de votre serveur Splunk hello.</span><span class="sxs-lookup"><span data-stu-id="1be36-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="1be36-161">Bonjour **URL de réponse** zone de texte, tapez l’URL hello avec hello modèle :`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="1be36-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="1be36-162">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1be36-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="1be36-163">Sur hello **configurer l’authentification unique à Splunk Enterprise et Splunk Cloud** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1be36-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="1be36-165">Cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1be36-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="1be36-166">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1be36-166">Click **Next**.</span></span>

5. <span data-ttu-id="1be36-167">tooget SSO configuré pour votre application, contactez Splunk entreprise et l’équipe de support Splunk Cloud et par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="1be36-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="1be36-168">Hello téléchargé **federaton métadonnées**</span><span class="sxs-lookup"><span data-stu-id="1be36-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="1be36-169">Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="1be36-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Authentification unique Azure AD][10]

7. <span data-ttu-id="1be36-171">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1be36-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1be36-173">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-173">Create an Azure AD test user</span></span>
<span data-ttu-id="1be36-174">Dans cette section, vous créez un utilisateur de test dans le portail classique de hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1be36-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="1be36-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1be36-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1be36-177">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1be36-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1be36-179">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="1be36-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="1be36-180">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1be36-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1be36-182">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1be36-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1be36-184">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1be36-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="1be36-186">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="1be36-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1be36-187">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1be36-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1be36-188">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1be36-188">Click **Next**.</span></span>

6.  <span data-ttu-id="1be36-189">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1be36-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="1be36-191">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="1be36-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1be36-192">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1be36-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="1be36-193">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1be36-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="1be36-194">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1be36-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="1be36-195">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1be36-195">Click **Next**.</span></span>

7. <span data-ttu-id="1be36-196">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="1be36-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1be36-198">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1be36-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="1be36-200">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1be36-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="1be36-201">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="1be36-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="1be36-202">Créer un utilisateur de test Splunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="1be36-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="1be36-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="1be36-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="1be36-204">Collaborez avec Splunk Enterprise et Splunk Cloud prise en charge team tooadd hello utilisateurs hello Splunk Enterprise et Splunk Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="1be36-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1be36-205">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1be36-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1be36-206">Dans cette section, vous activez Britta Simon toouse SSOy Azure accorder son accès tooSplunk Enterprise et le Cloud de Splunk.</span><span class="sxs-lookup"><span data-stu-id="1be36-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1be36-208">**tooassign Britta Simon tooSplunk Enterprise et Splunk nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1be36-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1be36-209">Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="1be36-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1be36-211">Dans la liste des applications hello, sélectionnez **Splunk Enterprise et Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1be36-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="1be36-213">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1be36-213">In hello menu on hello top, click **Users**.</span></span>

    ![Affecter des utilisateurs][203]

4. <span data-ttu-id="1be36-215">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1be36-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="1be36-216">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="1be36-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1be36-218">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1be36-218">Test single sign-on</span></span>

<span data-ttu-id="1be36-219">Dans cette section, vous testez votre SSOonfiguration d’Active Directory Azure à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="1be36-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="1be36-220">Lorsque vous cliquez sur hello Splunk Enterprise et vignette Splunk Cloud Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Splunk Enterprise et Splunk Cloud une application.</span><span class="sxs-lookup"><span data-stu-id="1be36-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1be36-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1be36-221">Additional resources</span></span>

* [<span data-ttu-id="1be36-222">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1be36-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1be36-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1be36-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
