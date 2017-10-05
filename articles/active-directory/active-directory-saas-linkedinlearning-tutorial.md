---
title: "Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Learning | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LinkedIn Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="d94c5-103">Didacticiel : Intégration d’Azure Active Directory à LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="d94c5-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="d94c5-104">Dans ce didacticiel, vous allez apprendre à intégrer LinkedIn Learning à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d94c5-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d94c5-105">L’intégration de LinkedIn Learning dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d94c5-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d94c5-106">Dans Azure AD, vous pouvez contrôler qui a accès à LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="d94c5-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="d94c5-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à LinkedIn Learning (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d94c5-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d94c5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d94c5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d94c5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d94c5-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d94c5-110">Prerequisites</span></span>

<span data-ttu-id="d94c5-111">Pour configurer l’intégration d’Azure AD à LinkedIn Learning, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d94c5-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="d94c5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d94c5-113">Un abonnement LinkedIn Learning pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d94c5-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d94c5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d94c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d94c5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d94c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d94c5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d94c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d94c5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d94c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d94c5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d94c5-118">Scenario description</span></span>
<span data-ttu-id="d94c5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d94c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d94c5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d94c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d94c5-121">Ajout de LinkedIn Learning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d94c5-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="d94c5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="d94c5-123">Ajout de LinkedIn Learning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d94c5-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="d94c5-124">Pour configurer l’intégration de LinkedIn Learning à Azure AD, vous devez ajouter LinkedIn Learning à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="d94c5-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d94c5-125">**Pour ajouter LinkedIn Learning à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d94c5-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d94c5-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d94c5-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d94c5-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d94c5-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d94c5-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d94c5-133">Dans la zone de recherche, entrez **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="d94c5-134">Dans le volet de résultats, cliquez sur **LinkedIn Learning** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d94c5-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d94c5-136">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d94c5-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Learning avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d94c5-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d94c5-138">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LinkedIn Learning équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d94c5-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="d94c5-139">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LinkedIn Learning associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d94c5-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="d94c5-140">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="d94c5-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="d94c5-141">Pour configurer et tester l’authentification unique Azure AD avec LinkedIn Learning, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="d94c5-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d94c5-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d94c5-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d94c5-143">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d94c5-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d94c5-144">**[Création d’un utilisateur de test LinkedIn Learning](#creating-a-linkedin-learning-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d94c5-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="d94c5-145">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d94c5-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d94c5-146">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d94c5-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d94c5-147">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d94c5-148">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="d94c5-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="d94c5-149">**Pour configurer l’authentification unique Azure AD avec LinkedIn Learning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d94c5-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="d94c5-150">Dans le portail Azure, dans la page d’intégration de l’application **LinkedIn Learning**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d94c5-152">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d94c5-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="d94c5-154">Dans une autre fenêtre de navigateur web, connectez-vous à votre client LinkedIn Learning en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d94c5-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="d94c5-155">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="d94c5-156">Sélectionnez aussi **Apprentissage - Par défaut** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d94c5-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="d94c5-158">Cliquez sur  **OU cliquez ici pour charger et copier les champs individuels du formulaire**, puis copiez l’**ID d’entité** et l’**URL ACS (Assertion Consumer Access)**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="d94c5-160">Dans la section **Domaines et URL LinkedIn Learning**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en **Mode initié par IDP**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="d94c5-162">a.</span><span class="sxs-lookup"><span data-stu-id="d94c5-162">a.</span></span> <span data-ttu-id="d94c5-163">Dans la zone de texte **Identificateur**, entrez **l’ID d’entité** copié à partir de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="d94c5-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="d94c5-164">b.</span><span class="sxs-lookup"><span data-stu-id="d94c5-164">b.</span></span> <span data-ttu-id="d94c5-165">Dans la zone de texte **URL de réponse**, entrez **l’URL ACS** copiée à partir du portail LinkedIn</span><span class="sxs-lookup"><span data-stu-id="d94c5-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="d94c5-166">Si vous souhaitez configurer l’authentification unique en mode **Initié par SP**, cliquez sur l’option Afficher les paramètres d’URL avancés dans la section de configuration et configurez l’URL d’authentification avec le format suivant :</span><span class="sxs-lookup"><span data-stu-id="d94c5-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="d94c5-168">Votre application LinkedIn Learning attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML .</span><span class="sxs-lookup"><span data-stu-id="d94c5-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="d94c5-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="d94c5-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="d94c5-170">La valeur par défaut pour **Identificateur d’utilisateur** est **user.userprincipalname**, mais LinkedIn Learning s’attend à ce qu’elle soit mappée sur l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d94c5-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="d94c5-171">Pour cela, vous pouvez utiliser l’attribut **user.mail** dans la liste ou utiliser la valeur d’attribut appropriée en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d94c5-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="d94c5-173">Dans **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** et définissez les attributs.</span><span class="sxs-lookup"><span data-stu-id="d94c5-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="d94c5-174">L’utilisateur doit ajouter quatre revendications nommées **email**, **department**, **firstname** et **lastname** et la valeur doit être mappée respectivement à **user.mail**, **user.department**, **user.givenname** et **user.surname**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="d94c5-175">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="d94c5-175">Attribute Name</span></span> | <span data-ttu-id="d94c5-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="d94c5-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d94c5-177">email</span><span class="sxs-lookup"><span data-stu-id="d94c5-177">email</span></span>| <span data-ttu-id="d94c5-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="d94c5-178">user.mail</span></span> |    
    | <span data-ttu-id="d94c5-179">department</span><span class="sxs-lookup"><span data-stu-id="d94c5-179">department</span></span>| <span data-ttu-id="d94c5-180">user.department</span><span class="sxs-lookup"><span data-stu-id="d94c5-180">user.department</span></span> |
    | <span data-ttu-id="d94c5-181">firstname</span><span class="sxs-lookup"><span data-stu-id="d94c5-181">firstname</span></span>| <span data-ttu-id="d94c5-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d94c5-182">user.givenname</span></span> |
    | <span data-ttu-id="d94c5-183">lastname</span><span class="sxs-lookup"><span data-stu-id="d94c5-183">lastname</span></span>| <span data-ttu-id="d94c5-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="d94c5-184">user.surname</span></span> |
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="d94c5-186">a.</span><span class="sxs-lookup"><span data-stu-id="d94c5-186">a.</span></span> <span data-ttu-id="d94c5-187">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue associée.</span><span class="sxs-lookup"><span data-stu-id="d94c5-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d94c5-190">b.</span><span class="sxs-lookup"><span data-stu-id="d94c5-190">b.</span></span> <span data-ttu-id="d94c5-191">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d94c5-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d94c5-192">c.</span><span class="sxs-lookup"><span data-stu-id="d94c5-192">c.</span></span> <span data-ttu-id="d94c5-193">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d94c5-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d94c5-194">d.</span><span class="sxs-lookup"><span data-stu-id="d94c5-194">d.</span></span> <span data-ttu-id="d94c5-195">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-195">Click **Ok**</span></span>

10. <span data-ttu-id="d94c5-196">Effectuez les étapes suivantes au niveau de l’attribut **name**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="d94c5-197">a.</span><span class="sxs-lookup"><span data-stu-id="d94c5-197">a.</span></span> <span data-ttu-id="d94c5-198">Cliquez sur l’attribut pour ouvrir la fenêtre **Modifier l’attribut**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="d94c5-200">b.</span><span class="sxs-lookup"><span data-stu-id="d94c5-200">b.</span></span> <span data-ttu-id="d94c5-201">Supprimez la valeur d’URL dans **namespace**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="d94c5-202">c.</span><span class="sxs-lookup"><span data-stu-id="d94c5-202">c.</span></span> <span data-ttu-id="d94c5-203">Cliquez sur **OK** pour enregistrer le paramètre.</span><span class="sxs-lookup"><span data-stu-id="d94c5-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="d94c5-204">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d94c5-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="d94c5-206">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-206">Click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="d94c5-208">Accédez à la section **Paramètres de l’administrateur LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="d94c5-209">Chargez le fichier XML que vous avez téléchargé à partir du portail Azure en cliquant sur l’option Charger le fichier XML.</span><span class="sxs-lookup"><span data-stu-id="d94c5-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="d94c5-211">Cliquez sur **Activer** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d94c5-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="d94c5-212">L’état de l’authentification unique passe de **Non connecté** à **Connecté**</span><span class="sxs-lookup"><span data-stu-id="d94c5-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d94c5-214">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="d94c5-215">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d94c5-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d94c5-217">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d94c5-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d94c5-218">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d94c5-220">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d94c5-222">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d94c5-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d94c5-224">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d94c5-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d94c5-226">a.</span><span class="sxs-lookup"><span data-stu-id="d94c5-226">a.</span></span> <span data-ttu-id="d94c5-227">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d94c5-228">b.</span><span class="sxs-lookup"><span data-stu-id="d94c5-228">b.</span></span> <span data-ttu-id="d94c5-229">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d94c5-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d94c5-230">c.</span><span class="sxs-lookup"><span data-stu-id="d94c5-230">c.</span></span> <span data-ttu-id="d94c5-231">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d94c5-232">d.</span><span class="sxs-lookup"><span data-stu-id="d94c5-232">d.</span></span> <span data-ttu-id="d94c5-233">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="d94c5-234">Création d’un utilisateur de test LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="d94c5-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="d94c5-235">L’application LinkedIn Learning prend en charge</span><span class="sxs-lookup"><span data-stu-id="d94c5-235">Linked Learning Application supports.</span></span> <span data-ttu-id="d94c5-236">la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="d94c5-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="d94c5-237">Sur la page de paramètres administrateur sur le portail LinkedIn Learning, activez le commutateur **Affecter automatiquement les licences** pour la configuration juste à temps. Cela affectera également une licence à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d94c5-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d94c5-239">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d94c5-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d94c5-240">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="d94c5-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d94c5-242">**Pour affecter Britta Simon à LinkedIn Learning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d94c5-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="d94c5-243">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d94c5-245">Dans la liste des applications, sélectionnez **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="d94c5-247">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d94c5-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-249">Click **Add** button.</span></span> <span data-ttu-id="d94c5-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d94c5-252">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d94c5-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d94c5-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d94c5-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d94c5-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d94c5-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d94c5-255">Testing single sign-on</span></span>

<span data-ttu-id="d94c5-256">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d94c5-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d94c5-257">Lorsque vous cliquez sur la vignette LinkedIn Learning dans le volet d’accès, vous devriez obtenir la page d’authentification Azure et, après une authentification réussie, vous devriez accéder à votre application LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="d94c5-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d94c5-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d94c5-258">Additional resources</span></span>

* [<span data-ttu-id="d94c5-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d94c5-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d94c5-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d94c5-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png