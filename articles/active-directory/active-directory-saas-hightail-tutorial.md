---
title: "Didacticiel : Intégration d’Azure Active Directory à Hightail | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="48d60-103">Didacticiel : Intégration d’Azure Active Directory à Hightail</span><span class="sxs-lookup"><span data-stu-id="48d60-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="48d60-104">Dans ce didacticiel, vous allez apprendre à intégrer Hightail à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48d60-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48d60-105">L’intégration de Hightail à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="48d60-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48d60-106">Dans Azure AD, vous pouvez contrôler qui a accès à Hightail</span><span class="sxs-lookup"><span data-stu-id="48d60-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="48d60-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Hightail (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48d60-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48d60-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="48d60-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48d60-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48d60-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48d60-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="48d60-110">Prerequisites</span></span>

<span data-ttu-id="48d60-111">Pour configurer l’intégration d’Azure AD à Hightail, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="48d60-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="48d60-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="48d60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48d60-113">Un abonnement Hightail pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="48d60-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48d60-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="48d60-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48d60-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="48d60-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48d60-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="48d60-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48d60-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48d60-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48d60-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="48d60-118">Scenario description</span></span>
<span data-ttu-id="48d60-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="48d60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48d60-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="48d60-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48d60-121">Ajout de Hightail à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="48d60-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="48d60-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="48d60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="48d60-123">Ajout de Hightail à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="48d60-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="48d60-124">Pour configurer l’intégration de Hightail à Azure AD, vous devez ajouter Hightail, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="48d60-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48d60-125">**Pour ajouter Hightail à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48d60-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48d60-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48d60-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48d60-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="48d60-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48d60-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="48d60-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="48d60-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="48d60-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="48d60-133">Dans la zone de recherche, tapez **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="48d60-133">In the search box, type **Hightail**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="48d60-135">Dans le panneau des résultats, sélectionnez **Hightail**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="48d60-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48d60-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="48d60-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48d60-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Hightail avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="48d60-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48d60-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Hightail équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48d60-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="48d60-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Hightail associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="48d60-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="48d60-141">Dans Hightail, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="48d60-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48d60-142">Pour configurer et tester l’authentification unique Azure AD avec Hightail, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="48d60-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48d60-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="48d60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48d60-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48d60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48d60-145">**[Création d’un utilisateur de test Hightail](#creating-a-hightail-test-user)** pour avoir un équivalent de Britta Simon dans Hightail lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="48d60-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48d60-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48d60-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48d60-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="48d60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48d60-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="48d60-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48d60-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Hightail.</span><span class="sxs-lookup"><span data-stu-id="48d60-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="48d60-150">**Pour configurer l’authentification unique Azure AD avec Hightail, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48d60-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="48d60-151">Dans le portail Azure, sur la page d’intégration de l’application **Hightail**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="48d60-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="48d60-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="48d60-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="48d60-155">Dans la section **Domaine et URL Hightail**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48d60-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="48d60-157">Dans la zone de texte **URL de réponse**, tapez l’URL : `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="48d60-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48d60-158">La valeur ci-dessus n’est pas une valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="48d60-158">The preceding value is not real value.</span></span> <span data-ttu-id="48d60-159">Vous mettrez à jour la valeur avec l’URL de réponse réelle. La procédure est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="48d60-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="48d60-160">Dans la section **Domaine et URL Hightail**, si vous souhaitez configurer l’application en **Mode initié par SP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48d60-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="48d60-162">a.</span><span class="sxs-lookup"><span data-stu-id="48d60-162">a.</span></span> <span data-ttu-id="48d60-163">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="48d60-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="48d60-164">b.</span><span class="sxs-lookup"><span data-stu-id="48d60-164">b.</span></span> <span data-ttu-id="48d60-165">Dans la zone de texte **URL d’authentification**, saisissez l’URL : `https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="48d60-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="48d60-166">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="48d60-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="48d60-168">L’application Hightail attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="48d60-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="48d60-169">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="48d60-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="48d60-170">Vous pouvez gérer les valeurs de ces attributs à partir de l’onglet **Attribut** de l’application.</span><span class="sxs-lookup"><span data-stu-id="48d60-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="48d60-171">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="48d60-171">The following screenshot shows an example for this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="48d60-173">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48d60-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="48d60-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="48d60-174">Attribute Name</span></span> | <span data-ttu-id="48d60-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="48d60-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="48d60-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="48d60-176">FirstName</span></span> | <span data-ttu-id="48d60-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="48d60-177">user.givenname</span></span> |
    | <span data-ttu-id="48d60-178">LastName</span><span class="sxs-lookup"><span data-stu-id="48d60-178">LastName</span></span> | <span data-ttu-id="48d60-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="48d60-179">user.surname</span></span> |
    | <span data-ttu-id="48d60-180">Email</span><span class="sxs-lookup"><span data-stu-id="48d60-180">Email</span></span> | <span data-ttu-id="48d60-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="48d60-181">user.mail</span></span> |    
    | <span data-ttu-id="48d60-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="48d60-182">UserIdentity</span></span> | <span data-ttu-id="48d60-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="48d60-183">user.mail</span></span> |
    
    <span data-ttu-id="48d60-184">a.</span><span class="sxs-lookup"><span data-stu-id="48d60-184">a.</span></span> <span data-ttu-id="48d60-185">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="48d60-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="48d60-188">b.</span><span class="sxs-lookup"><span data-stu-id="48d60-188">b.</span></span> <span data-ttu-id="48d60-189">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="48d60-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="48d60-190">c.</span><span class="sxs-lookup"><span data-stu-id="48d60-190">c.</span></span> <span data-ttu-id="48d60-191">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="48d60-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="48d60-192">d.</span><span class="sxs-lookup"><span data-stu-id="48d60-192">d.</span></span> <span data-ttu-id="48d60-193">Laissez le champ **Espace de noms** vide.</span><span class="sxs-lookup"><span data-stu-id="48d60-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="48d60-194">e.</span><span class="sxs-lookup"><span data-stu-id="48d60-194">e.</span></span> <span data-ttu-id="48d60-195">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="48d60-195">Click **Ok**.</span></span>

7. <span data-ttu-id="48d60-196">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="48d60-196">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="48d60-198">Dans la section **Configuration de Hightail** , cliquez sur **Configurer Hightail** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="48d60-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48d60-199">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="48d60-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="48d60-201">Avant de configurer l’authentification unique sur l’application Hightail, ajoutez votre domaine de messagerie à la liste approuvée de l’équipe Hightail afin que tous les utilisateurs de ce domaine puissent utiliser la fonctionnalité d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="48d60-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="48d60-202">Pour que l’authentification unique soit configurée pour votre application, vous devez vous connecter à votre locataire Hightail en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="48d60-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="48d60-203">a.</span><span class="sxs-lookup"><span data-stu-id="48d60-203">a.</span></span> <span data-ttu-id="48d60-204">Dans le menu situé en haut, cliquez sur l’onglet **Compte** et sélectionnez **Configure SAML** (Configurer SAML).</span><span class="sxs-lookup"><span data-stu-id="48d60-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="48d60-206">b.</span><span class="sxs-lookup"><span data-stu-id="48d60-206">b.</span></span> <span data-ttu-id="48d60-207">Cochez la case **Enable SAML Authentication**(Activer l’authentification SAML).</span><span class="sxs-lookup"><span data-stu-id="48d60-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="48d60-209">c.</span><span class="sxs-lookup"><span data-stu-id="48d60-209">c.</span></span> <span data-ttu-id="48d60-210">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **Certificat de signature de jeton SAML**.</span><span class="sxs-lookup"><span data-stu-id="48d60-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="48d60-212">d.</span><span class="sxs-lookup"><span data-stu-id="48d60-212">d.</span></span> <span data-ttu-id="48d60-213">Dans la zone de texte **Autorité SAML (fournisseur d’identité)**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48d60-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="48d60-215">e.</span><span class="sxs-lookup"><span data-stu-id="48d60-215">e.</span></span> <span data-ttu-id="48d60-216">Si vous souhaitez configurer l’application en **mode lancé par le fournisseur d’identité**, sélectionnez **Identity Provider (IdP) initiated log in** (Connexion lancée par le fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="48d60-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="48d60-217">En **mode lancé par le fournisseur de service**, sélectionnez **Service Provider (SP) initiated log in** (Connexion lancée par le fournisseur de service).</span><span class="sxs-lookup"><span data-stu-id="48d60-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="48d60-219">f.</span><span class="sxs-lookup"><span data-stu-id="48d60-219">f.</span></span> <span data-ttu-id="48d60-220">Copiez l’URL de consommateur SAML pour votre instance et collez-la dans la zone de texte **URL de réponse** de la section **Domaine et URL Hightail** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48d60-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="48d60-221">g.</span><span class="sxs-lookup"><span data-stu-id="48d60-221">g.</span></span> <span data-ttu-id="48d60-222">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="48d60-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="48d60-223">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="48d60-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48d60-224">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="48d60-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48d60-225">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48d60-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48d60-226">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="48d60-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="48d60-227">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48d60-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="48d60-229">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48d60-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48d60-230">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48d60-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48d60-232">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="48d60-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48d60-234">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="48d60-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48d60-236">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48d60-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48d60-238">a.</span><span class="sxs-lookup"><span data-stu-id="48d60-238">a.</span></span> <span data-ttu-id="48d60-239">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48d60-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48d60-240">b.</span><span class="sxs-lookup"><span data-stu-id="48d60-240">b.</span></span> <span data-ttu-id="48d60-241">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48d60-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48d60-242">c.</span><span class="sxs-lookup"><span data-stu-id="48d60-242">c.</span></span> <span data-ttu-id="48d60-243">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="48d60-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48d60-244">d.</span><span class="sxs-lookup"><span data-stu-id="48d60-244">d.</span></span> <span data-ttu-id="48d60-245">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="48d60-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="48d60-246">Création d’un utilisateur de test Hightail</span><span class="sxs-lookup"><span data-stu-id="48d60-246">Creating a Hightail test user</span></span>

<span data-ttu-id="48d60-247">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Hightail.</span><span class="sxs-lookup"><span data-stu-id="48d60-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="48d60-248">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="48d60-248">There is no action item for you in this section.</span></span> <span data-ttu-id="48d60-249">Hightail prend en charge l’approvisionnement juste-à-temps d’utilisateurs basé sur les revendications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="48d60-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="48d60-250">Si vous avez configuré les revendications personnalisées comme indiqué dans la section **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** ci-dessus, un utilisateur est automatiquement créé dans l’application s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="48d60-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="48d60-251">Si vous avez besoin de créer un utilisateur manuellement, vous devez contacter [l’équipe de support de Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="48d60-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48d60-252">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="48d60-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48d60-253">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Hightail.</span><span class="sxs-lookup"><span data-stu-id="48d60-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="48d60-255">**Pour affecter Britta Simon à Hightail, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48d60-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="48d60-256">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="48d60-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="48d60-258">Dans la liste des applications, sélectionnez **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="48d60-258">In the applications list, select **Hightail**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="48d60-260">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="48d60-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="48d60-262">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="48d60-262">Click **Add** button.</span></span> <span data-ttu-id="48d60-263">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="48d60-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="48d60-265">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="48d60-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48d60-266">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="48d60-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48d60-267">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="48d60-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48d60-268">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="48d60-268">Testing single sign-on</span></span>

<span data-ttu-id="48d60-269">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="48d60-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48d60-270">Quand vous cliquez sur la vignette Hightail dans le volet d’accès, vous devez être connecté automatiquement à votre application Hightail.</span><span class="sxs-lookup"><span data-stu-id="48d60-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="48d60-271">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="48d60-271">Additional resources</span></span>

* [<span data-ttu-id="48d60-272">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48d60-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48d60-273">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="48d60-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

