---
title: "Didacticiel : Intégration d’Azure Active Directory avec Litmos | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="95d62-103">Didacticiel : Intégration d’Azure Active Directory avec Litmos</span><span class="sxs-lookup"><span data-stu-id="95d62-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="95d62-104">Dans ce didacticiel, vous allez apprendre à intégrer Litmos avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95d62-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95d62-105">L’intégration de Litmos dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="95d62-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="95d62-106">Vous pouvez contrôler dans Azure AD qui a accès à Litmos.</span><span class="sxs-lookup"><span data-stu-id="95d62-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="95d62-107">Vous pouvez permettre à vos utilisateurs d’être automatiquement connectés à Litmos (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d62-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="95d62-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95d62-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="95d62-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95d62-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95d62-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="95d62-110">Prerequisites</span></span>

<span data-ttu-id="95d62-111">Pour configurer l’intégration d’Azure AD avec Litmos, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="95d62-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="95d62-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95d62-113">Un abonnement Litmos pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="95d62-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95d62-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="95d62-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95d62-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="95d62-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95d62-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="95d62-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95d62-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95d62-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95d62-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="95d62-118">Scenario description</span></span>
<span data-ttu-id="95d62-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="95d62-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95d62-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="95d62-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95d62-121">Ajout de Litmos à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="95d62-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="95d62-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d62-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="95d62-123">Ajout de Litmos à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="95d62-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="95d62-124">Pour configurer l’intégration de Litmos avec Azure AD, vous devez ajouter Litmos à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="95d62-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="95d62-125">**Pour ajouter Litmos à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95d62-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95d62-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95d62-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="95d62-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="95d62-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="95d62-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="95d62-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="95d62-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="95d62-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="95d62-133">Dans la zone de recherche, tapez **Litmos**, sélectionnez **Litmos** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="95d62-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![Litmos dans la liste des résultats](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="95d62-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d62-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="95d62-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Litmos sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="95d62-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95d62-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Litmos équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d62-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="95d62-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Litmos associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="95d62-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="95d62-139">Dans Litmos, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="95d62-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="95d62-140">Pour configurer et tester l’authentification unique Azure AD avec Litmos, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="95d62-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95d62-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="95d62-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95d62-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95d62-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95d62-143">**[Créer utilisateur de test Litmos](#create-a-litmos-test-user)** pour avoir un équivalent de Britta Simon dans Litmos lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="95d62-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="95d62-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d62-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95d62-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="95d62-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="95d62-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d62-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="95d62-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Litmos.</span><span class="sxs-lookup"><span data-stu-id="95d62-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="95d62-148">**Pour configurer l’authentification unique Azure AD avec Litmos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95d62-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="95d62-149">Dans le portail Azure, sur la page d’intégration de l’application **Litmos**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="95d62-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="95d62-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="95d62-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="95d62-153">Dans la section **Domaine et URL Litmos**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="95d62-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="95d62-155">a.</span><span class="sxs-lookup"><span data-stu-id="95d62-155">a.</span></span> <span data-ttu-id="95d62-156">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="95d62-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="95d62-157">b.</span><span class="sxs-lookup"><span data-stu-id="95d62-157">b.</span></span> <span data-ttu-id="95d62-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="95d62-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95d62-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="95d62-159">These values are not real.</span></span> <span data-ttu-id="95d62-160">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réelles qui sont décrits plus loin dans le didacticiel, ou contactez l’[équipe de support technique Litmos](https://www.litmos.com/contact-us/) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="95d62-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="95d62-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="95d62-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="95d62-163">Dans le cadre de la configuration, vous devez personnaliser les **Attributs du jeton SAML** pour votre application Litmos.</span><span class="sxs-lookup"><span data-stu-id="95d62-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![Section de l’attribut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="95d62-165">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="95d62-165">Attribute Name</span></span>   | <span data-ttu-id="95d62-166">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="95d62-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="95d62-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="95d62-167">FirstName</span></span> |<span data-ttu-id="95d62-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="95d62-168">user.givenname</span></span> |
    | <span data-ttu-id="95d62-169">LastName</span><span class="sxs-lookup"><span data-stu-id="95d62-169">LastName</span></span>  |<span data-ttu-id="95d62-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="95d62-170">user.surname</span></span> |
    | <span data-ttu-id="95d62-171">Email</span><span class="sxs-lookup"><span data-stu-id="95d62-171">Email</span></span> |<span data-ttu-id="95d62-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="95d62-172">user.mail</span></span> |

    <span data-ttu-id="95d62-173">a.</span><span class="sxs-lookup"><span data-stu-id="95d62-173">a.</span></span> <span data-ttu-id="95d62-174">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="95d62-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Ajouter un attribut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Boîte de dialogue Ajouter un attribut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="95d62-177">b.</span><span class="sxs-lookup"><span data-stu-id="95d62-177">b.</span></span> <span data-ttu-id="95d62-178">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="95d62-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="95d62-179">c.</span><span class="sxs-lookup"><span data-stu-id="95d62-179">c.</span></span> <span data-ttu-id="95d62-180">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="95d62-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="95d62-181">d.</span><span class="sxs-lookup"><span data-stu-id="95d62-181">d.</span></span> <span data-ttu-id="95d62-182">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95d62-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="95d62-183">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="95d62-183">Click **Save** button.</span></span>

    ![Bouton Enregistrer de Configurer l’authentification unique](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="95d62-185">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise Litmos en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="95d62-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="95d62-186">Dans la barre de navigation située à gauche, cliquez sur **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="95d62-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Section Comptes côté application][22] 

9. <span data-ttu-id="95d62-188">Cliquez sur l’onglet **Integrations** .</span><span class="sxs-lookup"><span data-stu-id="95d62-188">Click the **Integrations** tab.</span></span>
   
    ![Onglet Intégration][23] 

10. <span data-ttu-id="95d62-190">Sur l’onglet **Integrations**, accédez à **3rd Party Integrations**, puis cliquez sur l’onglet **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="95d62-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Section SAML 2.0][24] 

11. <span data-ttu-id="95d62-192">Copiez la valeur sous **The SAML endpoint for litmos is** (Le point de terminaison SAML pour litmos est), puis collez-la dans la zone de texte **URL de réponse** de la section **Domaine et URL Litmos** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95d62-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Point de terminaison SAML][26] 

