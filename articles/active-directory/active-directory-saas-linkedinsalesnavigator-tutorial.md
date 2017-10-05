---
title: "Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Sales Navigator | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LinkedIn Sales Navigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="1ffd5-103">Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="1ffd5-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="1ffd5-104">Dans ce didacticiel, vous allez apprendre à intégrer LinkedIn Sales Navigator dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ffd5-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ffd5-105">L’intégration de LinkedIn Sales Navigator dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1ffd5-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ffd5-106">Dans Azure AD, vous pouvez contrôler qui a accès à LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="1ffd5-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="1ffd5-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à LinkedIn Sales Navigator (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ffd5-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1ffd5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ffd5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ffd5-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ffd5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1ffd5-110">Prerequisites</span></span>

<span data-ttu-id="1ffd5-111">Pour configurer l’intégration d’Azure AD dans LinkedIn Sales Navigator, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1ffd5-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="1ffd5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ffd5-113">Un abonnement LinkedIn Sales Navigator pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1ffd5-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ffd5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ffd5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1ffd5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ffd5-116">Évitez d’utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ffd5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ffd5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ffd5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1ffd5-118">Scenario description</span></span>
<span data-ttu-id="1ffd5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ffd5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ffd5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ffd5-121">Ajout de LinkedIn Sales Navigator à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1ffd5-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="1ffd5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="1ffd5-123">Ajout de LinkedIn Sales Navigator à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1ffd5-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="1ffd5-124">Pour configurer l’intégration de LinkedIn Sales Navigator avec Azure AD, vous devez ajouter LinkedIn Sales Navigator à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ffd5-125">**Pour ajouter LinkedIn Sales Navigator à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ffd5-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ffd5-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ffd5-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ffd5-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1ffd5-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1ffd5-133">Dans la zone de recherche, entrez **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="1ffd5-135">Dans le volet des résultats, sélectionnez **LinkedIn Sales Navigator**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ffd5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ffd5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Sales Navigator par le biais d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1ffd5-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ffd5-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LinkedIn Sales Navigator équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="1ffd5-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LinkedIn Sales Navigator associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="1ffd5-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="1ffd5-142">Pour configurer et tester l’authentification unique Azure AD avec LinkedIn Sales Navigator, vous devez vous conformer aux instructions des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ffd5-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ffd5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ffd5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ffd5-145">**[Création d’un utilisateur de test LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)** pour avoir un équivalent de Britta Simon dans LinkedIn Sales Navigator lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="1ffd5-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ffd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ffd5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ffd5-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="1ffd5-150">**Pour configurer l’authentification unique Azure AD avec LinkedIn Sales Navigator, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ffd5-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="1ffd5-151">Dans le portail Azure, sur la page d’intégration de l’application **LinkedIn Sales Navigator**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1ffd5-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** afin d’activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="1ffd5-155">Dans une autre fenêtre de navigateur web, connectez-vous à votre site web **LinkedIn Sales Navigator** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="1ffd5-156">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="1ffd5-157">En outre, sélectionnez **Sales Navigator** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="1ffd5-159">Cliquez sur **OU cliquez ici pour charger et copier des champs du formulaire** et copiez **ID d’entité** et **URL ACS**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="1ffd5-161">Dans la section **Domaines et URL LinkedIn Sales Navigator** du portail Azure, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="1ffd5-163">a.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-163">a.</span></span> <span data-ttu-id="1ffd5-164">Dans la zone de texte **Identificateur**, entrez **l’ID d’entité** copié à partir de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="1ffd5-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="1ffd5-165">b.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-165">b.</span></span> <span data-ttu-id="1ffd5-166">Dans la zone de texte **URL de réponse**, entrez l’**URL ACS** copiée à partir du portail LinkedIn</span><span class="sxs-lookup"><span data-stu-id="1ffd5-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="1ffd5-167">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode initié par le **fournisseur de service**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="1ffd5-169">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="1ffd5-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="1ffd5-170">Votre application **LinkedIn Sales Navigator** attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="1ffd5-171">La capture d’écran suivante présente un exemple.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-171">The following screenshot shows an example.</span></span> <span data-ttu-id="1ffd5-172">La valeur par défaut pour **Identificateur d’utilisateur** est **user.userprincipalname**, mais LinkedIn Sales Navigator s’attend à ce qu’elle soit mappée sur l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="1ffd5-173">Vous pouvez utiliser l’attribut **user.mail** dans la liste ou utiliser la valeur d’attribut appropriée en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="1ffd5-175">Dans **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** et définissez les attributs.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="1ffd5-176">L’utilisateur doit ajouter quatre revendications nommées **email**, **department**, **firstname** et **lastname** et la valeur doit être mappée respectivement à **user.mail**, **user.department**, **user.givenname** et **user.surname**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="1ffd5-177">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="1ffd5-177">Attribute Name</span></span> | <span data-ttu-id="1ffd5-178">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="1ffd5-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="1ffd5-179">email</span><span class="sxs-lookup"><span data-stu-id="1ffd5-179">email</span></span>| <span data-ttu-id="1ffd5-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="1ffd5-180">user.mail</span></span> |
    | <span data-ttu-id="1ffd5-181">department</span><span class="sxs-lookup"><span data-stu-id="1ffd5-181">department</span></span>| <span data-ttu-id="1ffd5-182">user.department</span><span class="sxs-lookup"><span data-stu-id="1ffd5-182">user.department</span></span> |
    | <span data-ttu-id="1ffd5-183">firstname</span><span class="sxs-lookup"><span data-stu-id="1ffd5-183">firstname</span></span>| <span data-ttu-id="1ffd5-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1ffd5-184">user.givenname</span></span> |
    | <span data-ttu-id="1ffd5-185">lastname</span><span class="sxs-lookup"><span data-stu-id="1ffd5-185">lastname</span></span>| <span data-ttu-id="1ffd5-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="1ffd5-186">user.surname</span></span> |
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="1ffd5-188">a.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-188">a.</span></span> <span data-ttu-id="1ffd5-189">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue associée.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="1ffd5-192">b.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-192">b.</span></span> <span data-ttu-id="1ffd5-193">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1ffd5-194">c.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-194">c.</span></span> <span data-ttu-id="1ffd5-195">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1ffd5-196">d.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-196">d.</span></span> <span data-ttu-id="1ffd5-197">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-197">Click **Ok**</span></span>

10. <span data-ttu-id="1ffd5-198">Effectuez les étapes suivantes au niveau de l’attribut **name**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="1ffd5-199">a.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-199">a.</span></span> <span data-ttu-id="1ffd5-200">Cliquez sur l’attribut pour ouvrir la fenêtre **Modifier l’attribut**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="1ffd5-202">b.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-202">b.</span></span> <span data-ttu-id="1ffd5-203">Supprimez la valeur d’URL dans **namespace**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="1ffd5-204">c.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-204">c.</span></span> <span data-ttu-id="1ffd5-205">Cliquez sur **OK** pour enregistrer le paramètre.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="1ffd5-206">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="1ffd5-208">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1ffd5-208">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="1ffd5-210">Accédez à la section **Paramètres de l’administrateur LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="1ffd5-211">Cliquez sur **Télécharger fichier XML** pour charger le fichier XML de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="1ffd5-213">Cliquez sur **Activer** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="1ffd5-214">L’état de l’authentification unique passe de **Non connecté** à **Connecté**</span><span class="sxs-lookup"><span data-stu-id="1ffd5-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="1ffd5-216">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ffd5-217">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ffd5-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ffd5-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ffd5-219">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ffd5-220">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1ffd5-222">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ffd5-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ffd5-223">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ffd5-225">Allez dans **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ffd5-227">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ffd5-229">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ffd5-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ffd5-231">a.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-231">a.</span></span> <span data-ttu-id="1ffd5-232">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ffd5-233">b.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-233">b.</span></span> <span data-ttu-id="1ffd5-234">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ffd5-235">c.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-235">c.</span></span> <span data-ttu-id="1ffd5-236">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ffd5-237">d.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-237">d.</span></span> <span data-ttu-id="1ffd5-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="1ffd5-239">Création d’un utilisateur de test LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="1ffd5-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="1ffd5-240">L’application LinkedIn Sales Navigator prend en charge la configuration d’utilisateur juste à temps (JIT), et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="1ffd5-241">Activez **Affecter automatiquement les licences** pour affecter une licence à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ffd5-243">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffd5-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ffd5-244">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1ffd5-246">**Pour affecter Britta Simon à LinkedIn Sales Navigator, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ffd5-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="1ffd5-247">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1ffd5-249">Dans la liste des applications, sélectionnez **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="1ffd5-251">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1ffd5-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-253">Click **Add** button.</span></span> <span data-ttu-id="1ffd5-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1ffd5-256">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ffd5-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ffd5-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ffd5-259">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1ffd5-259">Testing single sign-on</span></span>

<span data-ttu-id="1ffd5-260">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1ffd5-261">Lorsque vous cliquez sur la vignette LinkedIn Sales Navigator dans le volet d’accès, vous êtes normalement redirigé vers page d’organisation où vous devez fournir vos informations de compte personnelles LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="1ffd5-262">Votre compte personnel est ainsi lié à votre compte professionnel LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1ffd5-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="1ffd5-263">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1ffd5-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1ffd5-264">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1ffd5-264">Additional resources</span></span>

* [<span data-ttu-id="1ffd5-265">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ffd5-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ffd5-266">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1ffd5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

