---
title: "Didacticiel : intégration d’Azure Active Directory à Small Improvements | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Small Improvements."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 49a8cd3acfc6df15ef6a51171c8421162bc94efc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="a6228-103">Didacticiel : intégration d’Azure Active Directory avec Small Improvements</span><span class="sxs-lookup"><span data-stu-id="a6228-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="a6228-104">Dans ce didacticiel, vous allez apprendre à intégrer Small Improvements à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6228-104">In this tutorial, you learn how to integrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6228-105">L’intégration de Small Improvements à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a6228-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a6228-106">Dans Azure AD, vous pouvez contrôler qui a accès à Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="a6228-106">You can control in Azure AD who has access to Small Improvements</span></span>
- <span data-ttu-id="a6228-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Small Improvements (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6228-107">You can enable your users to automatically get signed-on to Small Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6228-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a6228-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a6228-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6228-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6228-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a6228-110">Prerequisites</span></span>

<span data-ttu-id="a6228-111">Pour configurer l’intégration d’Azure AD avec Small Improvements, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a6228-111">To configure Azure AD integration with Small Improvements, you need the following items:</span></span>

- <span data-ttu-id="a6228-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6228-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6228-113">Un abonnement Small Improvements pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a6228-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6228-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a6228-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6228-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a6228-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6228-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a6228-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6228-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6228-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6228-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a6228-118">Scenario description</span></span>
<span data-ttu-id="a6228-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a6228-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6228-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6228-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6228-121">Ajout de Small Improvements à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a6228-121">Adding Small Improvements from the gallery</span></span>
2. <span data-ttu-id="a6228-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6228-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-the-gallery"></a><span data-ttu-id="a6228-123">Ajout de Small Improvements à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a6228-123">Adding Small Improvements from the gallery</span></span>
<span data-ttu-id="a6228-124">Pour configurer l’intégration de Small Improvements avec Azure AD, vous devez ajouter Small Improvements à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a6228-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a6228-125">**Pour ajouter Small Improvements à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6228-125">**To add Small Improvements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a6228-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6228-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6228-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a6228-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a6228-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a6228-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a6228-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a6228-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a6228-133">Dans la zone de recherche, tapez **Small Improvements**.</span><span class="sxs-lookup"><span data-stu-id="a6228-133">In the search box, type **Small Improvements**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="a6228-135">Dans le volet de résultats, sélectionnez **Small Improvements**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a6228-135">In the results panel, select **Small Improvements**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6228-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6228-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6228-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD après de Small Improvements, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a6228-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a6228-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Small Improvements équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6228-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Small Improvements is to a user in Azure AD.</span></span> <span data-ttu-id="a6228-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Small Improvements associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a6228-140">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span></span>

