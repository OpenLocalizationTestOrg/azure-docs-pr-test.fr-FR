---
title: "Didacticiel : intégration d’Azure Active Directory à Trakopolis | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3887cf8c085c30eb01ac769944da2fcfe3df81f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="335a9-103">Didacticiel : Intégration d’Azure Active Directory à Trakopolis</span><span class="sxs-lookup"><span data-stu-id="335a9-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="335a9-104">Dans ce didacticiel, vous allez découvrir comment intégrer Trakopolis à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="335a9-104">In this tutorial, you learn how to integrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="335a9-105">L’intégration de Trakopolis dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="335a9-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="335a9-106">Dans Azure AD, vous pouvez contrôler qui a accès à Trakopolis</span><span class="sxs-lookup"><span data-stu-id="335a9-106">You can control in Azure AD who has access to Trakopolis</span></span>
- <span data-ttu-id="335a9-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Trakopolis (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="335a9-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="335a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="335a9-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="335a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="335a9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="335a9-110">Prerequisites</span></span>

<span data-ttu-id="335a9-111">Pour configurer l’intégration d’Azure AD à Trakopolis, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="335a9-111">To configure Azure AD integration with Trakopolis, you need the following items:</span></span>

- <span data-ttu-id="335a9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="335a9-113">Un abonnement Trakopolis pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="335a9-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="335a9-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="335a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="335a9-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="335a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="335a9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="335a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="335a9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="335a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="335a9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="335a9-118">Scenario description</span></span>
<span data-ttu-id="335a9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="335a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="335a9-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="335a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="335a9-121">Ajout de Trakopolis à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="335a9-121">Adding Trakopolis from the gallery</span></span>
2. <span data-ttu-id="335a9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-the-gallery"></a><span data-ttu-id="335a9-123">Ajout de Trakopolis à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="335a9-123">Adding Trakopolis from the gallery</span></span>
<span data-ttu-id="335a9-124">Pour configurer l’intégration de Trakopolis à Azure AD, vous devez ajouter Trakopolis à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="335a9-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="335a9-125">**Pour ajouter Trakopolis à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="335a9-125">**To add Trakopolis from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="335a9-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="335a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="335a9-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="335a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="335a9-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="335a9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="335a9-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="335a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="335a9-133">Dans la zone de recherche, tapez **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="335a9-133">In the search box, type **Trakopolis**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="335a9-135">Dans le panneau de résultats, sélectionnez **Trakopolis**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="335a9-135">In the results panel, select **Trakopolis**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="335a9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="335a9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Trakopolis avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="335a9-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="335a9-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Trakopolis équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="335a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis is to a user in Azure AD.</span></span> <span data-ttu-id="335a9-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Trakopolis associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="335a9-140">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span></span>

<span data-ttu-id="335a9-141">Dans Trakopolis, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="335a9-141">In Trakopolis, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="335a9-142">Pour configurer et tester l’authentification unique Azure AD avec Trakopolis, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="335a9-142">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="335a9-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="335a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="335a9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="335a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="335a9-145">**[Création d’un utilisateur de test Trakopolis](#creating-a-trakopolis-test-user)** pour avoir un équivalent de Britta Simon dans Trakopolis lié à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="335a9-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="335a9-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="335a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="335a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="335a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="335a9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="335a9-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="335a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="335a9-150">**Pour configurer l’authentification unique Azure AD avec Trakopolis, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="335a9-150">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="335a9-151">Dans le portail Azure, dans la page d’intégration de l’application **Trakopolis**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="335a9-151">In the Azure portal, on the **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="335a9-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="335a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="335a9-155">Dans la section **Domaine et URL Trakopolis**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="335a9-155">On the **Trakopolis Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="335a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="335a9-157">a.</span></span> <span data-ttu-id="335a9-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="335a9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="335a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="335a9-159">b.</span></span> <span data-ttu-id="335a9-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="335a9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="335a9-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="335a9-161">These values are not real.</span></span> <span data-ttu-id="335a9-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="335a9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="335a9-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="335a9-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) to get these values.</span></span> 

4. <span data-ttu-id="335a9-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="335a9-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="335a9-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="335a9-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="335a9-168">Dans la section **Configuration de Trakopolis**, cliquez sur **Configurer Trakopolis** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="335a9-168">On the **Trakopolis Configuration** section, click **Configure Trakopolis** to open **Configure sign-on** window.</span></span> <span data-ttu-id="335a9-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="335a9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="335a9-171">Pour configurer l’authentification unique côté **Trakopolis**, vous devez envoyer le **XML de métadonnées, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** téléchargés à l’[équipe de support technique de Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="335a9-171">To configure single sign-on on **Trakopolis** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="335a9-172">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="335a9-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="335a9-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="335a9-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="335a9-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="335a9-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="335a9-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="335a9-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="335a9-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="335a9-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="335a9-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="335a9-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="335a9-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="335a9-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="335a9-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="335a9-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="335a9-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="335a9-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="335a9-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="335a9-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="335a9-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="335a9-188">a.</span><span class="sxs-lookup"><span data-stu-id="335a9-188">a.</span></span> <span data-ttu-id="335a9-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="335a9-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="335a9-190">b.</span><span class="sxs-lookup"><span data-stu-id="335a9-190">b.</span></span> <span data-ttu-id="335a9-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="335a9-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="335a9-192">c.</span><span class="sxs-lookup"><span data-stu-id="335a9-192">c.</span></span> <span data-ttu-id="335a9-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="335a9-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="335a9-194">d.</span><span class="sxs-lookup"><span data-stu-id="335a9-194">d.</span></span> <span data-ttu-id="335a9-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="335a9-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="335a9-196">Création d’un utilisateur de test Trakopolis</span><span class="sxs-lookup"><span data-stu-id="335a9-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="335a9-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="335a9-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="335a9-198">Collaborez avec l’[équipe de support technique de Trakopolis](mailto:support@cantelematics.com) pour ajouter des utilisateurs dans la plateforme Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="335a9-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add the users in the Trakopolis platform.</span></span> <span data-ttu-id="335a9-199">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="335a9-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="335a9-200">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="335a9-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="335a9-201">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="335a9-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakopolis.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="335a9-203">**Pour affecter Britta Simon à Trakopolis, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="335a9-203">**To assign Britta Simon to Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="335a9-204">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="335a9-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="335a9-206">Dans la liste des applications, sélectionnez **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="335a9-206">In the applications list, select **Trakopolis**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="335a9-208">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="335a9-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="335a9-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="335a9-210">Click **Add** button.</span></span> <span data-ttu-id="335a9-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="335a9-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="335a9-213">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="335a9-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="335a9-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="335a9-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="335a9-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="335a9-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="335a9-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="335a9-216">Testing single sign-on</span></span>

<span data-ttu-id="335a9-217">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="335a9-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="335a9-218">Lorsque vous cliquez sur la mosaïque Trakopolis dans le volet d’accès, vous devez être connecté automatiquement à votre application Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="335a9-218">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="335a9-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="335a9-219">Additional resources</span></span>

* [<span data-ttu-id="335a9-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="335a9-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="335a9-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="335a9-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

