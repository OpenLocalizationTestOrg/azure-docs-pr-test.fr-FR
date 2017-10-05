---
title: "Didacticiel : Intégration d’Azure Active Directory à Clever | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="c9503-103">Didacticiel : Intégration d’Azure Active Directory à Clever</span><span class="sxs-lookup"><span data-stu-id="c9503-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="c9503-104">Dans ce didacticiel, vous allez apprendre à intégrer Clever dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9503-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9503-105">L’intégration de Clever dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c9503-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c9503-106">Dans Azure AD, vous pouvez contrôler qui a accès à Clever.</span><span class="sxs-lookup"><span data-stu-id="c9503-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="c9503-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Clever (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9503-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c9503-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c9503-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c9503-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9503-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9503-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c9503-110">Prerequisites</span></span>

<span data-ttu-id="c9503-111">Pour configurer l’intégration d’Azure AD avec Clever, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c9503-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="c9503-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9503-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9503-113">Un abonnement Clever pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c9503-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9503-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c9503-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9503-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c9503-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9503-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c9503-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9503-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9503-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9503-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c9503-118">Scenario description</span></span>
<span data-ttu-id="c9503-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c9503-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9503-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9503-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9503-121">Ajout de Clever depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="c9503-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="c9503-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9503-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="c9503-123">Ajout de Clever depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="c9503-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="c9503-124">Pour configurer l’intégration de Clever avec Azure AD, vous devez ajouter Clever, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c9503-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9503-125">**Pour ajouter Clever à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9503-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9503-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9503-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="c9503-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c9503-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9503-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c9503-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="c9503-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c9503-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="c9503-133">Dans la zone de recherche, tapez **Clever**, sélectionnez **Clever** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c9503-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Clever dans la liste des résultats](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c9503-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9503-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c9503-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Clever avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c9503-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9503-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Clever correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9503-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="c9503-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Clever associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c9503-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="c9503-139">Dans Clever, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c9503-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c9503-140">Pour configurer et tester l’authentification unique Azure AD avec Clever, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9503-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9503-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c9503-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9503-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9503-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9503-143">**[Créer utilisateur de test Clever](#create-a-clever-test-user)** pour avoir un équivalent de Britta Simon dans Clever lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c9503-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9503-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9503-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9503-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c9503-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c9503-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9503-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c9503-147">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Clever.</span><span class="sxs-lookup"><span data-stu-id="c9503-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="c9503-148">**Pour configurer l’authentification unique Azure AD avec Clever, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9503-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="c9503-149">Dans le Portail Azure, sur la page d’intégration de l’application **Clever**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c9503-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c9503-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c9503-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="c9503-153">Dans la section **Domaine et URL Clever**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9503-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="c9503-155">a.</span><span class="sxs-lookup"><span data-stu-id="c9503-155">a.</span></span> <span data-ttu-id="c9503-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c9503-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="c9503-157">b.</span><span class="sxs-lookup"><span data-stu-id="c9503-157">b.</span></span> <span data-ttu-id="c9503-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c9503-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9503-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c9503-159">These values are not real.</span></span> <span data-ttu-id="c9503-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="c9503-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c9503-161">Pour obtenir ces valeurs, contactez [l’équipe de support technique de Clever](https://clever.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="c9503-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="c9503-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c9503-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="c9503-164">L’application Clever attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration **Attributs du jeton SAML**.</span><span class="sxs-lookup"><span data-stu-id="c9503-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="c9503-165">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="c9503-165">The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="c9503-167">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9503-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="c9503-168">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="c9503-168">Attribute Name</span></span>  | <span data-ttu-id="c9503-169">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="c9503-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="c9503-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="c9503-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="c9503-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c9503-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="c9503-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="c9503-172">Firstname</span></span>  | <span data-ttu-id="c9503-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c9503-173">user.givenname</span></span> |
    | <span data-ttu-id="c9503-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="c9503-174">Lastname</span></span>  | <span data-ttu-id="c9503-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="c9503-175">user.surname</span></span> |    

    <span data-ttu-id="c9503-176">a.</span><span class="sxs-lookup"><span data-stu-id="c9503-176">a.</span></span> <span data-ttu-id="c9503-177">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c9503-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="c9503-180">b.</span><span class="sxs-lookup"><span data-stu-id="c9503-180">b.</span></span> <span data-ttu-id="c9503-181">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c9503-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c9503-182">c.</span><span class="sxs-lookup"><span data-stu-id="c9503-182">c.</span></span> <span data-ttu-id="c9503-183">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c9503-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="c9503-184">d.</span><span class="sxs-lookup"><span data-stu-id="c9503-184">d.</span></span> <span data-ttu-id="c9503-185">Laissez la zone de texte **Espace de noms** vide.</span><span class="sxs-lookup"><span data-stu-id="c9503-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="c9503-186">d.</span><span class="sxs-lookup"><span data-stu-id="c9503-186">d.</span></span> <span data-ttu-id="c9503-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9503-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="c9503-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c9503-188">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c9503-190">Pour générer l’URL des **métadonnées**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9503-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="c9503-191">a.</span><span class="sxs-lookup"><span data-stu-id="c9503-191">a.</span></span> <span data-ttu-id="c9503-192">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="c9503-192">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="c9503-194">b.</span><span class="sxs-lookup"><span data-stu-id="c9503-194">b.</span></span> <span data-ttu-id="c9503-195">Cliquez sur **Points de terminaison** pour ouvrir la boîte de dialogue **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="c9503-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="c9503-197">c.</span><span class="sxs-lookup"><span data-stu-id="c9503-197">c.</span></span> <span data-ttu-id="c9503-198">Cliquez sur le bouton Copier pour copier l’URL du document de métadonnées de fédération (**FEDERATION METADATA DOCUMENT**), puis collez-la dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="c9503-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="c9503-200">d.</span><span class="sxs-lookup"><span data-stu-id="c9503-200">d.</span></span> <span data-ttu-id="c9503-201">Accédez maintenant à la page de propriétés de **Clever**, puis copiez l’**ID d’application** à l’aide du bouton **Copier** et collez-le dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="c9503-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="c9503-203">e.</span><span class="sxs-lookup"><span data-stu-id="c9503-203">e.</span></span> <span data-ttu-id="c9503-204">Générez l’**URL des métadonnées** en utilisant le format suivant : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="c9503-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="c9503-205">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Clever en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c9503-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="c9503-206">Dans la barre d’outils, cliquez sur **Instant Login**.</span><span class="sxs-lookup"><span data-stu-id="c9503-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="c9503-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="c9503-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="c9503-208">Dans la page **Instant Login** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9503-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="c9503-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="c9503-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="c9503-210">a.</span><span class="sxs-lookup"><span data-stu-id="c9503-210">a.</span></span> <span data-ttu-id="c9503-211">Renseignez le champ **Login URL**.</span><span class="sxs-lookup"><span data-stu-id="c9503-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="c9503-212">**Login URL** est une valeur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c9503-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="c9503-213">Pour obtenir cette valeur, contactez [l’équipe de support technique de Clever](https://clever.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="c9503-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="c9503-214">b.</span><span class="sxs-lookup"><span data-stu-id="c9503-214">b.</span></span> <span data-ttu-id="c9503-215">Sous **Identity System**, sélectionnez **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="c9503-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="c9503-216">c.</span><span class="sxs-lookup"><span data-stu-id="c9503-216">c.</span></span> <span data-ttu-id="c9503-217">Saisissez **l’URL des métadonnées** dans la zone de texte **URL des métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="c9503-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="c9503-218">d.</span><span class="sxs-lookup"><span data-stu-id="c9503-218">d.</span></span> <span data-ttu-id="c9503-219">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="c9503-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c9503-220">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c9503-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c9503-221">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c9503-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c9503-222">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9503-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c9503-223">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9503-223">Create an Azure AD test user</span></span>

<span data-ttu-id="c9503-224">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c9503-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c9503-226">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9503-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9503-227">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9503-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c9503-229">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c9503-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c9503-231">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c9503-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c9503-233">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9503-233">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c9503-235">a.</span><span class="sxs-lookup"><span data-stu-id="c9503-235">a.</span></span> <span data-ttu-id="c9503-236">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9503-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9503-237">b.</span><span class="sxs-lookup"><span data-stu-id="c9503-237">b.</span></span> <span data-ttu-id="c9503-238">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9503-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c9503-239">c.</span><span class="sxs-lookup"><span data-stu-id="c9503-239">c.</span></span> <span data-ttu-id="c9503-240">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c9503-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c9503-241">d.</span><span class="sxs-lookup"><span data-stu-id="c9503-241">d.</span></span> <span data-ttu-id="c9503-242">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c9503-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="c9503-243">Créer un utilisateur de test Clever</span><span class="sxs-lookup"><span data-stu-id="c9503-243">Create a Clever test user</span></span>

<span data-ttu-id="c9503-244">Pour se connecter à Clever, les utilisateurs d’Azure AD doivent être approvisionnés dans Clever.</span><span class="sxs-lookup"><span data-stu-id="c9503-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="c9503-245">Si vous optez pour Clever, travaillez avec [équipe de prise en charge des clients Clever](https://clever.com/about/contact/) pour ajouter des utilisateurs dans la plateforme Clever.</span><span class="sxs-lookup"><span data-stu-id="c9503-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="c9503-246">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c9503-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="c9503-247">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur fourni par Clever pour approvisionner des comptes d’utilisateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9503-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c9503-248">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9503-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="c9503-249">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Clever.</span><span class="sxs-lookup"><span data-stu-id="c9503-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="c9503-251">**Pour affecter Britta Simon à Clever, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9503-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="c9503-252">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c9503-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c9503-254">Dans la liste des applications, sélectionnez **Clever**.</span><span class="sxs-lookup"><span data-stu-id="c9503-254">In the applications list, select **Clever**.</span></span>

    ![Lien Clever dans la liste des applications](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="c9503-256">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c9503-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="c9503-258">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c9503-258">Click **Add** button.</span></span> <span data-ttu-id="c9503-259">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c9503-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="c9503-261">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c9503-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c9503-262">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c9503-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9503-263">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c9503-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c9503-264">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c9503-264">Test single sign-on</span></span>

<span data-ttu-id="c9503-265">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c9503-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9503-266">Lorsque vous cliquez sur la vignette Clever dans le volet d’accès, vous devez être connecté automatiquement à votre application Clever.</span><span class="sxs-lookup"><span data-stu-id="c9503-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="c9503-267">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9503-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c9503-268">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c9503-268">Additional resources</span></span>

* [<span data-ttu-id="c9503-269">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9503-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9503-270">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c9503-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

