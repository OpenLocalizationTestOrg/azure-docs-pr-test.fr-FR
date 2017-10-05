---
title: "Didacticiel : Intégration d’Azure Active Directory dans Lifesize Cloud | Documentation Microsoft"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Lifesize Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="1d5d8-103">Didacticiel : Intégration d’Azure Active Directory à Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="1d5d8-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="1d5d8-104">Dans ce didacticiel, vous allez apprendre à intégrer Lifesize Cloud à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d5d8-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d5d8-105">L’intégration de Lifesize Cloud dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d5d8-106">Dans Azure AD, vous pouvez contrôler qui a accès à Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="1d5d8-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="1d5d8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Lifesize Cloud (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d5d8-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1d5d8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1d5d8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d5d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d5d8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1d5d8-110">Prerequisites</span></span>

<span data-ttu-id="1d5d8-111">Pour configurer l’intégration d’Azure AD à Lifesize Cloud, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="1d5d8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d5d8-113">Un abonnement Lifesize Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1d5d8-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d5d8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d5d8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d5d8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d5d8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d5d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d5d8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1d5d8-118">Scenario description</span></span>
<span data-ttu-id="1d5d8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d5d8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d5d8-121">Ajout de Lifesize Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1d5d8-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="1d5d8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="1d5d8-123">Ajout de Lifesize Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1d5d8-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="1d5d8-124">Pour configurer l’intégration de Lifesize Cloud à Azure AD, vous devez ajouter Lifesize Cloud de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d5d8-125">**Pour ajouter Lifesize Cloud à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d5d8-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d5d8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d5d8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1d5d8-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1d5d8-133">Dans la zone de recherche, entrez **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="1d5d8-135">Dans le panneau de résultats, sélectionnez **Lifesize Cloud**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d5d8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d5d8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lifesize Cloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1d5d8-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d5d8-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Lifesize Cloud équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="1d5d8-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Lifesize Cloud associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="1d5d8-141">Dans Lifesize Cloud, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1d5d8-142">Pour configurer et tester l’authentification unique avec Azure AD avec Lifesize Cloud, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d5d8-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d5d8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d5d8-145">**[Création d’un utilisateur de test Lifesize Cloud](#creating-a-lifesize-cloud-test-user)** pour avoir un équivalent de Britta Simon dans Lifesize Cloud qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d5d8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d5d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d5d8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d5d8-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="1d5d8-150">**Pour configurer l’authentification unique Azure AD avec Lifesize Cloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1d5d8-151">Dans le portail Azure, dans la page d’intégration de l’application **Lifesize Cloud**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1d5d8-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="1d5d8-155">Dans la section **Domaine et URL Lifesize Cloud**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="1d5d8-157">a.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-157">a.</span></span> <span data-ttu-id="1d5d8-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="1d5d8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="1d5d8-159">b.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-159">b.</span></span> <span data-ttu-id="1d5d8-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1d5d8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="1d5d8-161">Cochez l’option **Afficher les paramètres d’URL avancés**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="1d5d8-163">Dans la zone de texte **État de relais**, entrez une valeur en respectant le format suivant : `https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="1d5d8-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="1d5d8-164">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-164">Please note that these are not the real values.</span></span> <span data-ttu-id="1d5d8-165">Vous devez mettre à jour ces valeurs avec l’URL de connexion, l’état de relais et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="1d5d8-166">Pour obtenir les valeurs d’URL de connexion et d’identificateur, contactez [l’équipe de support aux clients Lifesize Cloud](https://www.lifesize.com/support). Vous pouvez également obtenir la valeur de l’état de relais à partir de la configuration SSO, expliquée plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="1d5d8-167">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="1d5d8-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1d5d8-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d5d8-171">Pour ouvrir la fenêtre **Configurer l’authentification**, dans la section **Configuration Lifesize Cloud**, cliquez sur **Configurer Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1d5d8-172">Copiez **l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="1d5d8-174">Pour configurer SSO pour votre application, connectez-vous à l’application Lifesize Cloud avec les privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="1d5d8-175">Dans le coin supérieur droit, cliquez sur votre nom, puis cliquez sur **Paramètres avancés**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="1d5d8-177">Dans les Paramètres avancés, cliquez maintenant sur le lien **Configuration de l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="1d5d8-178">La page Configuration SSO de l’instance s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="1d5d8-180">Maintenant, configurez les valeurs suivantes dans l’interface utilisateur de configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="1d5d8-182">a.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-182">a.</span></span> <span data-ttu-id="1d5d8-183">Dans la zone de texte **Émetteur du fournisseur d'identité**, collez la valeur de l’**ID d’entité SAML** copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1d5d8-184">b.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-184">b.</span></span>  <span data-ttu-id="1d5d8-185">Dans la zone de texte **URL de connexion**, collez la valeur de l’**URL du service d’authentification unique SAML** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1d5d8-186">c.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-186">c.</span></span> <span data-ttu-id="1d5d8-187">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure. Copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat X.509**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="1d5d8-188">d.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-188">d.</span></span> <span data-ttu-id="1d5d8-189">Dans le mappage d’attribut SAML pour la zone de texte Prénom, saisissez la valeur **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="1d5d8-190">e.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-190">e.</span></span> <span data-ttu-id="1d5d8-191">Dans le mappage d’attribut SAML pour la zone de texte **Nom**, saisissez la valeur **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="1d5d8-192">f.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-192">f.</span></span> <span data-ttu-id="1d5d8-193">Dans le mappage d’attribut SAML pour la zone de texte **E-mail**, saisissez la valeur **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="1d5d8-194">Pour vérifier la configuration, vous pouvez cliquer sur le bouton **Test**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1d5d8-195">Pour que les tests se déroulent correctement, vous devez exécuter l’assistant de configuration dans Azure AD et également fournir l’accès aux utilisateurs ou groupes autorisés à effectuer le test.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="1d5d8-196">Activez l’authentification unique en appuyant sur le bouton **Activer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="1d5d8-197">Maintenant, cliquez sur le bouton **Mettre à jour** afin que tous les paramètres soient enregistrés.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="1d5d8-198">Cela génère la valeur RelayState.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-198">This will generate the RelayState value.</span></span> <span data-ttu-id="1d5d8-199">Copiez la valeur RelayState générée dans la zone de texte, puis collez-la dans la zone de texte **État de relais**, sous la section **Domaine et URL Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="1d5d8-200">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1d5d8-201">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1d5d8-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d5d8-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d5d8-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="1d5d8-204">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1d5d8-206">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d5d8-207">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d5d8-209">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d5d8-211">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d5d8-213">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d5d8-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d5d8-215">a.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-215">a.</span></span> <span data-ttu-id="1d5d8-216">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d5d8-217">b.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-217">b.</span></span> <span data-ttu-id="1d5d8-218">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d5d8-219">c.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-219">c.</span></span> <span data-ttu-id="1d5d8-220">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1d5d8-221">d.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-221">d.</span></span> <span data-ttu-id="1d5d8-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="1d5d8-223">Créer un utilisateur de test Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="1d5d8-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="1d5d8-224">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="1d5d8-225">Lifesize Cloud ne prend pas en charge l’approvisionnement automatique des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="1d5d8-226">Après une authentification réussie à Azure AD, l’utilisateur sera automatiquement approvisionné dans l’application.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d5d8-227">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5d8-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1d5d8-228">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1d5d8-230">**Pour affecter Britta Simon à Lifesize Cloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1d5d8-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1d5d8-231">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1d5d8-233">Dans la liste des applications, sélectionnez **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="1d5d8-235">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1d5d8-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-237">Click **Add** button.</span></span> <span data-ttu-id="1d5d8-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1d5d8-240">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d5d8-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d5d8-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d5d8-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1d5d8-243">Testing single sign-on</span></span>

<span data-ttu-id="1d5d8-244">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1d5d8-245">En cliquant sur la vignette Lifesize Cloud dans le Panneau d’accès, vous allez en principe être connecté automatiquement à votre application Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1d5d8-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="1d5d8-246">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1d5d8-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d5d8-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1d5d8-247">Additional resources</span></span>

* [<span data-ttu-id="1d5d8-248">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d5d8-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d5d8-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1d5d8-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