<span data-ttu-id="a6228-141">Dans Small Improvements, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a6228-141">In Small Improvements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a6228-142">Pour configurer et tester l’authentification unique Azure AD avec Small Improvements, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6228-142">To configure and test Azure AD single sign-on with Small Improvements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a6228-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a6228-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a6228-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6228-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6228-145">**[Création d’un utilisateur de test Small Improvements](#creating-a-small-improvements-test-user)** pour avoir un équivalent de Britta Simon dans Small Improvements lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a6228-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6228-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6228-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6228-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a6228-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6228-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6228-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6228-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="a6228-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="a6228-150">**Pour configurer l’authentification unique Azure AD avec Small Improvements, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6228-150">**To configure Azure AD single sign-on with Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="a6228-151">Dans le Portail Azure, dans la page d’intégration de l’application **Small Improvements**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a6228-151">In the Azure portal, on the **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a6228-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a6228-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="a6228-155">Dans la section **Domaine et URL Small Improvements**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6228-155">On the **Small Improvements Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="a6228-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6228-157">a.</span></span> <span data-ttu-id="a6228-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="a6228-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="a6228-159">b.</span><span class="sxs-lookup"><span data-stu-id="a6228-159">b.</span></span> <span data-ttu-id="a6228-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="a6228-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6228-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a6228-161">These values are not real.</span></span> <span data-ttu-id="a6228-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="a6228-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a6228-163">Contactez l’[équipe de support client Small Improvements](mailto:support@small-improvements.com) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a6228-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a6228-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a6228-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="a6228-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a6228-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6228-168">Dans la section **Configuration de Small Improvements**, cliquez sur **Configurer Small Improvements** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a6228-168">On the **Small Improvements Configuration** section, click **Configure Small Improvements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a6228-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a6228-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="a6228-171">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise Small Improvements en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a6228-171">In another browser window, sign on to your Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="a6228-172">Sur la page du tableau de bord principal, cliquez sur le bouton **Administration** situé sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="a6228-172">From the main dashboard page, click **Administration** button on the left.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="a6228-174">Cliquez sur le bouton **SAML SSO** de la section **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="a6228-174">Click the **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="a6228-176">Sur la page de configuration de l’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6228-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="a6228-178">a.</span><span class="sxs-lookup"><span data-stu-id="a6228-178">a.</span></span> <span data-ttu-id="a6228-179">Dans la zone de texte **Point de terminaison HTTP**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a6228-179">In the **HTTP Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a6228-180">b.</span><span class="sxs-lookup"><span data-stu-id="a6228-180">b.</span></span> <span data-ttu-id="a6228-181">Ouvrez le certificat que vous avez téléchargé dans le Bloc-notes, copiez son contenu, puis collez-le dans la zone de texte **Certificat x509** .</span><span class="sxs-lookup"><span data-stu-id="a6228-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="a6228-182">c.</span><span class="sxs-lookup"><span data-stu-id="a6228-182">c.</span></span> <span data-ttu-id="a6228-183">Si vous souhaitez que les utilisateurs disposent de l’authentification unique et de l’option d’authentification par formulaire de connexion, activez l’option **Activer l’accès également via une connexion/un mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a6228-183">If you wish to have SSO and Login form authentication option available for users, then check the **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="a6228-184">d.</span><span class="sxs-lookup"><span data-stu-id="a6228-184">d.</span></span> <span data-ttu-id="a6228-185">Entrez les informations appropriées pour nommer le bouton de connexion d’authentification unique dans la zone de texte **SAML Prompt** .</span><span class="sxs-lookup"><span data-stu-id="a6228-185">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="a6228-186">e.</span><span class="sxs-lookup"><span data-stu-id="a6228-186">e.</span></span> <span data-ttu-id="a6228-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a6228-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a6228-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a6228-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a6228-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a6228-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a6228-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6228-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6228-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6228-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6228-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a6228-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a6228-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6228-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a6228-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6228-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6228-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a6228-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6228-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a6228-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6228-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6228-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6228-203">a.</span><span class="sxs-lookup"><span data-stu-id="a6228-203">a.</span></span> <span data-ttu-id="a6228-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6228-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6228-205">b.</span><span class="sxs-lookup"><span data-stu-id="a6228-205">b.</span></span> <span data-ttu-id="a6228-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6228-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6228-207">c.</span><span class="sxs-lookup"><span data-stu-id="a6228-207">c.</span></span> <span data-ttu-id="a6228-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a6228-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a6228-209">d.</span><span class="sxs-lookup"><span data-stu-id="a6228-209">d.</span></span> <span data-ttu-id="a6228-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6228-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="a6228-211">Création d'un utilisateur de test Small Improvements</span><span class="sxs-lookup"><span data-stu-id="a6228-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="a6228-212">Pour se connecter à Small Improvements, les utilisateurs d’Azure AD doivent être approvisionnés dans Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="a6228-212">To enable Azure AD users to log in to Small Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="a6228-213">Dans le cas de Small Improvements, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="a6228-213">In the case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="a6228-214">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6228-214">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a6228-215">Connectez-vous à votre site d’entreprise Small Improvements en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a6228-215">Sign-on to your Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="a6228-216">À partir de la page d’accueil, accédez au menu de gauche, puis cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="a6228-216">From the Home page, go to the menu on the left, click **Administration**.</span></span>

3. <span data-ttu-id="a6228-217">Cliquez sur le bouton **User Directory** dans la section User Management.</span><span class="sxs-lookup"><span data-stu-id="a6228-217">Click the **User Directory** button from User Management section.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="a6228-219">Cliquez sur **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="a6228-219">Click **Add users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="a6228-221">Dans la boîte de dialogue **Add users** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a6228-221">On the **Add Users** dialog, perform the following steps:</span></span> 

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="a6228-223">a.</span><span class="sxs-lookup"><span data-stu-id="a6228-223">a.</span></span> <span data-ttu-id="a6228-224">Entrez le **prénom** de l’utilisateur, à savoir **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a6228-224">Enter the **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="a6228-225">b.</span><span class="sxs-lookup"><span data-stu-id="a6228-225">b.</span></span> <span data-ttu-id="a6228-226">Entrez le **nom de famille** de l’utilisateur, à savoir **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a6228-226">Enter the **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="a6228-227">c.</span><span class="sxs-lookup"><span data-stu-id="a6228-227">c.</span></span> <span data-ttu-id="a6228-228">Entrez l’**adresse e-mail** de l’utilisateur, à savoir **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a6228-228">Enter the **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="a6228-229">d.</span><span class="sxs-lookup"><span data-stu-id="a6228-229">d.</span></span> <span data-ttu-id="a6228-230">Vous pouvez également choisir d’entrer le message personnel dans la zone **Envoyer un e-mail de notification** .</span><span class="sxs-lookup"><span data-stu-id="a6228-230">You can also choose to enter the personal message in the **Send notification email** box.</span></span> <span data-ttu-id="a6228-231">Décochez cette case si vous ne souhaitez envoyer de notification.</span><span class="sxs-lookup"><span data-stu-id="a6228-231">If you do not wish to send the notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="a6228-232">e.</span><span class="sxs-lookup"><span data-stu-id="a6228-232">e.</span></span> <span data-ttu-id="a6228-233">Cliquez sur **Créer des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a6228-233">Click **Create Users**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a6228-234">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6228-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a6228-235">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="a6228-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Small Improvements.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a6228-237">**Pour affecter Britta Simon à Small Improvements, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a6228-237">**To assign Britta Simon to Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="a6228-238">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a6228-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a6228-240">Dans la liste des applications, sélectionnez **Small Improvements**.</span><span class="sxs-lookup"><span data-stu-id="a6228-240">In the applications list, select **Small Improvements**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="a6228-242">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a6228-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a6228-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a6228-244">Click **Add** button.</span></span> <span data-ttu-id="a6228-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a6228-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a6228-247">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a6228-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a6228-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a6228-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6228-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a6228-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6228-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a6228-250">Testing single sign-on</span></span>

<span data-ttu-id="a6228-251">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a6228-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="a6228-252">Lorsque vous cliquez sur la vignette Small Improvements dans le volet d’accès, vous devez être connecté automatiquement à votre application Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="a6228-252">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6228-253">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a6228-253">Additional resources</span></span>

* [<span data-ttu-id="a6228-254">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6228-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6228-255">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a6228-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

