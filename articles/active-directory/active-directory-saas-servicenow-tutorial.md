---
title: "Didacticiel : Intégration d’Azure Active Directory à ServiceNow | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Service Now et ServiceNow Express."
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
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="774f3-103">Didacticiel : Intégration d’Azure Active Directory à ServiceNow</span><span class="sxs-lookup"><span data-stu-id="774f3-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="774f3-104">Dans ce didacticiel, vous allez apprendre à intégrer ServiceNow et ServiceNow Express à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="774f3-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="774f3-105">L’intégration de ServiceNow et ServiceNow Express à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="774f3-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="774f3-106">Dans Azure AD, vous pouvez contrôler qui a accès à ServiceNow et ServiceNow Express.</span><span class="sxs-lookup"><span data-stu-id="774f3-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="774f3-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à ServiceNow et ServiceNow Express (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774f3-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="774f3-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="774f3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="774f3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="774f3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="774f3-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="774f3-110">Prerequisites</span></span>
<span data-ttu-id="774f3-111">Pour configurer l’intégration d’Azure AD à ServiceNow et ServiceNow Express, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="774f3-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="774f3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="774f3-112">An Azure AD subscription</span></span>
* <span data-ttu-id="774f3-113">Pour ServiceNow, une instance ou un locataire ServiceNow, version Calgary ou supérieure</span><span class="sxs-lookup"><span data-stu-id="774f3-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="774f3-114">Pour ServiceNow Express, une instance ServiceNow Express, version Helsinki ou supérieure</span><span class="sxs-lookup"><span data-stu-id="774f3-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="774f3-115">Le locataire ServiceNow doit avoir le [plug-in d’authentification unique à plusieurs fournisseurs](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) activé.</span><span class="sxs-lookup"><span data-stu-id="774f3-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="774f3-116">Cette opération est possible en [envoyant une demande de service](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="774f3-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="774f3-117">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="774f3-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="774f3-118">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="774f3-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="774f3-119">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="774f3-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="774f3-120">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="774f3-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="774f3-121">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="774f3-121">Scenario description</span></span>
<span data-ttu-id="774f3-122">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="774f3-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="774f3-123">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="774f3-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="774f3-124">Ajout de ServiceNow à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="774f3-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="774f3-125">Configuration et test de l’authentification unique Azure AD pour ServiceNow ou ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="774f3-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="774f3-126">Ajout de ServiceNow à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="774f3-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="774f3-127">Pour configurer l’intégration de ServiceNow ou ServiceNow Express à Azure AD, vous devez ajouter Service Now depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="774f3-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="774f3-128">**Pour ajouter ServiceNow à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="774f3-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="774f3-129">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="774f3-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="774f3-131">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="774f3-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="774f3-132">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="774f3-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="774f3-134">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="774f3-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="774f3-136">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="774f3-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="774f3-138">Dans la zone de recherche, entrez **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="774f3-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="774f3-140">Dans le volet des résultats, sélectionnez **ServiceNow**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="774f3-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="774f3-142">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="774f3-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="774f3-143">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ServiceNow ou ServiceNow Express avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="774f3-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="774f3-144">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ServiceNow équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774f3-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="774f3-145">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur ServiceNow associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="774f3-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="774f3-146">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="774f3-147">Pour configurer et tester l’authentification unique Azure AD avec ServiceNow, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="774f3-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="774f3-148">**[Configuration de l’authentification unique Azure AD pour ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="774f3-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="774f3-149">**[Configuration de l’authentification unique Azure AD pour ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="774f3-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="774f3-150">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="774f3-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="774f3-151">**[Création d’un utilisateur de test ServiceNow](#creating-a-servicenow-test-user)** pour avoir un équivalent de Britta Simon dans ServiceNow lié à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774f3-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="774f3-152">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774f3-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="774f3-153">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="774f3-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="774f3-154">Si vous voulez configurer ServiceNow, omettez l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="774f3-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="774f3-155">De même, si vous voulez configurer ServiceNow Express, omettez l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="774f3-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="774f3-156">Configuration de l’authentification unique Azure AD pour ServiceNow</span><span class="sxs-lookup"><span data-stu-id="774f3-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="774f3-157">Dans la page d’intégration d’applications **ServiceNow** du portail Azure AD Classic, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="774f3-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="774f3-158">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="774f3-159">Dans la page **Comment voulez-vous que les utilisateurs se connectent à ServiceNow**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="774f3-160">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="774f3-161">Dans la page **Configurer les paramètres de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="774f3-162">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="774f3-163">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-163">a.</span></span> <span data-ttu-id="774f3-164">Dans la zone de texte **URL d’authentification unique ServiceNow**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application ServiceNow : `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="774f3-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="774f3-165">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-165">b.</span></span> <span data-ttu-id="774f3-166">Dans la zone de texte **Identificateur**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application ServiceNow : `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="774f3-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="774f3-167">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-167">c.</span></span> <span data-ttu-id="774f3-168">Cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="774f3-168">Click **Next**</span></span>

4. <span data-ttu-id="774f3-169">Pour permettre à Azure AD de configurer automatiquement ServiceNow pour l’authentification basée SAML, entrez votre nom d’instance ServiceNow, le nom d’utilisateur administrateur et le mot de passe administrateur dans le formulaire **Configurer automatiquement l’authentification unique** puis cliquez sur *Configurer*.</span><span class="sxs-lookup"><span data-stu-id="774f3-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="774f3-170">Notez que le nom d’utilisateur administrateur fourni doit avoir le rôle **security_admin** attribué dans ServiceNow pour que cela fonctionne.</span><span class="sxs-lookup"><span data-stu-id="774f3-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="774f3-171">Sinon, pour configurer manuellement ServiceNow afin d’utiliser Azure AD comme fournisseur d’identité SAML, cliquez sur **Configurer manuellement l’application pour l’authentification unique**, sur **Suivant**, puis effectuez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="774f3-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="774f3-172">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="774f3-173">Dans la page **Configurer l’authentification unique à ServiceNow**, cliquez sur **Télécharger le certificat**, enregistrez le fichier de certificat en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="774f3-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="774f3-174">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="774f3-175">Connectez-vous à votre application ServiceNow en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="774f3-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="774f3-176">Activez le plug-in *Integration - Multiple Provider Single Sign-On Installer* (Intégration - Programme d’installation de l’authentification unique à plusieurs fournisseurs) en suivant la procédure ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="774f3-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="774f3-177">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-177">a.</span></span> <span data-ttu-id="774f3-178">Dans le volet de navigation à gauche, accédez à la section **System Definition** (Définition du système), puis cliquez sur **Plugins** (Plug-ins).</span><span class="sxs-lookup"><span data-stu-id="774f3-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="774f3-179">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activer le plug-in")</span><span class="sxs-lookup"><span data-stu-id="774f3-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="774f3-180">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-180">b.</span></span> <span data-ttu-id="774f3-181">Recherchez *Integration - Multiple Provider Single Sign-On Installer* (Intégration - Programme d’installation de l’authentification unique à plusieurs fournisseurs).</span><span class="sxs-lookup"><span data-stu-id="774f3-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="774f3-182">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activer le plug-in")</span><span class="sxs-lookup"><span data-stu-id="774f3-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="774f3-183">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-183">c.</span></span> <span data-ttu-id="774f3-184">Sélectionnez le plug-in.</span><span class="sxs-lookup"><span data-stu-id="774f3-184">Select the plugin.</span></span> <span data-ttu-id="774f3-185">Cliquez avec le bouton droit et sélectionnez **Activate/Upgrade** (Activer/Mettre à niveau).</span><span class="sxs-lookup"><span data-stu-id="774f3-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="774f3-186">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-186">d.</span></span> <span data-ttu-id="774f3-187">Cliquez sur le bouton **Activate** (Activer).</span><span class="sxs-lookup"><span data-stu-id="774f3-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="774f3-188">À gauche du volet de navigation, cliquez sur **Properties**.</span><span class="sxs-lookup"><span data-stu-id="774f3-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="774f3-189">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="774f3-190">Dans la boîte de dialogue **Multiple Provider SSO Properties** , effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="774f3-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="774f3-191">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="774f3-192">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-192">a.</span></span> <span data-ttu-id="774f3-193">Pour **Enable multiple provider SSO**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="774f3-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="774f3-194">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-194">b.</span></span> <span data-ttu-id="774f3-195">Pour **Enable debug logging got the multiple provider SSO integration**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="774f3-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="774f3-196">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-196">c.</span></span> <span data-ttu-id="774f3-197">Dans la zone de texte **The field on the user table that...**, entrez **user_name**.</span><span class="sxs-lookup"><span data-stu-id="774f3-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="774f3-198">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-198">d.</span></span> <span data-ttu-id="774f3-199">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-199">Click **Save**.</span></span>

10. <span data-ttu-id="774f3-200">À gauche du volet de navigation, cliquez sur **x509 Certificates**.</span><span class="sxs-lookup"><span data-stu-id="774f3-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="774f3-201">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="774f3-202">Dans la boîte de dialogue **X.509 Certificates**, cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="774f3-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="774f3-203">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="774f3-204">Dans la boîte de dialogue **X.509 Certificates** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="774f3-205">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="774f3-206">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-206">a.</span></span> <span data-ttu-id="774f3-207">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="774f3-207">Click **New**.</span></span>
    
     <span data-ttu-id="774f3-208">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-208">b.</span></span> <span data-ttu-id="774f3-209">Dans la zone de texte **Name**, indiquez le nom de votre configuration (p. ex., **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="774f3-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="774f3-210">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-210">c.</span></span> <span data-ttu-id="774f3-211">Sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="774f3-211">Select **Active**.</span></span>
    
     <span data-ttu-id="774f3-212">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-212">d.</span></span> <span data-ttu-id="774f3-213">Pour **Format**, sélectionnez **PEM**.</span><span class="sxs-lookup"><span data-stu-id="774f3-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="774f3-214">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-214">e.</span></span> <span data-ttu-id="774f3-215">Pour **Type**, sélectionnez **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="774f3-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="774f3-216">f.</span><span class="sxs-lookup"><span data-stu-id="774f3-216">f.</span></span> <span data-ttu-id="774f3-217">Ouvrez votre certificat codé en base64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **PEM Certificate** (Certificat PEM).</span><span class="sxs-lookup"><span data-stu-id="774f3-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="774f3-218">g.</span><span class="sxs-lookup"><span data-stu-id="774f3-218">g.</span></span> <span data-ttu-id="774f3-219">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="774f3-219">Click **Update**.</span></span>

13. <span data-ttu-id="774f3-220">À gauche du volet de navigation, cliquez sur **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="774f3-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="774f3-221">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="774f3-222">Dans la boîte de dialogue **Identity Providers**, cliquez sur **New** :</span><span class="sxs-lookup"><span data-stu-id="774f3-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="774f3-223">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="774f3-224">Dans la boîte de dialogue **Identity Providers**, cliquez sur **SAML2 Update1?** :</span><span class="sxs-lookup"><span data-stu-id="774f3-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="774f3-225">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="774f3-226">Dans la boîte de dialogue SAML2 Update1 Properties, effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="774f3-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="774f3-227">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="774f3-228">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-228">a.</span></span> <span data-ttu-id="774f3-229">Dans la zone de texte **Nom**, tapez le nom de votre configuration (ex. **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="774f3-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="774f3-230">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-230">b.</span></span> <span data-ttu-id="774f3-231">Dans la zone de texte **Champ utilisateur**, tapez **email** ou **user_name**, selon le champ utilisé pour identifier les utilisateurs dans votre déploiement ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="774f3-232">Vous pouvez configurer Azure AD afin d’émettre l’ID d’utilisateur Azure AD (nom d’utilisateur principal) ou l’adresse de messagerie comme identificateur unique dans le jeton SAML en accédant à la section **ServiceNow > Attributes > Single Sign-On** (ServiceNow > Attributs > Authentification unique) du portail Azure Classic et en mappant le champ souhaité à l’attribut **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="774f3-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="774f3-233">La valeur stockée pour l’attribut sélectionné dans Azure AD (par exemple, nom d’utilisateur principal) doit correspondre à la valeur stockée dans ServiceNow pour le champ saisi (par exemple, user_name)</span><span class="sxs-lookup"><span data-stu-id="774f3-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="774f3-234">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-234">c.</span></span> <span data-ttu-id="774f3-235">Dans le portail Azure AD Classic, copiez la valeur de **l’ID de fournisseur d’identité**, puis collez-la dans la zone de texte **URL de fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="774f3-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="774f3-236">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-236">d.</span></span> <span data-ttu-id="774f3-237">Dans le portail Azure AD Classic, copiez la valeur de **l’URL de la demande d’authentification**, puis collez-la dans la zone de texte **Demande d’authentification du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="774f3-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="774f3-238">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-238">e.</span></span> <span data-ttu-id="774f3-239">Dans le portail Azure AD Classic, copiez la valeur de **l’URL du service de déconnexion unique**, puis collez-la dans la zone de texte **Demande de déconnexion unique du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="774f3-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="774f3-240">f.</span><span class="sxs-lookup"><span data-stu-id="774f3-240">f.</span></span> <span data-ttu-id="774f3-241">Dans la zone de texte **Page d’accueil ServiceNow** , entrez l’URL de la page d’accueil de votre instance ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="774f3-242">La page d’accueil de l’instance ServiceNow est une concaténation de votre **URL de locataire ServiceNow** et de **/navpage.do** (p. ex., `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="774f3-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="774f3-243">g.</span><span class="sxs-lookup"><span data-stu-id="774f3-243">g.</span></span> <span data-ttu-id="774f3-244">Dans la zone de texte **ID de l’entité / Émetteur** , entrez l’URL de votre locataire ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="774f3-245">h.</span><span class="sxs-lookup"><span data-stu-id="774f3-245">h.</span></span> <span data-ttu-id="774f3-246">Dans la zone de texte **URL de l’audience** , entrez l’URL de votre locataire ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="774f3-247">i.</span><span class="sxs-lookup"><span data-stu-id="774f3-247">i.</span></span> <span data-ttu-id="774f3-248">Dans la zone de texte **Liaison du protocole pour la demande de déconnexion unique du fournisseur d’identité**, entrez **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="774f3-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="774f3-249">j.</span><span class="sxs-lookup"><span data-stu-id="774f3-249">j.</span></span> <span data-ttu-id="774f3-250">Dans la zone de texte Stratégie d’ID de nom, entrez **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="774f3-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="774f3-251">k.</span><span class="sxs-lookup"><span data-stu-id="774f3-251">k.</span></span> <span data-ttu-id="774f3-252">Désélectionnez **Créer une classe de contexte d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="774f3-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="774f3-253">l.</span><span class="sxs-lookup"><span data-stu-id="774f3-253">l.</span></span> <span data-ttu-id="774f3-254">Dans **AuthnContextClassRef Method**, entrez `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="774f3-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="774f3-255">Cela n’est nécessaire que si votre organisation utilise uniquement le cloud.</span><span class="sxs-lookup"><span data-stu-id="774f3-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="774f3-256">Si vous utilisez des services ADFS ou MFA locaux pour l’authentification, vous ne devez pas configurer cette valeur.</span><span class="sxs-lookup"><span data-stu-id="774f3-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="774f3-257">m.</span><span class="sxs-lookup"><span data-stu-id="774f3-257">m.</span></span> <span data-ttu-id="774f3-258">Dans la zone de texte **Variation d’horloge**, entrez **60**.</span><span class="sxs-lookup"><span data-stu-id="774f3-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="774f3-259">n.</span><span class="sxs-lookup"><span data-stu-id="774f3-259">n.</span></span> <span data-ttu-id="774f3-260">Pour **Script d’authentification unique**, sélectionnez **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="774f3-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="774f3-261">o.</span><span class="sxs-lookup"><span data-stu-id="774f3-261">o.</span></span> <span data-ttu-id="774f3-262">Pour **Certificat x509**, sélectionnez le certificat que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="774f3-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="774f3-263">p.</span><span class="sxs-lookup"><span data-stu-id="774f3-263">p.</span></span> <span data-ttu-id="774f3-264">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="774f3-265">Dans le portail Azure AD Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="774f3-266">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="774f3-267">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="774f3-268">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="774f3-269">Configuration de l’authentification unique Azure AD pour ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="774f3-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="774f3-270">Dans la page d’intégration d’applications **ServiceNow** du portail Azure AD Classic, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="774f3-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="774f3-271">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="774f3-272">Dans la page **Comment voulez-vous que les utilisateurs se connectent à ServiceNow**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="774f3-273">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="774f3-274">Dans la page **Configurer les paramètres de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="774f3-275">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="774f3-276">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-276">a.</span></span> <span data-ttu-id="774f3-277">Dans la zone de texte **URL d’authentification unique ServiceNow**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application ServiceNow : `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="774f3-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="774f3-278">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-278">b.</span></span> <span data-ttu-id="774f3-279">Dans la zone de texte **URL de l’émetteur**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application ServiceNow `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="774f3-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="774f3-280">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-280">c.</span></span> <span data-ttu-id="774f3-281">Cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="774f3-281">Click **Next**</span></span>

4. <span data-ttu-id="774f3-282">Cliquez sur **Configurer manuellement l'authentification unique pour cette application**, puis cliquez sur **Suivant** et suivez la procédure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="774f3-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="774f3-283">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="774f3-284">Dans la page **Configurer l’authentification unique à ServiceNow**, cliquez sur **Télécharger le certificat**, enregistrez le fichier de certificat en local sur votre ordinateur, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="774f3-285">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="774f3-286">Connectez-vous à votre application ServiceNow Express en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="774f3-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="774f3-287">Dans le volet de navigation à gauche, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="774f3-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="774f3-288">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="774f3-289">Dans la boîte de dialogue **Authentification unique**, cliquez sur l’icône de configuration en haut à droite et définissez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="774f3-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="774f3-290">![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="774f3-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="774f3-291">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-291">a.</span></span> <span data-ttu-id="774f3-292">Activez **Enable multiple provider SSO** (Activer l’authentification unique à plusieurs fournisseurs) à droite.</span><span class="sxs-lookup"><span data-stu-id="774f3-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="774f3-293">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-293">b.</span></span> <span data-ttu-id="774f3-294">Activez **Enable debug logging for the multiple provider SSO integration** (Activer l’enregistrement du débogage pour l’intégration de l’authentification unique à plusieurs fournisseurs) à droite.</span><span class="sxs-lookup"><span data-stu-id="774f3-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="774f3-295">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-295">c.</span></span> <span data-ttu-id="774f3-296">Dans la zone de texte **The field on the user table that...**, entrez **user_name**.</span><span class="sxs-lookup"><span data-stu-id="774f3-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="774f3-297">Dans la boîte de dialogue **Authentification unique**, cliquez sur **Add New Certificate** (Ajouter un nouveau certificat).</span><span class="sxs-lookup"><span data-stu-id="774f3-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="774f3-298">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="774f3-299">Dans la boîte de dialogue **X.509 Certificates** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="774f3-300">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="774f3-301">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-301">a.</span></span> <span data-ttu-id="774f3-302">Dans la zone de texte **Name**, indiquez le nom de votre configuration (p. ex., **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="774f3-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="774f3-303">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-303">b.</span></span> <span data-ttu-id="774f3-304">Sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="774f3-304">Select **Active**.</span></span>
    
    <span data-ttu-id="774f3-305">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-305">c.</span></span> <span data-ttu-id="774f3-306">Pour **Format**, sélectionnez **PEM**.</span><span class="sxs-lookup"><span data-stu-id="774f3-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="774f3-307">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-307">d.</span></span> <span data-ttu-id="774f3-308">Pour **Type**, sélectionnez **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="774f3-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="774f3-309">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-309">e.</span></span> <span data-ttu-id="774f3-310">Créez un fichier codé en base64 à partir du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="774f3-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="774f3-311">Pour plus d’informations, consultez [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="774f3-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="774f3-312">f.</span><span class="sxs-lookup"><span data-stu-id="774f3-312">f.</span></span> <span data-ttu-id="774f3-313">Ouvrez votre certificat codé en base64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **PEM Certificate** (Certificat PEM).</span><span class="sxs-lookup"><span data-stu-id="774f3-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="774f3-314">g.</span><span class="sxs-lookup"><span data-stu-id="774f3-314">g.</span></span> <span data-ttu-id="774f3-315">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="774f3-315">Click **Update**.</span></span>
11. <span data-ttu-id="774f3-316">Dans la boîte de dialogue **Authentification unique**, cliquez sur **Add New IdP** (Ajouter un nouveau fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="774f3-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="774f3-317">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="774f3-318">Dans la boîte de dialogue **Add New Identity Provider** (Ajouter un nouveau fournisseur d’identité), sous **Configure Identity Provider** (Configurer un fournisseur d’identité), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="774f3-319">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="774f3-320">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-320">a.</span></span> <span data-ttu-id="774f3-321">Dans la zone de texte **Nom**, tapez le nom de votre configuration (par ex., **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="774f3-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="774f3-322">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-322">b.</span></span> <span data-ttu-id="774f3-323">Dans le portail Azure AD Classic, copiez la valeur de **l’ID de fournisseur d’identité**, puis collez-la dans la zone de texte **URL de fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="774f3-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="774f3-324">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-324">c.</span></span> <span data-ttu-id="774f3-325">Dans le portail Azure AD Classic, copiez la valeur de **l’URL de la demande d’authentification**, puis collez-la dans la zone de texte **Demande d’authentification du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="774f3-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="774f3-326">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-326">d.</span></span> <span data-ttu-id="774f3-327">Dans le portail Azure AD Classic, copiez la valeur de **l’URL du service de déconnexion unique**, puis collez-la dans la zone de texte **Demande de déconnexion unique du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="774f3-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="774f3-328">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-328">e.</span></span> <span data-ttu-id="774f3-329">Pour **Identity Provider Certificate** (Certificat du fournisseur d’identité), sélectionnez le certificat que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="774f3-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="774f3-330">Cliquez sur **Advanced Settings** (Paramètres avancés), et sous **Additional Identity Provider Properties** (Autres propriétés du fournisseur d’identité), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="774f3-331">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="774f3-332">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-332">a.</span></span> <span data-ttu-id="774f3-333">Dans la zone de texte **Liaison du protocole pour la demande de déconnexion unique du fournisseur d’identité**, entrez **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="774f3-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="774f3-334">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-334">b.</span></span> <span data-ttu-id="774f3-335">Dans la zone de texte **Stratégie d’ID de nom**, entrez **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="774f3-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="774f3-336">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-336">c.</span></span> <span data-ttu-id="774f3-337">Dans la **méthode AuthnContextClassRef**, saisissez **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="774f3-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="774f3-338">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-338">d.</span></span> <span data-ttu-id="774f3-339">Désélectionnez **Créer une classe de contexte d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="774f3-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="774f3-340">Sous **Additional Service Provider Properties** (Autres propriétés du fournisseur d’identité), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="774f3-341">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="774f3-342">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-342">a.</span></span> <span data-ttu-id="774f3-343">Dans la zone de texte **Page d’accueil ServiceNow** , entrez l’URL de la page d’accueil de votre instance ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="774f3-344">La page d’accueil de l’instance ServiceNow est une concaténation de votre **URL de locataire ServiceNow** et de **/navpage.do** (p. ex., `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="774f3-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="774f3-345">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-345">b.</span></span> <span data-ttu-id="774f3-346">Dans la zone de texte **ID de l’entité / Émetteur** , entrez l’URL de votre locataire ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="774f3-347">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-347">c.</span></span> <span data-ttu-id="774f3-348">Dans la zone de texte **URI d’audience** , entrez l’URL de votre locataire ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="774f3-349">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-349">d.</span></span> <span data-ttu-id="774f3-350">Dans la zone de texte **Variation d’horloge**, entrez **60**.</span><span class="sxs-lookup"><span data-stu-id="774f3-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="774f3-351">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-351">e.</span></span> <span data-ttu-id="774f3-352">Dans la zone de texte **Champ utilisateur**, tapez **email** ou **user_name**, selon le champ utilisé pour identifier les utilisateurs dans votre déploiement ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="774f3-353">Vous pouvez configurer Azure AD afin d’émettre l’ID d’utilisateur Azure AD (nom d’utilisateur principal) ou l’adresse de messagerie comme identificateur unique dans le jeton SAML en accédant à la section **ServiceNow > Attributes > Single Sign-On** (ServiceNow > Attributs > Authentification unique) du portail Azure Classic et en mappant le champ souhaité à l’attribut **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="774f3-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="774f3-354">La valeur stockée pour l’attribut sélectionné dans Azure AD (par exemple, nom d’utilisateur principal) doit correspondre à la valeur stockée dans ServiceNow pour le champ saisi (par exemple, user_name)</span><span class="sxs-lookup"><span data-stu-id="774f3-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="774f3-355">f.</span><span class="sxs-lookup"><span data-stu-id="774f3-355">f.</span></span> <span data-ttu-id="774f3-356">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-356">Click **Save**.</span></span> 

3. <span data-ttu-id="774f3-357">Dans le portail Azure AD Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="774f3-358">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="774f3-359">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="774f3-360">![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="774f3-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="774f3-361">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="774f3-361">Configuring user provisioning</span></span>
<span data-ttu-id="774f3-362">Cette section décrit comment activer l’approvisionnement des utilisateurs des comptes d’utilisateurs Active Directory sur ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="774f3-363">Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="774f3-364">Dans la page d’intégration d’applications **ServiceNow** du portail de gestion Azure Classic, cliquez sur **Configurer l’approvisionnement d’utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="774f3-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="774f3-365">![Approvisionnement d'utilisateurs](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Approvisionnement d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="774f3-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="774f3-366">Dans la page **Entrez vos informations d’identification ServiceNow pour activer la configuration automatique d’un utilisateur**, indiquez les paramètres de configuration suivants :</span><span class="sxs-lookup"><span data-stu-id="774f3-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="774f3-367">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-367">a.</span></span> <span data-ttu-id="774f3-368">Dans la zone de texte **Nom de l'Instance ServiceNow** , tapez le nom d'instance ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="774f3-369">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-369">b.</span></span> <span data-ttu-id="774f3-370">Dans la zone de texte **Nom d’utilisateur admin ServiceNow** , entrez le nom du compte d’administrateur ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="774f3-371">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-371">c.</span></span> <span data-ttu-id="774f3-372">Dans la zone de texte **Mot de passe de l’admin ServiceNow** , entrez le mot de passe de ce compte.</span><span class="sxs-lookup"><span data-stu-id="774f3-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="774f3-373">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-373">d.</span></span> <span data-ttu-id="774f3-374">Cliquez sur **Valider** pour vérifier votre configuration.</span><span class="sxs-lookup"><span data-stu-id="774f3-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="774f3-375">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-375">e.</span></span> <span data-ttu-id="774f3-376">Cliquez sur le bouton **Suivant** pour ouvrir la page **Étapes suivantes**.</span><span class="sxs-lookup"><span data-stu-id="774f3-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="774f3-377">f.</span><span class="sxs-lookup"><span data-stu-id="774f3-377">f.</span></span> <span data-ttu-id="774f3-378">Si vous voulez approvisionner tous les utilisateurs pour cette application, sélectionnez «**Approvisionner automatiquement tous les comptes du répertoire dans cette application**».</span><span class="sxs-lookup"><span data-stu-id="774f3-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="774f3-379">![Étapes suivantes](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Étapes suivantes")</span><span class="sxs-lookup"><span data-stu-id="774f3-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="774f3-380">g.</span><span class="sxs-lookup"><span data-stu-id="774f3-380">g.</span></span> <span data-ttu-id="774f3-381">Sur la page **Étapes suivantes**, cliquez sur **Terminer** pour enregistrer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="774f3-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="774f3-382">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="774f3-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="774f3-383">Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="774f3-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="774f3-385">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="774f3-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="774f3-386">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="774f3-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="774f3-388">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="774f3-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="774f3-389">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="774f3-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="774f3-391">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="774f3-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="774f3-393">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="774f3-395">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-395">a.</span></span> <span data-ttu-id="774f3-396">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="774f3-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="774f3-397">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-397">b.</span></span> <span data-ttu-id="774f3-398">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="774f3-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="774f3-399">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-399">c.</span></span> <span data-ttu-id="774f3-400">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-400">Click **Next**.</span></span>

6. <span data-ttu-id="774f3-401">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="774f3-403">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-403">a.</span></span> <span data-ttu-id="774f3-404">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="774f3-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="774f3-405">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-405">b.</span></span> <span data-ttu-id="774f3-406">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="774f3-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="774f3-407">c.</span><span class="sxs-lookup"><span data-stu-id="774f3-407">c.</span></span> <span data-ttu-id="774f3-408">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="774f3-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="774f3-409">d.</span><span class="sxs-lookup"><span data-stu-id="774f3-409">d.</span></span> <span data-ttu-id="774f3-410">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="774f3-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="774f3-411">e.</span><span class="sxs-lookup"><span data-stu-id="774f3-411">e.</span></span> <span data-ttu-id="774f3-412">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="774f3-412">Click **Next**.</span></span>

7. <span data-ttu-id="774f3-413">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="774f3-415">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="774f3-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="774f3-417">a.</span><span class="sxs-lookup"><span data-stu-id="774f3-417">a.</span></span> <span data-ttu-id="774f3-418">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="774f3-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="774f3-419">b.</span><span class="sxs-lookup"><span data-stu-id="774f3-419">b.</span></span> <span data-ttu-id="774f3-420">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="774f3-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="774f3-421">Création d’un utilisateur de test ServiceNow</span><span class="sxs-lookup"><span data-stu-id="774f3-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="774f3-422">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="774f3-423">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="774f3-424">Si vous ne savez pas comment ajouter un utilisateur dans votre compte ServiceNow ou ServiceNow Express, contactez l’équipe de support technique de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="774f3-425">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="774f3-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="774f3-426">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="774f3-428">**Pour attribuer Britta Simon à ServiceNow, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="774f3-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="774f3-429">Pour ouvrir la vue des applications dans le portail Azure Classic, dans la vue d’annuaire, cliquez sur l’option **Applications** figurant dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="774f3-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="774f3-431">Dans la liste des applications, sélectionnez **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="774f3-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="774f3-433">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="774f3-433">In the menu on the top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203] 

4. <span data-ttu-id="774f3-435">Dans la liste Tous les utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="774f3-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="774f3-436">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="774f3-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="774f3-438">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="774f3-438">Testing single sign-on</span></span>
<span data-ttu-id="774f3-439">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="774f3-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="774f3-440">Lorsque vous cliquez sur la vignette ServiceNow dans le volet d’accès, vous devez être connecté automatiquement à votre application ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="774f3-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="774f3-441">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="774f3-441">Additional resources</span></span>
* [<span data-ttu-id="774f3-442">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="774f3-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="774f3-443">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="774f3-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
