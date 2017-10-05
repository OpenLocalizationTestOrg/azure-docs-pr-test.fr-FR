---
title: "Didacticiel : intégration d’Azure Active Directory à Promapp | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="5086c-103">Didacticiel : Intégration d’Azure Active Directory à Promapp</span><span class="sxs-lookup"><span data-stu-id="5086c-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="5086c-104">Dans ce didacticiel, vous allez apprendre à intégrer Promapp avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5086c-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5086c-105">L’intégration de Promapp dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5086c-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5086c-106">Dans Azure AD, vous pouvez contrôler qui a accès à Promapp.</span><span class="sxs-lookup"><span data-stu-id="5086c-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="5086c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Promapp (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5086c-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5086c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5086c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5086c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5086c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5086c-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="5086c-110">Prerequisites</span></span>

<span data-ttu-id="5086c-111">Pour configurer l’intégration d’Azure AD avec Promapp, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5086c-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="5086c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5086c-113">Un abonnement Promapp pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5086c-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5086c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5086c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5086c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5086c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5086c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5086c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5086c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5086c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5086c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5086c-118">Scenario description</span></span>
<span data-ttu-id="5086c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5086c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5086c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5086c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5086c-121">Ajout de Promapp à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5086c-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="5086c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="5086c-123">Ajout de Promapp à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5086c-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="5086c-124">Pour configurer l’intégration de Promapp avec Azure AD, vous devez ajouter Promapp à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5086c-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5086c-125">**Pour ajouter Promapp à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5086c-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5086c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5086c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5086c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5086c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5086c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5086c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5086c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5086c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5086c-133">Dans la zone de recherche, entrez **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="5086c-133">In the search box, type **Promapp**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="5086c-135">Dans le volet de résultats, sélectionnez **Promapp**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5086c-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5086c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5086c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Promapp sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5086c-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5086c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Promapp équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5086c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="5086c-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Promapp associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5086c-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="5086c-141">Dans Promapp, affectez la valeur du **nom d’utilisateur** d’Azure AD comme valeur du **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="5086c-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5086c-142">Pour configurer et tester l’authentification unique Azure AD avec Promapp, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5086c-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5086c-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5086c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5086c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5086c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5086c-145">**[Création d’un utilisateur de test Promapp](#creating-a-promapp-test-user)** pour avoir un équivalent de Britta Simon dans Promapp lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5086c-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5086c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5086c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5086c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5086c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5086c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5086c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Promapp.</span><span class="sxs-lookup"><span data-stu-id="5086c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="5086c-150">**Pour configurer l’authentification unique Azure AD avec Promapp, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5086c-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="5086c-151">Dans le portail Azure, sur la page d’intégration de l’application **Promapp**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5086c-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5086c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5086c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="5086c-155">Dans la section **Domaine et URL Promapp**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5086c-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="5086c-157">a.</span><span class="sxs-lookup"><span data-stu-id="5086c-157">a.</span></span> <span data-ttu-id="5086c-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="5086c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="5086c-159">b.</span><span class="sxs-lookup"><span data-stu-id="5086c-159">b.</span></span> <span data-ttu-id="5086c-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="5086c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5086c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5086c-161">These values are not real.</span></span> <span data-ttu-id="5086c-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5086c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5086c-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Promapp](https://www.promapp.com/about-us/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="5086c-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="5086c-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5086c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="5086c-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5086c-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5086c-168">Dans la section **Configuration de Promapp**, cliquez sur **Configurer Promapp** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="5086c-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5086c-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5086c-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="5086c-171">Connectez-vous à votre site d’entreprise Promapp en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5086c-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="5086c-172">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5086c-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Authentification unique Azure AD][12]

9. <span data-ttu-id="5086c-174">Cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="5086c-174">Click **Configure**.</span></span> 
   
    ![Authentification unique Azure AD][13]

10. <span data-ttu-id="5086c-176">Dans la boîte de dialogue **Security** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5086c-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Authentification unique Azure AD][14]
    
    <span data-ttu-id="5086c-178">a.</span><span class="sxs-lookup"><span data-stu-id="5086c-178">a.</span></span> <span data-ttu-id="5086c-179">Collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure dans la zone de texte **SSO-Login URL** (URL de connexion SSO).</span><span class="sxs-lookup"><span data-stu-id="5086c-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="5086c-180">b.</span><span class="sxs-lookup"><span data-stu-id="5086c-180">b.</span></span> <span data-ttu-id="5086c-181">Pour **Mode SSO (authentification unique)**, sélectionnez **Facultatif**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5086c-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="5086c-182">c.</span><span class="sxs-lookup"><span data-stu-id="5086c-182">c.</span></span> <span data-ttu-id="5086c-183">Ouvrez le certificat téléchargé dans le Bloc-notes, copiez le contenu du certificat sans la première ligne (-----BEGIN CERTIFICATE-----) ni la dernière ligne (-----END CERTIFICATE-----), collez-le dans la zone de texte **Certificat x.509 d’authentification unique**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5086c-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="5086c-184">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5086c-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5086c-185">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5086c-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5086c-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5086c-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5086c-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="5086c-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5086c-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5086c-190">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5086c-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5086c-191">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5086c-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5086c-193">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5086c-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5086c-195">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5086c-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5086c-197">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5086c-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5086c-199">a.</span><span class="sxs-lookup"><span data-stu-id="5086c-199">a.</span></span> <span data-ttu-id="5086c-200">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5086c-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5086c-201">b.</span><span class="sxs-lookup"><span data-stu-id="5086c-201">b.</span></span> <span data-ttu-id="5086c-202">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5086c-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5086c-203">c.</span><span class="sxs-lookup"><span data-stu-id="5086c-203">c.</span></span> <span data-ttu-id="5086c-204">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5086c-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5086c-205">d.</span><span class="sxs-lookup"><span data-stu-id="5086c-205">d.</span></span> <span data-ttu-id="5086c-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5086c-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="5086c-207">Création d’un utilisateur de test Promapp</span><span class="sxs-lookup"><span data-stu-id="5086c-207">Creating a Promapp test user</span></span>

<span data-ttu-id="5086c-208">L’application Promapp prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="5086c-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="5086c-209">Cela signifie qu’un compte d’utilisateur est automatiquement créé si nécessaire pendant la tentative d’accès à l’application à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5086c-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5086c-210">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086c-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5086c-211">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Promapp.</span><span class="sxs-lookup"><span data-stu-id="5086c-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5086c-213">**Pour affecter Britta Simon à Promapp, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5086c-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="5086c-214">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5086c-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5086c-216">Dans la liste des applications, sélectionnez **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="5086c-216">In the applications list, select **Promapp**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="5086c-218">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5086c-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5086c-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5086c-220">Click **Add** button.</span></span> <span data-ttu-id="5086c-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5086c-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5086c-223">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5086c-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5086c-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5086c-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5086c-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5086c-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5086c-226">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5086c-226">Testing single sign-on</span></span>

<span data-ttu-id="5086c-227">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5086c-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5086c-228">Lorsque vous cliquez sur la vignette Promapp dans le volet d’accès, vous devez être connecté automatiquement à votre application Promapp.</span><span class="sxs-lookup"><span data-stu-id="5086c-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5086c-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5086c-229">Additional resources</span></span>

* [<span data-ttu-id="5086c-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5086c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5086c-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5086c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

