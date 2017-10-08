---
title: "Didacticiel : Intégration d’Azure Active Directory à ServiceNow | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de ServiceNow et de ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="29603-103">Didacticiel : Intégration d’Azure Active Directory à ServiceNow</span><span class="sxs-lookup"><span data-stu-id="29603-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="29603-104">Dans ce didacticiel, vous apprendrez comment toointegrate ServiceNow et ServiceNow Express avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29603-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29603-105">Intégration de ServiceNow et ServiceNow Express avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="29603-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="29603-106">Vous pouvez contrôler dans Azure AD qui a accès tooServiceNow et de ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="29603-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="29603-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooServiceNow et le ServiceNow Express (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="29603-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="29603-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="29603-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="29603-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29603-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29603-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="29603-110">Prerequisites</span></span>
<span data-ttu-id="29603-111">tooconfigure intégration d’Azure AD avec ServiceNow et de ServiceNow Express, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29603-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="29603-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="29603-112">An Azure AD subscription</span></span>
* <span data-ttu-id="29603-113">Pour ServiceNow, une instance ou un locataire ServiceNow, version Calgary ou supérieure</span><span class="sxs-lookup"><span data-stu-id="29603-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="29603-114">Pour ServiceNow Express, une instance ServiceNow Express, version Helsinki ou supérieure</span><span class="sxs-lookup"><span data-stu-id="29603-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="29603-115">client de ServiceNow Hello doit avoir hello [plusieurs fournisseur unique signe de plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) activé.</span><span class="sxs-lookup"><span data-stu-id="29603-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="29603-116">Cette opération est possible en [envoyant une demande de service](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="29603-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="29603-117">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="29603-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="29603-118">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="29603-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="29603-119">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29603-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="29603-120">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29603-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29603-121">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="29603-121">Scenario description</span></span>
<span data-ttu-id="29603-122">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="29603-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29603-123">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="29603-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29603-124">Ajout de ServiceNow à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29603-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="29603-125">Configuration et test de l’authentification unique Azure AD pour ServiceNow ou ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="29603-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="29603-126">Ajout de ServiceNow à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29603-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="29603-127">tooconfigure hello l’intégration de ServiceNow ou ServiceNow Express dans Azure AD, vous devez tooadd ServiceNow à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="29603-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="29603-128">**tooadd ServiceNow à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29603-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29603-129">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29603-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="29603-131">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="29603-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="29603-132">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="29603-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="29603-134">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="29603-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="29603-136">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="29603-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="29603-138">Dans la zone de recherche de hello, tapez **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="29603-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="29603-140">Dans le volet de résultats hello, sélectionnez **ServiceNow**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="29603-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29603-142">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29603-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29603-143">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ServiceNow ou ServiceNow Express avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="29603-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29603-144">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ServiceNow est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29603-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="29603-145">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ServiceNow doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="29603-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="29603-146">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="29603-147">tooconfigure et test Azure AD l’authentification unique à ServiceNow, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="29603-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29603-148">**[Configuration d’Azure AD Single Sign-On pour ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="29603-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29603-149">**[Configuration d’Azure AD Single Sign-On pour ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="29603-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="29603-150">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29603-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="29603-151">**[Création d’un utilisateur de test ServiceNow](#creating-a-servicenow-test-user)**  -toohave de Britta Simon dans ServiceNow qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="29603-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="29603-152">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29603-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="29603-153">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="29603-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="29603-154">Si vous souhaitez tooconfigure ServiceNow omettez l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="29603-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="29603-155">De même, si vous souhaitez tooconfigure ServiceNow Express omettez l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="29603-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="29603-156">Configuration de l’authentification unique Azure AD pour ServiceNow</span><span class="sxs-lookup"><span data-stu-id="29603-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="29603-157">Dans le portail classique hello Azure AD, sur hello **ServiceNow** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue .</span><span class="sxs-lookup"><span data-stu-id="29603-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="29603-158">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="29603-159">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooServiceNow** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="29603-160">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="29603-161">Sur hello **configurer les paramètres de l’application** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="29603-162">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="29603-163">a.</span><span class="sxs-lookup"><span data-stu-id="29603-163">a.</span></span> <span data-ttu-id="29603-164">Bonjour **ServiceNow URL de connexion** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle : `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="29603-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="29603-165">b.</span><span class="sxs-lookup"><span data-stu-id="29603-165">b.</span></span> <span data-ttu-id="29603-166">Bonjour **identificateur** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle : `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="29603-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="29603-167">c.</span><span class="sxs-lookup"><span data-stu-id="29603-167">c.</span></span> <span data-ttu-id="29603-168">Cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="29603-168">Click **Next**</span></span>

4. <span data-ttu-id="29603-169">toohave Azure AD est automatiquement configurer ServiceNow pour l’authentification SAML, entrez votre nom d’instance ServiceNow, le nom d’utilisateur administrateur et le mot de passe administrateur Bonjour **configurer automatiquement l’authentification unique sur** écran et cliquez sur  *Configurer*.</span><span class="sxs-lookup"><span data-stu-id="29603-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="29603-170">Notez que ce nom d’utilisateur administrateur de hello fourni doit avoir hello **security_admin** rôle attribué dans ServiceNow pour cette toowork.</span><span class="sxs-lookup"><span data-stu-id="29603-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="29603-171">Dans le cas contraire, toomanually configurer ServiceNow toouse Azure AD comme fournisseur d’identité SAML, cliquez sur **configurer manuellement l’application hello pour l’authentification unique sur**, puis cliquez sur **suivant** et hello terminée étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="29603-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="29603-172">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="29603-173">Sur hello **configurer l’authentification unique auprès de ServiceNow** , cliquez sur **télécharger le certificat**, enregistrez le fichier de certificat hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="29603-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="29603-174">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="29603-175">Authentification tooyour application ServiceNow en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="29603-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="29603-176">Activer hello *intégration - plusieurs fournisseur d’authentification programme d’installation unique* plug-in en suivant hello les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="29603-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="29603-177">a.</span><span class="sxs-lookup"><span data-stu-id="29603-177">a.</span></span> <span data-ttu-id="29603-178">Dans le volet de navigation hello sur le côté gauche de hello, accédez trop**définition système** section, puis cliquez sur **plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="29603-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="29603-179">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activer le plug-in")</span><span class="sxs-lookup"><span data-stu-id="29603-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="29603-180">b.</span><span class="sxs-lookup"><span data-stu-id="29603-180">b.</span></span> <span data-ttu-id="29603-181">Recherchez *Integration - Multiple Provider Single Sign-On Installer* (Intégration - Programme d’installation de l’authentification unique à plusieurs fournisseurs).</span><span class="sxs-lookup"><span data-stu-id="29603-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="29603-182">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activer le plug-in")</span><span class="sxs-lookup"><span data-stu-id="29603-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="29603-183">c.</span><span class="sxs-lookup"><span data-stu-id="29603-183">c.</span></span> <span data-ttu-id="29603-184">Sélectionnez le plug-in hello.</span><span class="sxs-lookup"><span data-stu-id="29603-184">Select hello plugin.</span></span> <span data-ttu-id="29603-185">Cliquez avec le bouton droit et sélectionnez **Activate/Upgrade** (Activer/Mettre à niveau).</span><span class="sxs-lookup"><span data-stu-id="29603-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="29603-186">d.</span><span class="sxs-lookup"><span data-stu-id="29603-186">d.</span></span> <span data-ttu-id="29603-187">Cliquez sur hello **activer** bouton.</span><span class="sxs-lookup"><span data-stu-id="29603-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="29603-188">Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="29603-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="29603-189">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="29603-190">Sur hello **plusieurs propriétés de l’authentification unique de fournisseur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="29603-191">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="29603-192">a.</span><span class="sxs-lookup"><span data-stu-id="29603-192">a.</span></span> <span data-ttu-id="29603-193">Pour **Enable multiple provider SSO**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="29603-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="29603-194">b.</span><span class="sxs-lookup"><span data-stu-id="29603-194">b.</span></span> <span data-ttu-id="29603-195">En tant que **activer obtenue de la journalisation du débogage hello plusieurs fournisseur SSO integration**, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="29603-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="29603-196">c.</span><span class="sxs-lookup"><span data-stu-id="29603-196">c.</span></span> <span data-ttu-id="29603-197">Dans **champ hello sur utilisateur de hello table...**  zone de texte, type **nom_utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29603-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="29603-198">d.</span><span class="sxs-lookup"><span data-stu-id="29603-198">d.</span></span> <span data-ttu-id="29603-199">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="29603-199">Click **Save**.</span></span>

10. <span data-ttu-id="29603-200">Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **x509 certificats**.</span><span class="sxs-lookup"><span data-stu-id="29603-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="29603-201">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="29603-202">Sur hello **certificats X.509** boîte de dialogue, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="29603-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="29603-203">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="29603-204">Sur hello **certificats X.509** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="29603-205">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="29603-206">a.</span><span class="sxs-lookup"><span data-stu-id="29603-206">a.</span></span> <span data-ttu-id="29603-207">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="29603-207">Click **New**.</span></span>
    
     <span data-ttu-id="29603-208">b.</span><span class="sxs-lookup"><span data-stu-id="29603-208">b.</span></span> <span data-ttu-id="29603-209">Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="29603-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="29603-210">c.</span><span class="sxs-lookup"><span data-stu-id="29603-210">c.</span></span> <span data-ttu-id="29603-211">Sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="29603-211">Select **Active**.</span></span>
    
     <span data-ttu-id="29603-212">d.</span><span class="sxs-lookup"><span data-stu-id="29603-212">d.</span></span> <span data-ttu-id="29603-213">Pour **Format**, sélectionnez **PEM**.</span><span class="sxs-lookup"><span data-stu-id="29603-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="29603-214">e.</span><span class="sxs-lookup"><span data-stu-id="29603-214">e.</span></span> <span data-ttu-id="29603-215">Pour **Type**, sélectionnez **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="29603-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="29603-216">f.</span><span class="sxs-lookup"><span data-stu-id="29603-216">f.</span></span> <span data-ttu-id="29603-217">Ouvrez votre certificat codé en Base64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **PEM Certificate** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="29603-218">g.</span><span class="sxs-lookup"><span data-stu-id="29603-218">g.</span></span> <span data-ttu-id="29603-219">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="29603-219">Click **Update**.</span></span>

13. <span data-ttu-id="29603-220">Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="29603-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="29603-221">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="29603-222">Sur hello **fournisseurs d’identité** boîte de dialogue, cliquez sur **nouveau**:</span><span class="sxs-lookup"><span data-stu-id="29603-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="29603-223">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="29603-224">Sur hello **fournisseurs d’identité** boîte de dialogue, cliquez sur **SAML2 mise à jour 1 ?**:</span><span class="sxs-lookup"><span data-stu-id="29603-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="29603-225">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="29603-226">Dans la boîte de dialogue Propriétés de mise à jour 1 SAML2 hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="29603-227">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="29603-228">a.</span><span class="sxs-lookup"><span data-stu-id="29603-228">a.</span></span> <span data-ttu-id="29603-229">Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="29603-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="29603-230">b.</span><span class="sxs-lookup"><span data-stu-id="29603-230">b.</span></span> <span data-ttu-id="29603-231">Bonjour **champ utilisateur** zone de texte, type **messagerie** ou **nom_utilisateur**, selon le champ utilisé toouniquely identifier les utilisateurs dans votre déploiement de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="29603-232">Vous pouvez tooemit de configuration Azure AD un ID d’utilisateur hello Azure AD (nom d’utilisateur principal) ou que vous hello adresse de messagerie comme hello identificateur unique dans le jeton SAML de hello en va de toohello **ServiceNow > attributs > Single Sign-On** section de Hello portail Azure classic et mappage hello souhaité champ toohello **nameidentifier** attribut.</span><span class="sxs-lookup"><span data-stu-id="29603-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="29603-233">valeur de Hello pour l’attribut sélectionné de hello dans Azure AD (par exemple, nom d’utilisateur principal) doit correspondre à valeur hello stocké dans ServiceNow pour le champ hello entrée (par exemple, nom_utilisateur)</span><span class="sxs-lookup"><span data-stu-id="29603-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="29603-234">c.</span><span class="sxs-lookup"><span data-stu-id="29603-234">c.</span></span> <span data-ttu-id="29603-235">Dans le portail classique de hello Azure AD, copiez hello **ID fournisseur d’identité** valeur, puis collez-le dans hello **URL du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="29603-236">d.</span><span class="sxs-lookup"><span data-stu-id="29603-236">d.</span></span> <span data-ttu-id="29603-237">Dans le portail classique de hello Azure AD, copiez hello **URL de la demande d’authentification** valeur, puis collez-le dans hello **AuthnRequest du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="29603-238">e.</span><span class="sxs-lookup"><span data-stu-id="29603-238">e.</span></span> <span data-ttu-id="29603-239">Dans le portail classique de hello Azure AD, copiez hello **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **'s SingleLogoutRequest du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="29603-240">f.</span><span class="sxs-lookup"><span data-stu-id="29603-240">f.</span></span> <span data-ttu-id="29603-241">Bonjour **ServiceNow Homepage** zone de texte, tapez l’URL de votre page d’accueil d’instance ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="29603-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29603-242">page d’accueil d’instance Hello ServiceNow est une concaténation de votre **URL de client ServieNow** et **/navpage.do** (par exemple :`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="29603-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="29603-243">g.</span><span class="sxs-lookup"><span data-stu-id="29603-243">g.</span></span> <span data-ttu-id="29603-244">Bonjour **ID d’entité / émetteur** zone de texte, tapez l’URL de votre locataire ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="29603-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="29603-245">h.</span><span class="sxs-lookup"><span data-stu-id="29603-245">h.</span></span> <span data-ttu-id="29603-246">Bonjour **Audience URL** zone de texte, tapez l’URL de votre locataire ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="29603-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="29603-247">i.</span><span class="sxs-lookup"><span data-stu-id="29603-247">i.</span></span> <span data-ttu-id="29603-248">Bonjour **une liaison de protocole pour ' s SingleLogoutRequest hello d’IDP** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:bindings:HTTP-rediriger**.</span><span class="sxs-lookup"><span data-stu-id="29603-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="29603-249">j.</span><span class="sxs-lookup"><span data-stu-id="29603-249">j.</span></span> <span data-ttu-id="29603-250">Bonjour NameID Policy la zone de texte, tapez **urn : oasis : noms : tc : SAML:1.1:nameid-format : non spécifiée**.</span><span class="sxs-lookup"><span data-stu-id="29603-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="29603-251">k.</span><span class="sxs-lookup"><span data-stu-id="29603-251">k.</span></span> <span data-ttu-id="29603-252">Désélectionnez **Créer une classe de contexte d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="29603-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="29603-253">l.</span><span class="sxs-lookup"><span data-stu-id="29603-253">l.</span></span> <span data-ttu-id="29603-254">Bonjour **the AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="29603-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="29603-255">Cela n’est nécessaire que si votre organisation utilise uniquement le cloud.</span><span class="sxs-lookup"><span data-stu-id="29603-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="29603-256">Si vous utilisez des services ADFS ou MFA locaux pour l’authentification, vous ne devez pas configurer cette valeur.</span><span class="sxs-lookup"><span data-stu-id="29603-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="29603-257">m.</span><span class="sxs-lookup"><span data-stu-id="29603-257">m.</span></span> <span data-ttu-id="29603-258">Dans la zone de texte **Variation d’horloge**, entrez **60**.</span><span class="sxs-lookup"><span data-stu-id="29603-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="29603-259">n.</span><span class="sxs-lookup"><span data-stu-id="29603-259">n.</span></span> <span data-ttu-id="29603-260">Pour **Script d’authentification unique**, sélectionnez **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="29603-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="29603-261">o.</span><span class="sxs-lookup"><span data-stu-id="29603-261">o.</span></span> <span data-ttu-id="29603-262">En tant que **x509 certificat**, sélectionnez certificats hello que vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="29603-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="29603-263">p.</span><span class="sxs-lookup"><span data-stu-id="29603-263">p.</span></span> <span data-ttu-id="29603-264">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="29603-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="29603-265">Sur le portail classique hello Azure AD, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="29603-266">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="29603-267">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="29603-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="29603-268">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="29603-269">Configuration de l’authentification unique Azure AD pour ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="29603-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="29603-270">Dans le portail classique hello Azure AD, sur hello **ServiceNow** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue .</span><span class="sxs-lookup"><span data-stu-id="29603-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="29603-271">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="29603-272">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooServiceNow** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="29603-273">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="29603-274">Sur hello **configurer les paramètres de l’application** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="29603-275">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="29603-276">a.</span><span class="sxs-lookup"><span data-stu-id="29603-276">a.</span></span> <span data-ttu-id="29603-277">Bonjour **ServiceNow URL de connexion** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle : `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="29603-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="29603-278">b.</span><span class="sxs-lookup"><span data-stu-id="29603-278">b.</span></span> <span data-ttu-id="29603-279">Bonjour **URL de l’émetteur** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="29603-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="29603-280">c.</span><span class="sxs-lookup"><span data-stu-id="29603-280">c.</span></span> <span data-ttu-id="29603-281">Cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="29603-281">Click **Next**</span></span>

4. <span data-ttu-id="29603-282">Cliquez sur **configurer manuellement l’application hello pour l’authentification unique sur**, puis cliquez sur **suivant** hello complète comme suit.</span><span class="sxs-lookup"><span data-stu-id="29603-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="29603-283">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="29603-284">Sur hello **configurer l’authentification unique auprès de ServiceNow** , cliquez sur **télécharger le certificat**, enregistrez le fichier de certificat hello localement sur votre ordinateur, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="29603-285">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="29603-286">Authentification tooyour application ServiceNow Express en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="29603-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="29603-287">Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="29603-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="29603-288">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="29603-289">Sur hello **Single Sign-On** boîte de dialogue, cliquez sur icône de configuration hello sur supérieur hello droite et définissez hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="29603-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="29603-290">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="29603-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="29603-291">a.</span><span class="sxs-lookup"><span data-stu-id="29603-291">a.</span></span> <span data-ttu-id="29603-292">Activer/désactiver **activer plusieurs fournisseur SSO** toohello droite.</span><span class="sxs-lookup"><span data-stu-id="29603-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="29603-293">b.</span><span class="sxs-lookup"><span data-stu-id="29603-293">b.</span></span> <span data-ttu-id="29603-294">Activer/désactiver **activer l’enregistrement pour hello plusieurs fournisseur d’intégration de l’authentification unique de débogage** toohello droite.</span><span class="sxs-lookup"><span data-stu-id="29603-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="29603-295">c.</span><span class="sxs-lookup"><span data-stu-id="29603-295">c.</span></span> <span data-ttu-id="29603-296">Dans **champ hello sur utilisateur de hello table...**  zone de texte, type **nom_utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29603-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="29603-297">Sur hello **Single Sign-On** boîte de dialogue, cliquez sur **ajouter un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="29603-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="29603-298">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="29603-299">Sur hello **certificats X.509** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="29603-300">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="29603-301">a.</span><span class="sxs-lookup"><span data-stu-id="29603-301">a.</span></span> <span data-ttu-id="29603-302">Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="29603-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="29603-303">b.</span><span class="sxs-lookup"><span data-stu-id="29603-303">b.</span></span> <span data-ttu-id="29603-304">Sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="29603-304">Select **Active**.</span></span>
    
    <span data-ttu-id="29603-305">c.</span><span class="sxs-lookup"><span data-stu-id="29603-305">c.</span></span> <span data-ttu-id="29603-306">Pour **Format**, sélectionnez **PEM**.</span><span class="sxs-lookup"><span data-stu-id="29603-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="29603-307">d.</span><span class="sxs-lookup"><span data-stu-id="29603-307">d.</span></span> <span data-ttu-id="29603-308">Pour **Type**, sélectionnez **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="29603-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="29603-309">e.</span><span class="sxs-lookup"><span data-stu-id="29603-309">e.</span></span> <span data-ttu-id="29603-310">Créez un fichier codé en base64 à partir du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="29603-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="29603-311">Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="29603-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="29603-312">f.</span><span class="sxs-lookup"><span data-stu-id="29603-312">f.</span></span> <span data-ttu-id="29603-313">Ouvrez votre certificat codé en Base64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **PEM Certificate** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="29603-314">g.</span><span class="sxs-lookup"><span data-stu-id="29603-314">g.</span></span> <span data-ttu-id="29603-315">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="29603-315">Click **Update**.</span></span>
11. <span data-ttu-id="29603-316">Sur hello **Single Sign-On** boîte de dialogue, cliquez sur **ajouter un nouveau IdP**.</span><span class="sxs-lookup"><span data-stu-id="29603-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="29603-317">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="29603-318">Sur hello **Ajouter nouveau fournisseur d’identité** boîte de dialogue, sous **configurer le fournisseur d’identité**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="29603-319">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="29603-320">a.</span><span class="sxs-lookup"><span data-stu-id="29603-320">a.</span></span> <span data-ttu-id="29603-321">Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="29603-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="29603-322">b.</span><span class="sxs-lookup"><span data-stu-id="29603-322">b.</span></span> <span data-ttu-id="29603-323">Dans le portail classique de hello Azure AD, copiez hello **ID fournisseur d’identité** valeur, puis collez-le dans hello **URL du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="29603-324">c.</span><span class="sxs-lookup"><span data-stu-id="29603-324">c.</span></span> <span data-ttu-id="29603-325">Dans le portail classique de hello Azure AD, copiez hello **URL de la demande d’authentification** valeur, puis collez-le dans hello **AuthnRequest du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="29603-326">d.</span><span class="sxs-lookup"><span data-stu-id="29603-326">d.</span></span> <span data-ttu-id="29603-327">Dans le portail classique de hello Azure AD, copiez hello **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **'s SingleLogoutRequest du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29603-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="29603-328">e.</span><span class="sxs-lookup"><span data-stu-id="29603-328">e.</span></span> <span data-ttu-id="29603-329">En tant que **certificat de fournisseur d’identité**, sélectionnez certificats hello que vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="29603-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="29603-330">Cliquez sur **paramètres avancés**et sous **des propriétés supplémentaires du fournisseur d’identité**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="29603-331">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="29603-332">a.</span><span class="sxs-lookup"><span data-stu-id="29603-332">a.</span></span> <span data-ttu-id="29603-333">Bonjour **une liaison de protocole pour ' s SingleLogoutRequest hello d’IDP** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:bindings:HTTP-rediriger**.</span><span class="sxs-lookup"><span data-stu-id="29603-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="29603-334">b.</span><span class="sxs-lookup"><span data-stu-id="29603-334">b.</span></span> <span data-ttu-id="29603-335">Bonjour **NameID Policy** zone de texte, type **urn : oasis : noms : tc : SAML:1.1:nameid-format : non spécifiée**.</span><span class="sxs-lookup"><span data-stu-id="29603-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="29603-336">c.</span><span class="sxs-lookup"><span data-stu-id="29603-336">c.</span></span> <span data-ttu-id="29603-337">Bonjour **the AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="29603-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="29603-338">d.</span><span class="sxs-lookup"><span data-stu-id="29603-338">d.</span></span> <span data-ttu-id="29603-339">Désélectionnez **Créer une classe de contexte d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="29603-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="29603-340">Sous **des propriétés de fournisseur de Service supplémentaires**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="29603-341">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="29603-342">a.</span><span class="sxs-lookup"><span data-stu-id="29603-342">a.</span></span> <span data-ttu-id="29603-343">Bonjour **ServiceNow Homepage** zone de texte, tapez l’URL de votre page d’accueil d’instance ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="29603-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="29603-344">page d’accueil d’instance Hello ServiceNow est une concaténation de votre **URL de client ServieNow** et **/navpage.do** (par exemple : `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="29603-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="29603-345">b.</span><span class="sxs-lookup"><span data-stu-id="29603-345">b.</span></span> <span data-ttu-id="29603-346">Bonjour **ID d’entité / émetteur** zone de texte, tapez l’URL de votre locataire ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="29603-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="29603-347">c.</span><span class="sxs-lookup"><span data-stu-id="29603-347">c.</span></span> <span data-ttu-id="29603-348">Bonjour **URI d’Audience** zone de texte, tapez l’URL de votre locataire ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="29603-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="29603-349">d.</span><span class="sxs-lookup"><span data-stu-id="29603-349">d.</span></span> <span data-ttu-id="29603-350">Dans la zone de texte **Variation d’horloge**, entrez **60**.</span><span class="sxs-lookup"><span data-stu-id="29603-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="29603-351">e.</span><span class="sxs-lookup"><span data-stu-id="29603-351">e.</span></span> <span data-ttu-id="29603-352">Bonjour **champ utilisateur** zone de texte, type **messagerie** ou **nom_utilisateur**, selon le champ utilisé toouniquely identifier les utilisateurs dans votre déploiement de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="29603-353">Vous pouvez tooemit de configuration Azure AD un ID d’utilisateur hello Azure AD (nom d’utilisateur principal) ou que vous hello adresse de messagerie comme hello identificateur unique dans le jeton SAML de hello en va de toohello **ServiceNow > attributs > Single Sign-On** section de Hello portail Azure classic et mappage hello souhaité champ toohello **nameidentifier** attribut.</span><span class="sxs-lookup"><span data-stu-id="29603-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="29603-354">valeur de Hello pour l’attribut sélectionné de hello dans Azure AD (par exemple, nom d’utilisateur principal) doit correspondre à valeur hello stocké dans ServiceNow pour le champ hello entrée (par exemple, nom_utilisateur)</span><span class="sxs-lookup"><span data-stu-id="29603-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="29603-355">f.</span><span class="sxs-lookup"><span data-stu-id="29603-355">f.</span></span> <span data-ttu-id="29603-356">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="29603-356">Click **Save**.</span></span> 

3. <span data-ttu-id="29603-357">Sur le portail classique hello Azure AD, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="29603-358">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="29603-359">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="29603-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="29603-360">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="29603-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="29603-361">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="29603-361">Configuring user provisioning</span></span>
<span data-ttu-id="29603-362">objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="29603-363">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="29603-364">Dans hello classique portail de gestion Azure, sur hello **ServiceNow** page d’intégration d’application, cliquez sur **configuration d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29603-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="29603-365">![Approvisionnement d'utilisateurs](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Approvisionnement d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="29603-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="29603-366">Sur hello **Entrez votre déploiement automatique d’utilisateur de ServiceNow informations d’identification tooenable** , fournissez hello suivant les paramètres de configuration :</span><span class="sxs-lookup"><span data-stu-id="29603-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="29603-367">a.</span><span class="sxs-lookup"><span data-stu-id="29603-367">a.</span></span> <span data-ttu-id="29603-368">Bonjour **nom de l’Instance ServiceNow** zone de texte, le nom d’instance de type hello ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="29603-369">b.</span><span class="sxs-lookup"><span data-stu-id="29603-369">b.</span></span> <span data-ttu-id="29603-370">Bonjour **nom d’utilisateur Admin ServiceNow** zone de texte, nom du type hello Hello compte d’administrateur ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="29603-371">c.</span><span class="sxs-lookup"><span data-stu-id="29603-371">c.</span></span> <span data-ttu-id="29603-372">Bonjour **mot de passe Admin ServiceNow** zone de texte, un mot de passe type hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="29603-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="29603-373">d.</span><span class="sxs-lookup"><span data-stu-id="29603-373">d.</span></span> <span data-ttu-id="29603-374">Cliquez sur **valider** tooverify votre configuration.</span><span class="sxs-lookup"><span data-stu-id="29603-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="29603-375">e.</span><span class="sxs-lookup"><span data-stu-id="29603-375">e.</span></span> <span data-ttu-id="29603-376">Cliquez sur hello **suivant** hello tooopen de bouton **étapes** page.</span><span class="sxs-lookup"><span data-stu-id="29603-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="29603-377">f.</span><span class="sxs-lookup"><span data-stu-id="29603-377">f.</span></span> <span data-ttu-id="29603-378">Si vous souhaitez tooprovision tous les utilisateurs toothis application, sélectionnez «**approvisionner automatiquement tous les comptes d’utilisateur dans l’application de hello Active toothis**».</span><span class="sxs-lookup"><span data-stu-id="29603-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="29603-379">![Étapes suivantes](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Étapes suivantes")</span><span class="sxs-lookup"><span data-stu-id="29603-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="29603-380">g.</span><span class="sxs-lookup"><span data-stu-id="29603-380">g.</span></span> <span data-ttu-id="29603-381">Sur hello **étapes** , cliquez sur **Complete** toosave votre configuration.</span><span class="sxs-lookup"><span data-stu-id="29603-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29603-382">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="29603-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="29603-383">Dans cette section, vous créez un utilisateur de test dans le portail classique de hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29603-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="29603-385">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29603-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29603-386">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29603-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="29603-388">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="29603-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="29603-389">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="29603-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29603-391">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29603-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="29603-393">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="29603-395">a.</span><span class="sxs-lookup"><span data-stu-id="29603-395">a.</span></span> <span data-ttu-id="29603-396">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="29603-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="29603-397">b.</span><span class="sxs-lookup"><span data-stu-id="29603-397">b.</span></span> <span data-ttu-id="29603-398">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29603-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="29603-399">c.</span><span class="sxs-lookup"><span data-stu-id="29603-399">c.</span></span> <span data-ttu-id="29603-400">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-400">Click **Next**.</span></span>

6. <span data-ttu-id="29603-401">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="29603-403">a.</span><span class="sxs-lookup"><span data-stu-id="29603-403">a.</span></span> <span data-ttu-id="29603-404">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="29603-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="29603-405">b.</span><span class="sxs-lookup"><span data-stu-id="29603-405">b.</span></span> <span data-ttu-id="29603-406">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="29603-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="29603-407">c.</span><span class="sxs-lookup"><span data-stu-id="29603-407">c.</span></span> <span data-ttu-id="29603-408">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29603-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="29603-409">d.</span><span class="sxs-lookup"><span data-stu-id="29603-409">d.</span></span> <span data-ttu-id="29603-410">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29603-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="29603-411">e.</span><span class="sxs-lookup"><span data-stu-id="29603-411">e.</span></span> <span data-ttu-id="29603-412">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="29603-412">Click **Next**.</span></span>

7. <span data-ttu-id="29603-413">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="29603-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="29603-415">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29603-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="29603-417">a.</span><span class="sxs-lookup"><span data-stu-id="29603-417">a.</span></span> <span data-ttu-id="29603-418">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="29603-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="29603-419">b.</span><span class="sxs-lookup"><span data-stu-id="29603-419">b.</span></span> <span data-ttu-id="29603-420">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="29603-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="29603-421">Création d’un utilisateur de test ServiceNow</span><span class="sxs-lookup"><span data-stu-id="29603-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="29603-422">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="29603-423">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="29603-424">Si vous ne savez pas comment tooadd un dans votre ServiceNow ou le ServiceNow Express compte d’utilisateur, contactez l’équipe de support technique ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="29603-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="29603-425">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="29603-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="29603-426">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooServiceNow de son accès.</span><span class="sxs-lookup"><span data-stu-id="29603-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="29603-428">**tooassign Britta Simon tooServiceNow, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29603-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="29603-429">Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="29603-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="29603-431">Dans la liste des applications hello, sélectionnez **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="29603-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="29603-433">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="29603-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203] 

4. <span data-ttu-id="29603-435">Dans la liste de tous les utilisateurs de hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29603-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="29603-436">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="29603-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="29603-438">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29603-438">Testing single sign-on</span></span>
<span data-ttu-id="29603-439">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29603-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="29603-440">Lorsque vous cliquez sur mosaïque ServiceNow hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ServiceNow application.</span><span class="sxs-lookup"><span data-stu-id="29603-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29603-441">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="29603-441">Additional resources</span></span>
* [<span data-ttu-id="29603-442">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29603-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29603-443">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="29603-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
