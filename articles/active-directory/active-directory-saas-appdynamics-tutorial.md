---
title: "Didacticiel : Intégration d’Azure Active Directory à AppDynamics | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="6a266-103">Didacticiel : Intégration d’Azure Active Directory à AppDynamics</span><span class="sxs-lookup"><span data-stu-id="6a266-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="6a266-104">Dans ce didacticiel, vous allez apprendre à intégrer AppDynamics à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a266-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a266-105">L’intégration d’AppDynamics à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6a266-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a266-106">Dans Azure AD, vous pouvez contrôler qui a accès à AppDynamics</span><span class="sxs-lookup"><span data-stu-id="6a266-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="6a266-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à AppDynamics (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a266-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6a266-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a266-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a266-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a266-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="6a266-110">Prerequisites</span></span>

<span data-ttu-id="6a266-111">Pour configurer l’intégration d’Azure AD à AppDynamics, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6a266-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="6a266-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a266-113">Un abonnement AppDynamics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6a266-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a266-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6a266-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a266-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6a266-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a266-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a266-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a266-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a266-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a266-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6a266-118">Scenario description</span></span>
<span data-ttu-id="6a266-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6a266-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a266-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a266-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a266-121">Ajout d’AppDynamics à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6a266-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="6a266-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="6a266-123">Ajout d’AppDynamics à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6a266-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="6a266-124">Pour configurer l’intégration d’AppDynamics à Azure AD, vous devez ajouter AppDynamics à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6a266-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a266-125">**Pour ajouter AppDynamics à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="6a266-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a266-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a266-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a266-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6a266-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a266-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6a266-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6a266-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6a266-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6a266-133">Dans la zone de recherche, tapez **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="6a266-133">In the search box, type **AppDynamics**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="6a266-135">Dans le panneau de résultats, sélectionnez **AppDynamics**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6a266-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a266-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a266-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec AppDynamics, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6a266-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a266-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur AppDynamics équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a266-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="6a266-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur AppDynamics associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="6a266-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="6a266-141">Dans AppDynamics, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6a266-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a266-142">Pour configurer et tester l’authentification unique Azure AD avec AppDynamics, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a266-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a266-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6a266-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a266-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a266-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a266-145">**[Création d’un utilisateur test AppDynamics](#creating-an-appdynamics-test-user)** pour avoir un équivalent de Britta Simon dans AppDynamics lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6a266-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a266-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a266-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a266-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6a266-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a266-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a266-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="6a266-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="6a266-150">**Pour configurer l’authentification unique Azure AD avec AppDynamics, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="6a266-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="6a266-151">Dans le portail Azure, dans la page d’intégration de l’application **AppDynamics**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6a266-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6a266-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6a266-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="6a266-155">Dans la section **Domaine et URL AppDynamics**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a266-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="6a266-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a266-157">a.</span></span> <span data-ttu-id="6a266-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="6a266-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="6a266-159">b.</span><span class="sxs-lookup"><span data-stu-id="6a266-159">b.</span></span> <span data-ttu-id="6a266-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="6a266-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a266-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6a266-161">These values are not real.</span></span> <span data-ttu-id="6a266-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="6a266-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6a266-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique AppDynamics](https://www.appdynamics.com/support/).</span><span class="sxs-lookup"><span data-stu-id="6a266-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="6a266-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6a266-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="6a266-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6a266-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a266-168">Dans la section **Configuration de AppDynamics**, cliquez sur **Configurer AppDynamics** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6a266-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6a266-169">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="6a266-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="6a266-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise AppDynamics en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6a266-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="6a266-172">Dans la barre d’outils située en haut, cliquez sur **Paramètres**, puis sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="6a266-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="6a266-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="6a266-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="6a266-174">Cliquez sur l’onglet **Authentication Provider** .</span><span class="sxs-lookup"><span data-stu-id="6a266-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="6a266-175">![Fournisseur d’authentification](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Fournisseur d’authentification")</span><span class="sxs-lookup"><span data-stu-id="6a266-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="6a266-176">Dans la section **Authentication Provider** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a266-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6a266-177">![Configuration SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="6a266-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="6a266-178">a.</span><span class="sxs-lookup"><span data-stu-id="6a266-178">a.</span></span> <span data-ttu-id="6a266-179">Dans **Fournisseur d’authentification**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6a266-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="6a266-180">b.</span><span class="sxs-lookup"><span data-stu-id="6a266-180">b.</span></span> <span data-ttu-id="6a266-181">Dans la zone de texte **URL de connexion**, collez la valeur de **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6a266-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a266-182">c.</span><span class="sxs-lookup"><span data-stu-id="6a266-182">c.</span></span> <span data-ttu-id="6a266-183">Dans la zone de texte **URL de déconnexion**, collez la valeur de **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6a266-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="6a266-184">d.</span><span class="sxs-lookup"><span data-stu-id="6a266-184">d.</span></span> <span data-ttu-id="6a266-185">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="6a266-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="6a266-186">e.</span><span class="sxs-lookup"><span data-stu-id="6a266-186">e.</span></span> <span data-ttu-id="6a266-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6a266-187">Click **Save**.</span></span>

     <span data-ttu-id="6a266-188">![Enregistrer](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "enregistrer")</span><span class="sxs-lookup"><span data-stu-id="6a266-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="6a266-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6a266-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a266-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6a266-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a266-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a266-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a266-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a266-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6a266-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6a266-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6a266-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a266-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a266-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a266-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6a266-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a266-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6a266-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a266-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a266-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a266-204">a.</span><span class="sxs-lookup"><span data-stu-id="6a266-204">a.</span></span> <span data-ttu-id="6a266-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a266-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a266-206">b.</span><span class="sxs-lookup"><span data-stu-id="6a266-206">b.</span></span> <span data-ttu-id="6a266-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a266-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a266-208">c.</span><span class="sxs-lookup"><span data-stu-id="6a266-208">c.</span></span> <span data-ttu-id="6a266-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6a266-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a266-210">d.</span><span class="sxs-lookup"><span data-stu-id="6a266-210">d.</span></span> <span data-ttu-id="6a266-211">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6a266-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="6a266-212">Création d’un utilisateur de test AppDynamics</span><span class="sxs-lookup"><span data-stu-id="6a266-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="6a266-213">Pour permettre aux utilisateurs Azure AD de se connecter à AppDynamics, vous devez les approvisionner dans AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="6a266-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="6a266-214">En l’occurrence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="6a266-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="6a266-215">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6a266-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6a266-216">Connectez-vous à votre site d’entreprise AppDynamics en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6a266-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="6a266-217">Accédez à **Utilisateurs**, puis cliquez sur **+** pour ouvrir la boîte de dialogue **Créer un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="6a266-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="6a266-218">![Utilisateurs](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="6a266-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="6a266-219">Dans la section **Créer un utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a266-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6a266-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="6a266-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="6a266-221">a.</span><span class="sxs-lookup"><span data-stu-id="6a266-221">a.</span></span> <span data-ttu-id="6a266-222">Tapez le **nom d’utilisateur**, le **nom**, **l’adresse e-mail**, le **nouveau mot de passe** et la **confirmation du nouveau mot de passe** d’un compte AAD valide que vous souhaitez approvisionner dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="6a266-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="6a266-223">b.</span><span class="sxs-lookup"><span data-stu-id="6a266-223">b.</span></span> <span data-ttu-id="6a266-224">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6a266-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6a266-225">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par AppDynamics pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a266-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a266-226">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a266-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a266-227">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="6a266-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6a266-229">**Pour affecter Britta Simon à AppDynamics, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="6a266-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="6a266-230">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6a266-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6a266-232">Dans la liste des applications, sélectionnez **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="6a266-232">In the applications list, select **AppDynamics**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="6a266-234">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6a266-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6a266-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6a266-236">Click **Add** button.</span></span> <span data-ttu-id="6a266-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6a266-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6a266-239">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6a266-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a266-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6a266-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a266-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6a266-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a266-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6a266-242">Testing single sign-on</span></span>

<span data-ttu-id="6a266-243">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6a266-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a266-244">Quand vous cliquez sur la vignette AppDynamics dans le volet d’accès, vous devez être connecté automatiquement à votre application AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="6a266-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a266-245">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6a266-245">Additional resources</span></span>

* [<span data-ttu-id="6a266-246">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a266-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a266-247">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6a266-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

