---
title: "Didacticiel : Intégration d’Azure Active Directory à etouches | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="5452b-103">Didacticiel : Intégration d’Azure Active Directory à etouches</span><span class="sxs-lookup"><span data-stu-id="5452b-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="5452b-104">Dans ce didacticiel, vous allez apprendre à intégrer etouches à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5452b-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5452b-105">L’intégration d’etouches à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5452b-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5452b-106">Dans Azure AD, vous pouvez contrôler qui a accès à etouches.</span><span class="sxs-lookup"><span data-stu-id="5452b-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="5452b-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à etouches (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5452b-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5452b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5452b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5452b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5452b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5452b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5452b-110">Prerequisites</span></span>

<span data-ttu-id="5452b-111">Pour configurer l’intégration d’Azure AD à etouches, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5452b-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="5452b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5452b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5452b-113">Un abonnement etouches pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5452b-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5452b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5452b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5452b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5452b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5452b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5452b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5452b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5452b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5452b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5452b-118">Scenario description</span></span>
<span data-ttu-id="5452b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5452b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5452b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5452b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5452b-121">Ajout d’etouches à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5452b-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="5452b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5452b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="5452b-123">Ajout d’etouches à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5452b-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="5452b-124">Pour configurer l’intégration d’etouches à Azure AD, vous devez ajouter etouches à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5452b-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5452b-125">**Pour ajouter etouches à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5452b-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5452b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5452b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="5452b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5452b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5452b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5452b-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="5452b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5452b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="5452b-133">Dans la zone de recherche, tapez **etouches**, sélectionnez **etouches** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5452b-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![etouches dans la liste des résultats](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5452b-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5452b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5452b-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec etouches avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5452b-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5452b-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur etouches équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5452b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="5452b-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur etouches associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5452b-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="5452b-139">Dans etouches, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5452b-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5452b-140">Pour configurer et tester l’authentification unique Azure AD avec etouches, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5452b-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5452b-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5452b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5452b-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5452b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5452b-143">**[Créer un utilisateur de test etouches](#create-an-etouches-test-user)** pour avoir un équivalent de Britta Simon dans etouches lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5452b-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5452b-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5452b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5452b-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5452b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5452b-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5452b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5452b-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application etouches.</span><span class="sxs-lookup"><span data-stu-id="5452b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="5452b-148">**Pour configurer l’authentification unique Azure AD avec etouches, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5452b-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="5452b-149">Dans le portail Azure, sur la page d’intégration de l’application **etouches**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5452b-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5452b-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5452b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="5452b-153">Dans la section **Domaine et URL etouches**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5452b-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="5452b-155">a.</span><span class="sxs-lookup"><span data-stu-id="5452b-155">a.</span></span> <span data-ttu-id="5452b-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="5452b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="5452b-157">b.</span><span class="sxs-lookup"><span data-stu-id="5452b-157">b.</span></span> <span data-ttu-id="5452b-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="5452b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5452b-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5452b-159">These values are not real.</span></span> <span data-ttu-id="5452b-160">Vous mettez à jour la valeur avec l’URL de connexion et l’identificateur réels. La procédure est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5452b-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="5452b-161">L’application etouches attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="5452b-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5452b-162">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="5452b-162">Configure the following claims for this application.</span></span> <span data-ttu-id="5452b-163">Vous pouvez gérer les valeurs de ces attributs à partir des « **Attributs utilisateur** » de l’application.</span><span class="sxs-lookup"><span data-stu-id="5452b-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="5452b-164">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="5452b-164">The following screenshot shows an example for this.</span></span> 

    ![Attribut utilisateur](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="5452b-166">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5452b-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="5452b-167">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="5452b-167">Attribute Name</span></span> | <span data-ttu-id="5452b-168">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="5452b-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="5452b-169">Email</span><span class="sxs-lookup"><span data-stu-id="5452b-169">Email</span></span> | <span data-ttu-id="5452b-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="5452b-170">user.mail</span></span> |    
    
    <span data-ttu-id="5452b-171">a.</span><span class="sxs-lookup"><span data-stu-id="5452b-171">a.</span></span> <span data-ttu-id="5452b-172">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="5452b-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Ajouter un attribut](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Boîte de dialogue Ajouter un attribut](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5452b-175">b.</span><span class="sxs-lookup"><span data-stu-id="5452b-175">b.</span></span> <span data-ttu-id="5452b-176">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5452b-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5452b-177">c.</span><span class="sxs-lookup"><span data-stu-id="5452b-177">c.</span></span> <span data-ttu-id="5452b-178">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5452b-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5452b-179">d.</span><span class="sxs-lookup"><span data-stu-id="5452b-179">d.</span></span> <span data-ttu-id="5452b-180">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5452b-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="5452b-181">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5452b-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="5452b-183">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5452b-183">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5452b-185">Pour configurer l’authentification unique pour votre application, procédez comme suit dans l’application etouches :</span><span class="sxs-lookup"><span data-stu-id="5452b-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![Configuration d’etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="5452b-187">a.</span><span class="sxs-lookup"><span data-stu-id="5452b-187">a.</span></span> <span data-ttu-id="5452b-188">Connectez-vous à l’application **etouches** à l’aide des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5452b-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="5452b-189">b.</span><span class="sxs-lookup"><span data-stu-id="5452b-189">b.</span></span> <span data-ttu-id="5452b-190">Accédez à la configuration **SAML**.</span><span class="sxs-lookup"><span data-stu-id="5452b-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="5452b-191">c.</span><span class="sxs-lookup"><span data-stu-id="5452b-191">c.</span></span> <span data-ttu-id="5452b-192">Dans la section **Paramètres généraux**, ouvrez votre certificat téléchargé à partir du portail Azure dans le Bloc-notes, copiez le contenu, puis collez-le dans la zone de texte des métadonnées IDP.</span><span class="sxs-lookup"><span data-stu-id="5452b-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="5452b-193">d.</span><span class="sxs-lookup"><span data-stu-id="5452b-193">d.</span></span> <span data-ttu-id="5452b-194">Cliquez sur le bouton **Enregistrer et rester**.</span><span class="sxs-lookup"><span data-stu-id="5452b-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="5452b-195">e.</span><span class="sxs-lookup"><span data-stu-id="5452b-195">e.</span></span> <span data-ttu-id="5452b-196">Dans la section SAML Metadata (Métadonnées SAML), cliquez sur le bouton **Update Metadata (Mettre à jour les métadonnées)** .</span><span class="sxs-lookup"><span data-stu-id="5452b-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="5452b-197">f.</span><span class="sxs-lookup"><span data-stu-id="5452b-197">f.</span></span> <span data-ttu-id="5452b-198">Cela ouvre la page et effectue l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5452b-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="5452b-199">Une fois l’authentification unique effectuée, vous pouvez configurer le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5452b-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="5452b-200">g.</span><span class="sxs-lookup"><span data-stu-id="5452b-200">g.</span></span> <span data-ttu-id="5452b-201">Dans le champ Nom d’utilisateur, sélectionnez **l’adresse e-mail** comme indiqué sur l’illustration ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5452b-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="5452b-202">h.</span><span class="sxs-lookup"><span data-stu-id="5452b-202">h.</span></span> <span data-ttu-id="5452b-203">Copiez la valeur de l’**ID d’entité SP** et collez-la dans la zone de texte **Identificateur** de la section **Domaine et URL etouches** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="5452b-204">i.</span><span class="sxs-lookup"><span data-stu-id="5452b-204">i.</span></span> <span data-ttu-id="5452b-205">Copiez la valeur de l’**URL d’authentification unique / ACS** et collez-la dans la zone de texte **URL de connexion** de la section **Domaine et URL etouches** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="5452b-206">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5452b-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5452b-207">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5452b-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5452b-208">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5452b-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5452b-209">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5452b-209">Create an Azure AD test user</span></span>
<span data-ttu-id="5452b-210">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="5452b-212">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5452b-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5452b-213">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5452b-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5452b-215">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5452b-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5452b-217">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5452b-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5452b-219">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5452b-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5452b-221">a.</span><span class="sxs-lookup"><span data-stu-id="5452b-221">a.</span></span> <span data-ttu-id="5452b-222">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5452b-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5452b-223">b.</span><span class="sxs-lookup"><span data-stu-id="5452b-223">b.</span></span> <span data-ttu-id="5452b-224">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5452b-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5452b-225">c.</span><span class="sxs-lookup"><span data-stu-id="5452b-225">c.</span></span> <span data-ttu-id="5452b-226">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5452b-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5452b-227">d.</span><span class="sxs-lookup"><span data-stu-id="5452b-227">d.</span></span> <span data-ttu-id="5452b-228">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5452b-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="5452b-229">Créer un utilisateur de test etouches</span><span class="sxs-lookup"><span data-stu-id="5452b-229">Create an etouches test user</span></span>

<span data-ttu-id="5452b-230">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans etouches.</span><span class="sxs-lookup"><span data-stu-id="5452b-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="5452b-231">Collaborez avec l’[équipe du support technique etouches](https://www.etouches.com/event-software/support/customer-support/) pour ajouter des utilisateurs à la plateforme etouches.</span><span class="sxs-lookup"><span data-stu-id="5452b-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5452b-232">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5452b-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="5452b-233">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à etouches.</span><span class="sxs-lookup"><span data-stu-id="5452b-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="5452b-235">**Pour affecter Britta Simon à etouches, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5452b-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="5452b-236">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5452b-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5452b-238">Dans la liste des applications, sélectionnez **etouches**.</span><span class="sxs-lookup"><span data-stu-id="5452b-238">In the applications list, select **etouches**.</span></span>

    ![Lien etouches dans la liste des applications](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="5452b-240">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5452b-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="5452b-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5452b-242">Click **Add** button.</span></span> <span data-ttu-id="5452b-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5452b-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="5452b-245">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5452b-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5452b-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5452b-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5452b-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5452b-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5452b-248">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5452b-248">Test single sign-on</span></span>


<span data-ttu-id="5452b-249">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5452b-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5452b-250">Si vous cliquez sur la vignette etouches dans le volet d’accès, vous devez vous connecter automatiquement à votre application etouches.</span><span class="sxs-lookup"><span data-stu-id="5452b-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5452b-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5452b-251">Additional resources</span></span>

* [<span data-ttu-id="5452b-252">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5452b-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5452b-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5452b-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

