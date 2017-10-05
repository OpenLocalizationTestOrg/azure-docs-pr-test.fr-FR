---
title: "Didacticiel : Intégration d’Azure Active Directory à LinkedIn Elevate | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LinkedIn Elevate."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="ff87f-103">Didacticiel : Intégration d’Azure Active Directory à LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="ff87f-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="ff87f-104">Dans ce didacticiel, vous allez apprendre à intégrer LinkedIn Elevate à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff87f-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff87f-105">L’intégration de LinkedIn Elevate à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ff87f-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff87f-106">Dans Azure AD, vous pouvez contrôler qui a accès à LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="ff87f-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="ff87f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à LinkedIn Elevate (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff87f-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="ff87f-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ff87f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff87f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff87f-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ff87f-110">Prerequisites</span></span>

<span data-ttu-id="ff87f-111">Pour configurer l’intégration d’Azure AD avec LinkedIn Elevate, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ff87f-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="ff87f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff87f-113">Un abonnement LinkedIn Elevate pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ff87f-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff87f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ff87f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff87f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ff87f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff87f-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ff87f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ff87f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff87f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff87f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ff87f-118">Scenario description</span></span>
<span data-ttu-id="ff87f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ff87f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff87f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff87f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff87f-121">Ajout de LinkedIn Elevate à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ff87f-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="ff87f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="ff87f-123">Ajout de LinkedIn Elevate à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ff87f-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="ff87f-124">Pour configurer l’intégration de LinkedIn Elevate à Azure AD, vous devez ajouter LinkedIn Elevate à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ff87f-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff87f-125">**Pour ajouter LinkedIn Elevate à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ff87f-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff87f-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff87f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff87f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ff87f-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ff87f-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ff87f-133">Dans la zone de recherche, entrez **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="ff87f-134">Dans le volet de résultats, cliquez sur **LinkedIn Elevate** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ff87f-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff87f-136">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff87f-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Elevate, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ff87f-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff87f-138">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LinkedIn Elevate équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff87f-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="ff87f-139">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LinkedIn Elevate associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ff87f-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="ff87f-140">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ff87f-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="ff87f-141">Pour configurer et tester l’authentification unique Azure AD avec LinkedIn Elevate, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff87f-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff87f-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ff87f-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff87f-143">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff87f-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff87f-144">**[Création d’un utilisateur de test LinkedIn Elevate](#creating-a-linkedin-elevate-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff87f-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="ff87f-145">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff87f-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff87f-146">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ff87f-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff87f-147">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff87f-148">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ff87f-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="ff87f-149">**Pour configurer l’authentification unique Azure AD avec LinkedIn Elevate, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ff87f-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="ff87f-150">Dans le portail de gestion Azure, sur la page d’intégration de l’application **LinkedIn Elevate**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ff87f-152">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ff87f-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="ff87f-154">Dans une autre fenêtre de navigateur web, connectez-vous à votre client LinkedIn Elevate en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ff87f-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="ff87f-155">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="ff87f-156">En outre, sélectionnez **Elevate - Test AAD Elevate** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ff87f-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="ff87f-158">Cliquez sur **OU cliquez ici pour charger et copier des champs du formulaire** et copiez **ID d’entité** et **URL ACS**</span><span class="sxs-lookup"><span data-stu-id="ff87f-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="ff87f-160">Dans le portail Azure, sous **Domaines et URL LinkedIn Elevate**, suivez les étapes ci-dessous si vous souhaitez configurer le SSO en mode **Initié par IDP**</span><span class="sxs-lookup"><span data-stu-id="ff87f-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="ff87f-162">a.</span><span class="sxs-lookup"><span data-stu-id="ff87f-162">a.</span></span> <span data-ttu-id="ff87f-163">Dans la zone de texte **Identificateur**, entrez **l’ID d’entité** copié à partir de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="ff87f-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="ff87f-164">b.</span><span class="sxs-lookup"><span data-stu-id="ff87f-164">b.</span></span> <span data-ttu-id="ff87f-165">Dans la zone de texte **URL de réponse**, entrez **l’URL ACS** copiée à partir du portail LinkedIn</span><span class="sxs-lookup"><span data-stu-id="ff87f-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="ff87f-166">Si vous souhaitez configurer l’authentification unique en mode **Initié par SP**, cliquez sur l’option Afficher les paramètres d’URL avancés dans la section de configuration et configurez l’URL d’authentification avec le format suivant :</span><span class="sxs-lookup"><span data-stu-id="ff87f-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="ff87f-168">Votre application LinkedIn Elevate attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML .</span><span class="sxs-lookup"><span data-stu-id="ff87f-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ff87f-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="ff87f-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="ff87f-170">La valeur par défaut pour **Identificateur d’utilisateur** est **user.userprincipalname**, mais LinkedIn Elevate s’attend à ce qu’elle soit mappée sur l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ff87f-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="ff87f-171">Pour cela, vous pouvez utiliser l’attribut **user.mail** dans la liste ou utiliser la valeur d’attribut appropriée en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ff87f-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="ff87f-173">Dans **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** et définissez les attributs.</span><span class="sxs-lookup"><span data-stu-id="ff87f-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="ff87f-174">Vous devez ajouter une autre revendication nommée **service**, et la valeur doit être mappée à **user.department**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="ff87f-175">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="ff87f-175">Attribute Name</span></span> | <span data-ttu-id="ff87f-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="ff87f-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="ff87f-177">department</span><span class="sxs-lookup"><span data-stu-id="ff87f-177">department</span></span>| <span data-ttu-id="ff87f-178">user.department</span><span class="sxs-lookup"><span data-stu-id="ff87f-178">user.department</span></span> |

      ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="ff87f-180">a.</span><span class="sxs-lookup"><span data-stu-id="ff87f-180">a.</span></span> <span data-ttu-id="ff87f-181">Cliquez sur Ajouter un attribut pour ouvrir la page de détails de l’attribut et ajouter l’attribut de département comme illustré ci-dessous-</span><span class="sxs-lookup"><span data-stu-id="ff87f-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="ff87f-183">b.</span><span class="sxs-lookup"><span data-stu-id="ff87f-183">b.</span></span> <span data-ttu-id="ff87f-184">Cliquez sur **OK** pour enregistrer l’attribut.</span><span class="sxs-lookup"><span data-stu-id="ff87f-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="ff87f-185">c.</span><span class="sxs-lookup"><span data-stu-id="ff87f-185">c.</span></span> <span data-ttu-id="ff87f-186">Remplacez le nom de l’attribut **emailaddress** par **email**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="ff87f-187">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ff87f-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="ff87f-189">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-189">Click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="ff87f-191">Accédez à la section **Paramètres de l’administrateur LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="ff87f-192">Téléchargez le fichier XML que vous venez de télécharger à partir du portail Azure en cliquant sur l’option Télécharger fichier XML.</span><span class="sxs-lookup"><span data-stu-id="ff87f-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="ff87f-194">Cliquez sur **Activer** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ff87f-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="ff87f-195">L’état de l’authentification unique passera de **Non connecté** à **Connecté**</span><span class="sxs-lookup"><span data-stu-id="ff87f-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff87f-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff87f-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="ff87f-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ff87f-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ff87f-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff87f-201">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff87f-203">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ff87f-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff87f-205">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff87f-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff87f-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff87f-209">a.</span><span class="sxs-lookup"><span data-stu-id="ff87f-209">a.</span></span> <span data-ttu-id="ff87f-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff87f-211">b.</span><span class="sxs-lookup"><span data-stu-id="ff87f-211">b.</span></span> <span data-ttu-id="ff87f-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff87f-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff87f-213">c.</span><span class="sxs-lookup"><span data-stu-id="ff87f-213">c.</span></span> <span data-ttu-id="ff87f-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff87f-215">d.</span><span class="sxs-lookup"><span data-stu-id="ff87f-215">d.</span></span> <span data-ttu-id="ff87f-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="ff87f-217">Création d’un utilisateur test LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="ff87f-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="ff87f-218">L’application LinkedIn Elevate prend en charge la configuration d’utilisateur juste à temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="ff87f-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="ff87f-219">Sur la page de paramètres administrateur sur le portail LinkedIn Elevate, activez le commutateur **Affecter automatiquement les licences** pour la configuration juste à temps. Cela affectera également une licence à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ff87f-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff87f-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff87f-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff87f-222">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ff87f-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ff87f-224">**Pour affecter Britta Simon à LinkedIn Elevate, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ff87f-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="ff87f-225">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ff87f-227">Dans la liste des applications, sélectionnez **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="ff87f-229">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ff87f-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-231">Click **Add** button.</span></span> <span data-ttu-id="ff87f-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ff87f-234">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ff87f-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff87f-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff87f-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ff87f-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff87f-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ff87f-237">Testing single sign-on</span></span>

<span data-ttu-id="ff87f-238">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ff87f-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff87f-239">Lorsque vous cliquez sur la mosaïque LinkedIn Elevate dans le volet d’accès, vous devriez obtenir la page d’authentification Azure et, après une authentification réussie, vous devriez accéder à votre application LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ff87f-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff87f-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ff87f-240">Additional resources</span></span>

* [<span data-ttu-id="ff87f-241">Didacticiel : Configuration de LinkedIn Elevate pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff87f-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="ff87f-242">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff87f-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff87f-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ff87f-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
