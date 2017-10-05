---
title: "Didacticiel : Intégration d’Azure Active Directory à Adobe Creative Cloud | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Adobe Creative Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="a4732-103">Didacticiel : Intégration d’Azure Active Directory à Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="a4732-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="a4732-104">Dans ce didacticiel, vous allez apprendre à intégrer Adobe Creative Cloud à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4732-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4732-105">L’intégration de Adobe Creative Cloud dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a4732-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a4732-106">Dans Azure AD, vous pouvez contrôler qui a accès à Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="a4732-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="a4732-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Adobe Creative Cloud (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4732-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="a4732-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="a4732-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4732-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4732-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a4732-110">Prerequisites</span></span>

<span data-ttu-id="a4732-111">Pour configurer l’intégration d’Azure AD à Adobe Creative Cloud, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a4732-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="a4732-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a4732-113">Un abonnement Adobe Creative Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a4732-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4732-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a4732-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4732-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a4732-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4732-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a4732-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a4732-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4732-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4732-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a4732-118">Scenario description</span></span>
<span data-ttu-id="a4732-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a4732-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4732-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a4732-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4732-121">Ajout de Adobe Creative Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a4732-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="a4732-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="a4732-123">Ajout de Adobe Creative Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a4732-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="a4732-124">Pour configurer l’intégration de Adobe Creative Cloud à Azure AD, vous devez ajouter Adobe Creative Cloud de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a4732-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a4732-125">**Pour ajouter Adobe Creative Cloud à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a4732-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a4732-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4732-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4732-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a4732-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a4732-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a4732-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a4732-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a4732-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a4732-133">Dans la zone de recherche, tapez **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a4732-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="a4732-135">Dans le volet de résultats, sélectionnez **Adobe Creative Cloud**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a4732-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4732-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4732-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Adobe Creative Cloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a4732-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4732-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Adobe Creative Cloud équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4732-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="a4732-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Adobe Creative Cloud associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a4732-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="a4732-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="a4732-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="a4732-142">Pour configurer et tester l’authentification unique avec Azure AD avec Adobe Creative Cloud, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="a4732-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a4732-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a4732-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a4732-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4732-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4732-145">**[Création d’un utilisateur de test Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)** pour avoir un équivalent de Britta Simon dans Adobe Creative Cloud lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a4732-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a4732-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4732-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4732-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a4732-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4732-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4732-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="a4732-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="a4732-150">**Pour configurer l’authentification unique Azure AD avec Adobe Creative Cloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a4732-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="a4732-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **Adobe Creative Cloud**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a4732-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a4732-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a4732-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="a4732-155">Dans la section **Domaines et URL Adobe Creative Cloud**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en **Mode initié par IDP** :</span><span class="sxs-lookup"><span data-stu-id="a4732-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="a4732-157">a.</span><span class="sxs-lookup"><span data-stu-id="a4732-157">a.</span></span> <span data-ttu-id="a4732-158">Dans la zone de texte **Identificateur**, entrez la valeur `https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="a4732-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="a4732-159">b.</span><span class="sxs-lookup"><span data-stu-id="a4732-159">b.</span></span> <span data-ttu-id="a4732-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="a4732-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a4732-161">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a4732-161">Please note that these are not the real values.</span></span> <span data-ttu-id="a4732-162">Vous devez mettre à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="a4732-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a4732-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="a4732-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="a4732-164">Si vous devez créer un utilisateur manuellement, contactez l’équipe du support technique Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="a4732-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="a4732-165">Dans la section **Domaines et URL Adobe Creative Cloud**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en **Mode initié par SP** :</span><span class="sxs-lookup"><span data-stu-id="a4732-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="a4732-167">a.</span><span class="sxs-lookup"><span data-stu-id="a4732-167">a.</span></span> <span data-ttu-id="a4732-168">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="a4732-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="a4732-169">b.</span><span class="sxs-lookup"><span data-stu-id="a4732-169">b.</span></span> <span data-ttu-id="a4732-170">Dans la zone de texte **URL de connexion**, tapez la valeur suivante : `https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="a4732-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="a4732-171">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a4732-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="a4732-173">Dans la section **Configuration de Adobe Creative Cloud**, cliquez sur **Configurer Adobe Creative Cloud** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a4732-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a4732-174">Copiez **l’ID d’entité SAML** et **l’URL du service SSO SAML** à partir de la section Référence rapide.</span><span class="sxs-lookup"><span data-stu-id="a4732-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="a4732-176">Dans une autre fenêtre de navigateur web, connectez-vous à votre client Adobe Creative Cloud en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a4732-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="a4732-177">Accédez à **Identité** dans le volet de navigation de gauche et cliquez sur votre domaine.</span><span class="sxs-lookup"><span data-stu-id="a4732-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="a4732-178">Suivez ensuite la procédure de la section **Configuration de l’authentification unique requise**.</span><span class="sxs-lookup"><span data-stu-id="a4732-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="a4732-179">![Paramètres](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="a4732-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="a4732-180">Cliquez sur **Parcourir** pour télécharger le certificat obtenu à partir d’Azure AD dans **Certificat IDP**.</span><span class="sxs-lookup"><span data-stu-id="a4732-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="a4732-181">Dans la zone de texte **IDP issuer**, placez la valeur de **l’ID d’entité SAML** que vous avez copiée depuis la section **Configurer l’authentification** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a4732-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="a4732-182">Dans la zone de texte **IDP Login URL**, placez la valeur de **l’URL du service SSO SAML** que vous avez copiée depuis la section **Configurer l’authentification** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a4732-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="a4732-183">Sélectionnez **HTTP - Redirection** en tant que **Liaison IDP**.</span><span class="sxs-lookup"><span data-stu-id="a4732-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="a4732-184">Sélectionnez **Adresse de messagerie** en tant que **Paramètre de connexion utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="a4732-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="a4732-185">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a4732-185">Click **Save** button.</span></span>

15. <span data-ttu-id="a4732-186">Le tableau de bord présente maintenant le fichier XML **« Télécharger les métadonnées »**.</span><span class="sxs-lookup"><span data-stu-id="a4732-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="a4732-187">Il contient les URL EntityDescriptor et AssertionConsumerService d’Adobe.</span><span class="sxs-lookup"><span data-stu-id="a4732-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="a4732-188">Ouvrez le fichier et configurez-les dans l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4732-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="a4732-191">a.</span><span class="sxs-lookup"><span data-stu-id="a4732-191">a.</span></span> <span data-ttu-id="a4732-192">Utilisez la valeur EntityDescriptor que Adobe vous a fournie pour **Identificateur** dans la boîte de dialogue **Configurer les paramètres d’application**.</span><span class="sxs-lookup"><span data-stu-id="a4732-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="a4732-193">b.</span><span class="sxs-lookup"><span data-stu-id="a4732-193">b.</span></span> <span data-ttu-id="a4732-194">Utilisez la valeur AssertionConsumerService que Adobe vous a fournie pour **URL de réponse** dans la boîte de dialogue **Configurer les paramètres d’application**.</span><span class="sxs-lookup"><span data-stu-id="a4732-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4732-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4732-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="a4732-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a4732-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a4732-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a4732-199">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4732-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4732-201">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a4732-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4732-203">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="a4732-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4732-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4732-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4732-207">a.</span><span class="sxs-lookup"><span data-stu-id="a4732-207">a.</span></span> <span data-ttu-id="a4732-208">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4732-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4732-209">b.</span><span class="sxs-lookup"><span data-stu-id="a4732-209">b.</span></span> <span data-ttu-id="a4732-210">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4732-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4732-211">c.</span><span class="sxs-lookup"><span data-stu-id="a4732-211">c.</span></span> <span data-ttu-id="a4732-212">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a4732-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a4732-213">d.</span><span class="sxs-lookup"><span data-stu-id="a4732-213">d.</span></span> <span data-ttu-id="a4732-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a4732-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="a4732-215">Création d’un utilisateur d’Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="a4732-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="a4732-216">Pour permettre aux utilisateurs Azure AD de se connecter à Adobe Creative Cloud, vous devez les approvisionner dans Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="a4732-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="a4732-217">Dans le cas d’Adobe Creative Cloud, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="a4732-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="a4732-218">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a4732-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="a4732-219">Connectez-vous à votre site d’entreprise Adobe Creative Cloud en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a4732-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="a4732-220">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="a4732-220">Click **People**.</span></span>

    <span data-ttu-id="a4732-221">![Personnes](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="a4732-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="a4732-222">Cliquez sur **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="a4732-222">Click **Invite User**.</span></span>

    <span data-ttu-id="a4732-223">![Inviter des utilisateurs](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "inviter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="a4732-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="a4732-224">Dans la boîte de dialogue **Invite People**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4732-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="a4732-225">![Inviter des personnes](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "inviter des personnes")</span><span class="sxs-lookup"><span data-stu-id="a4732-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="a4732-226">a.</span><span class="sxs-lookup"><span data-stu-id="a4732-226">a.</span></span> <span data-ttu-id="a4732-227">Dans la zone de texte **E-mail** , tapez l’adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4732-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="a4732-228">b.</span><span class="sxs-lookup"><span data-stu-id="a4732-228">b.</span></span> <span data-ttu-id="a4732-229">Cliquez sur **Inviter**.</span><span class="sxs-lookup"><span data-stu-id="a4732-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a4732-230">Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="a4732-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a4732-231">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4732-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a4732-232">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="a4732-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a4732-234">**Pour affecter Britta Simon Adobe Creative Cloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a4732-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="a4732-235">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a4732-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a4732-237">Dans la liste des applications, sélectionnez **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a4732-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="a4732-239">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a4732-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a4732-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a4732-241">Click **Add** button.</span></span> <span data-ttu-id="a4732-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a4732-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a4732-244">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a4732-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a4732-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a4732-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4732-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a4732-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4732-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a4732-247">Testing single sign-on</span></span>

<span data-ttu-id="a4732-248">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a4732-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a4732-249">Lorsque vous cliquez sur la vignette Adobe Creative Cloud dans le volet d’accès, vous devez être connecté automatiquement à votre application Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="a4732-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a4732-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a4732-250">Additional resources</span></span>

* [<span data-ttu-id="a4732-251">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4732-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4732-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a4732-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png