12. <span data-ttu-id="95d62-194">Dans votre application **Litmos** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="95d62-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Application Litmos][25] 
     
     <span data-ttu-id="95d62-196">a.</span><span class="sxs-lookup"><span data-stu-id="95d62-196">a.</span></span> <span data-ttu-id="95d62-197">Cliquez sur **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="95d62-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="95d62-198">b.</span><span class="sxs-lookup"><span data-stu-id="95d62-198">b.</span></span> <span data-ttu-id="95d62-199">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **SAML X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="95d62-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="95d62-200">c.</span><span class="sxs-lookup"><span data-stu-id="95d62-200">c.</span></span> <span data-ttu-id="95d62-201">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="95d62-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="95d62-202">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="95d62-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="95d62-203">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="95d62-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="95d62-204">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95d62-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="95d62-205">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d62-205">Create an Azure AD test user</span></span>

<span data-ttu-id="95d62-206">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95d62-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="95d62-208">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95d62-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95d62-209">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95d62-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="95d62-211">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="95d62-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="95d62-213">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="95d62-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="95d62-215">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="95d62-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="95d62-217">a.</span><span class="sxs-lookup"><span data-stu-id="95d62-217">a.</span></span> <span data-ttu-id="95d62-218">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95d62-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95d62-219">b.</span><span class="sxs-lookup"><span data-stu-id="95d62-219">b.</span></span> <span data-ttu-id="95d62-220">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95d62-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="95d62-221">c.</span><span class="sxs-lookup"><span data-stu-id="95d62-221">c.</span></span> <span data-ttu-id="95d62-222">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="95d62-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="95d62-223">d.</span><span class="sxs-lookup"><span data-stu-id="95d62-223">d.</span></span> <span data-ttu-id="95d62-224">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="95d62-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="95d62-225">Créer un utilisateur de test Litmos</span><span class="sxs-lookup"><span data-stu-id="95d62-225">Create a Litmos test user</span></span>

<span data-ttu-id="95d62-226">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Litmos.</span><span class="sxs-lookup"><span data-stu-id="95d62-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="95d62-227">L’application Litmos prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="95d62-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="95d62-228">Cela signifie qu’un compte d’utilisateur est automatiquement créé si nécessaire pendant la tentative d’accès à l’application à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="95d62-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="95d62-229">**Pour créer un utilisateur appelé Britta Simon dans Litmos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95d62-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="95d62-230">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise Litmos en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="95d62-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="95d62-231">Dans la barre de navigation située à gauche, cliquez sur **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="95d62-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Section Comptes côté application][22] 

3. <span data-ttu-id="95d62-233">Cliquez sur l’onglet **Integrations** .</span><span class="sxs-lookup"><span data-stu-id="95d62-233">Click the **Integrations** tab.</span></span>
   
    ![Onglet Intégrations][23] 

4. <span data-ttu-id="95d62-235">Sur l’onglet **Integrations**, accédez à **3rd Party Integrations**, puis cliquez sur l’onglet **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="95d62-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="95d62-237">Sélectionner **Générer automatiquement les utilisateurs**</span><span class="sxs-lookup"><span data-stu-id="95d62-237">Select **Autogenerate Users**</span></span>
   
    ![Générer automatiquement les utilisateurs][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="95d62-239">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d62-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="95d62-240">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Litmos.</span><span class="sxs-lookup"><span data-stu-id="95d62-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="95d62-242">**Pour affecter Britta Simon à Litmos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95d62-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="95d62-243">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="95d62-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="95d62-245">Dans la liste des applications, sélectionnez **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="95d62-245">In the applications list, select **Litmos**.</span></span>

    ![Lien Litmos dans la liste des applications](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="95d62-247">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="95d62-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="95d62-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95d62-249">Click **Add** button.</span></span> <span data-ttu-id="95d62-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="95d62-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="95d62-252">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="95d62-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="95d62-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="95d62-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95d62-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="95d62-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="95d62-255">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="95d62-255">Test single sign-on</span></span>

<span data-ttu-id="95d62-256">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="95d62-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="95d62-257">Lorsque vous cliquez sur la vignette Litmos dans le volet d’accès, vous devez être connecté automatiquement à votre application Litmos.</span><span class="sxs-lookup"><span data-stu-id="95d62-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="95d62-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="95d62-258">Additional resources</span></span>

* [<span data-ttu-id="95d62-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95d62-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95d62-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="95d62-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

