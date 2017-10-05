---
title: "Didacticiel : Intégration d’Azure Active Directory avec Mimecast Personal Portal | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Mimecast Personal Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="efb84-103">Didacticiel : Intégration d’Azure Active Directory avec Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="efb84-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="efb84-104">Dans ce didacticiel, vous allez apprendre à intégrer Mimecast Personal Portal avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="efb84-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efb84-105">L’intégration de Mimecast Personal Portal avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="efb84-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="efb84-106">Dans Azure AD, vous pouvez contrôler qui a accès à Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="efb84-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="efb84-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Mimecast Personal Portal (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb84-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efb84-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efb84-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="efb84-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efb84-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efb84-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="efb84-110">Prerequisites</span></span>

<span data-ttu-id="efb84-111">Pour configurer l’intégration d’Azure AD avec Mimecast Personal Portal, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="efb84-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="efb84-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efb84-113">Un abonnement Mimecast Personal Portal pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="efb84-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="efb84-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="efb84-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="efb84-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="efb84-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efb84-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="efb84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="efb84-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efb84-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efb84-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="efb84-118">Scenario description</span></span>
<span data-ttu-id="efb84-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="efb84-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="efb84-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="efb84-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efb84-121">Ajout de Mimecast Personal Portal à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="efb84-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="efb84-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb84-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="efb84-123">Ajout de Mimecast Personal Portal à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="efb84-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="efb84-124">Pour configurer l’intégration de Mimecast Personal Portal à Azure AD, vous devez ajouter Mimecast Personal Portal à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="efb84-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="efb84-125">**Pour ajouter Mimecast Personal Portal à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="efb84-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="efb84-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efb84-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="efb84-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="efb84-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="efb84-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="efb84-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="efb84-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="efb84-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="efb84-133">Dans la zone de recherche, tapez **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="efb84-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="efb84-135">Dans le volet des résultats, sélectionnez **Mimecast Personal Portal**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="efb84-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efb84-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb84-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="efb84-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mimecast Personal Portal sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="efb84-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="efb84-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Mimecast Personal Portal équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb84-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="efb84-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Mimecast Personal Portal associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="efb84-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="efb84-141">Dans Mimecast Personal Portal, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="efb84-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="efb84-142">Pour configurer et tester l’authentification unique Azure AD avec Mimecast Personal Portal, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="efb84-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="efb84-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="efb84-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="efb84-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efb84-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="efb84-145">**[Création d’un utilisateur de test Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)** pour obtenir un équivalent de Britta Simon dans Mimecast Personal Portal lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="efb84-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="efb84-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb84-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efb84-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="efb84-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efb84-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb84-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efb84-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="efb84-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="efb84-150">**Pour configurer l’authentification unique Azure AD avec Mimecast Personal Portal, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="efb84-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="efb84-151">Dans le portail Azure, sur la page d’intégration de l’application **Mimecast Personal Portal**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="efb84-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="efb84-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="efb84-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="efb84-155">Dans la section **Domaine et URL Mimecast Personal Portal**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="efb84-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="efb84-157">a.</span><span class="sxs-lookup"><span data-stu-id="efb84-157">a.</span></span> <span data-ttu-id="efb84-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="efb84-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="efb84-159">b.</span><span class="sxs-lookup"><span data-stu-id="efb84-159">b.</span></span> <span data-ttu-id="efb84-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="efb84-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="efb84-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="efb84-161">These values are not real.</span></span> <span data-ttu-id="efb84-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="efb84-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="efb84-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/).</span><span class="sxs-lookup"><span data-stu-id="efb84-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="efb84-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="efb84-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="efb84-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="efb84-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="efb84-168">Dans la section **Configuration de Mimecast Personal Portal**, cliquez sur **Configurer Mimecast Personal Portal** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="efb84-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="efb84-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="efb84-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="efb84-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mimecast Personal Portal en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="efb84-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="efb84-172">Accédez à **Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="efb84-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="efb84-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="efb84-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="efb84-174">Cliquez sur **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="efb84-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="efb84-175">![Profils d’authentification](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Profils d’authentification")</span><span class="sxs-lookup"><span data-stu-id="efb84-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="efb84-176">Cliquez sur **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="efb84-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="efb84-177">![Nouveau profil d’authentification](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "Nouveau profil d’authentification")</span><span class="sxs-lookup"><span data-stu-id="efb84-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="efb84-178">Dans la section **Authentication Profile** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="efb84-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="efb84-179">![Profil d’authentification](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Profil d’authentification")</span><span class="sxs-lookup"><span data-stu-id="efb84-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="efb84-180">a.</span><span class="sxs-lookup"><span data-stu-id="efb84-180">a.</span></span> <span data-ttu-id="efb84-181">Dans la zone de texte **Description** , indiquez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="efb84-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="efb84-182">b.</span><span class="sxs-lookup"><span data-stu-id="efb84-182">b.</span></span> <span data-ttu-id="efb84-183">Sélectionnez **Enforce SAML Authentication for Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="efb84-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="efb84-184">c.</span><span class="sxs-lookup"><span data-stu-id="efb84-184">c.</span></span> <span data-ttu-id="efb84-185">Pour **Provider**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efb84-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="efb84-186">d.</span><span class="sxs-lookup"><span data-stu-id="efb84-186">d.</span></span> <span data-ttu-id="efb84-187">Dans la zone de texte **Issuer URL (URL de l’émetteur)**, collez la valeur **SAML Entity ID (ID d’entité SAML)** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efb84-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="efb84-188">e.</span><span class="sxs-lookup"><span data-stu-id="efb84-188">e.</span></span> <span data-ttu-id="efb84-189">Dans la zone de texte **Login URL (URL de connexion)**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efb84-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="efb84-190">f.</span><span class="sxs-lookup"><span data-stu-id="efb84-190">f.</span></span> <span data-ttu-id="efb84-191">Dans la zone de texte **Logout URL (URL de déconnexion)**, collez la valeur **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efb84-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="efb84-192">g.</span><span class="sxs-lookup"><span data-stu-id="efb84-192">g.</span></span> <span data-ttu-id="efb84-193">Ouvrez votre certificat codé **en base 64** dans le bloc-notes téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Identity Provider Certificate (Metadata)** (Certificat de fournisseur d’identité (métadonnées)).</span><span class="sxs-lookup"><span data-stu-id="efb84-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="efb84-194">h.</span><span class="sxs-lookup"><span data-stu-id="efb84-194">h.</span></span> <span data-ttu-id="efb84-195">Sélectionnez **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="efb84-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="efb84-196">i.</span><span class="sxs-lookup"><span data-stu-id="efb84-196">i.</span></span> <span data-ttu-id="efb84-197">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="efb84-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="efb84-198">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="efb84-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="efb84-199">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="efb84-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="efb84-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="efb84-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efb84-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb84-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="efb84-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efb84-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="efb84-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="efb84-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="efb84-205">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efb84-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efb84-207">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="efb84-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efb84-209">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="efb84-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efb84-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="efb84-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="efb84-213">a.</span><span class="sxs-lookup"><span data-stu-id="efb84-213">a.</span></span> <span data-ttu-id="efb84-214">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efb84-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efb84-215">b.</span><span class="sxs-lookup"><span data-stu-id="efb84-215">b.</span></span> <span data-ttu-id="efb84-216">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efb84-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="efb84-217">c.</span><span class="sxs-lookup"><span data-stu-id="efb84-217">c.</span></span> <span data-ttu-id="efb84-218">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="efb84-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="efb84-219">d.</span><span class="sxs-lookup"><span data-stu-id="efb84-219">d.</span></span> <span data-ttu-id="efb84-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="efb84-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="efb84-221">Création d’un utilisateur de test Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="efb84-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="efb84-222">Pour permettre aux utilisateurs Azure AD de se connecter à Mimecast Personal Portal, vous devez les approvisionner dans Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="efb84-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="efb84-223">Dans le cas de Mimecast Personal Portal, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="efb84-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="efb84-224">Vous devez enregistrer un domaine avant de pouvoir créer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="efb84-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="efb84-225">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="efb84-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="efb84-226">Connectez-vous à **Mimecast Personal Portal** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="efb84-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="efb84-227">Accédez à **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="efb84-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="efb84-228">![Répertoires](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Répertoires")</span><span class="sxs-lookup"><span data-stu-id="efb84-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="efb84-229">Cliquez sur **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="efb84-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="efb84-230">![Enregistrer un nouveau domaine](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Enregistrer un nouveau domaine")</span><span class="sxs-lookup"><span data-stu-id="efb84-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="efb84-231">Après avoir créé votre domaine, cliquez sur **New Address**.</span><span class="sxs-lookup"><span data-stu-id="efb84-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="efb84-232">![Nouvelle adresse](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Nouvelle adresse")</span><span class="sxs-lookup"><span data-stu-id="efb84-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="efb84-233">Dans la boîte de dialogue Nouvelle Adresse, procédez comme suit pour un compte Azure AD valide que vous souhaitez approvisionner :</span><span class="sxs-lookup"><span data-stu-id="efb84-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="efb84-234">![Enregistrer](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "enregistrer")</span><span class="sxs-lookup"><span data-stu-id="efb84-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="efb84-235">a.</span><span class="sxs-lookup"><span data-stu-id="efb84-235">a.</span></span> <span data-ttu-id="efb84-236">Dans la zone de texte **Adresse e-mail**, entrez l’**adresse e-mail** de l’utilisateur. Ici, il s’agit de **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="efb84-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="efb84-237">b.</span><span class="sxs-lookup"><span data-stu-id="efb84-237">b.</span></span> <span data-ttu-id="efb84-238">Dans la zone de texte **Nom global**, tapez le **nom d’utilisateur** sous la forme **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efb84-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="efb84-239">c.</span><span class="sxs-lookup"><span data-stu-id="efb84-239">c.</span></span> <span data-ttu-id="efb84-240">Dans les zones de texte **Mot de passe** et **Confirmer le mot de passe**, type de le **mot de passe** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efb84-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="efb84-241">b.</span><span class="sxs-lookup"><span data-stu-id="efb84-241">b.</span></span> <span data-ttu-id="efb84-242">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="efb84-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="efb84-243">Vous pouvez utiliser tout autre outil ou API de création de compte d’utilisateur fourni par Mimecast Personal Portal pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb84-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="efb84-244">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb84-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="efb84-245">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="efb84-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="efb84-247">**Pour affecter Britta Simon à Mimecast Personal Portal, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="efb84-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="efb84-248">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="efb84-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="efb84-250">Dans la liste des applications, sélectionnez **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="efb84-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="efb84-252">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="efb84-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="efb84-254">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="efb84-254">Click **Add** button.</span></span> <span data-ttu-id="efb84-255">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="efb84-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="efb84-257">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="efb84-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="efb84-258">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="efb84-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="efb84-259">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="efb84-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="efb84-260">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="efb84-260">Testing single sign-on</span></span>
<span data-ttu-id="efb84-261">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="efb84-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="efb84-262">Lorsque vous cliquez sur la vignette Mimecast Personal Portal dans le panneau d’accès, vous devez être connecté automatiquement à votre application Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="efb84-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="efb84-263">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="efb84-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efb84-264">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="efb84-264">Additional resources</span></span>

* [<span data-ttu-id="efb84-265">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efb84-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efb84-266">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="efb84-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

