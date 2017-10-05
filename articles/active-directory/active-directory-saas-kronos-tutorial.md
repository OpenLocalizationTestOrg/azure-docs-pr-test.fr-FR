---
title: "Didacticiel : Intégration d’Azure Active Directory à Kronos | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="a2d1e-103">Didacticiel : Intégration d’Azure Active Directory à Kronos</span><span class="sxs-lookup"><span data-stu-id="a2d1e-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="a2d1e-104">Dans ce didacticiel, vous allez apprendre à intégrer Kronos à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2d1e-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2d1e-105">L’intégration de Kronos dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a2d1e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Kronos</span><span class="sxs-lookup"><span data-stu-id="a2d1e-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="a2d1e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Kronos (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2d1e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a2d1e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a2d1e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2d1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2d1e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a2d1e-110">Prerequisites</span></span>

<span data-ttu-id="a2d1e-111">Pour configurer l’intégration d’Azure AD avec Kronos, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="a2d1e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2d1e-113">Un abonnement **Kronos Workforce Central** pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a2d1e-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2d1e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2d1e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2d1e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2d1e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2d1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2d1e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a2d1e-118">Scenario description</span></span>
<span data-ttu-id="a2d1e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2d1e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2d1e-121">Ajout de Kronos à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a2d1e-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="a2d1e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="a2d1e-123">Ajout de Kronos à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a2d1e-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="a2d1e-124">Pour configurer l’intégration de Kronos avec Azure AD, vous devez ajouter Kronos à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a2d1e-125">**Pour ajouter Kronos à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2d1e-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a2d1e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2d1e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a2d1e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a2d1e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a2d1e-133">Dans la zone de recherche, entrez **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-133">In the search box, type **Kronos**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="a2d1e-135">Dans le volet de résultats, sélectionnez **Kronos**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2d1e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2d1e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kronos avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a2d1e-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2d1e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Kronos équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="a2d1e-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Kronos associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="a2d1e-141">Dans Kronos, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a2d1e-142">Pour configurer et tester l’authentification unique Azure AD avec Kronos, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a2d1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a2d1e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2d1e-145">**[Création d’un utilisateur de test Kronos](#creating-a-kronos-test-user)** pour avoir un équivalent de Britta Simon dans Kronos lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2d1e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2d1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2d1e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2d1e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kronos.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="a2d1e-150">**Pour configurer l’authentification unique Azure AD avec Kronos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2d1e-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="a2d1e-151">Dans le portail Azure, sur la page d’intégration de l’application **Kronos**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a2d1e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="a2d1e-155">Dans la section **Domaine et URL Kronos**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="a2d1e-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-157">a.</span></span> <span data-ttu-id="a2d1e-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="a2d1e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="a2d1e-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-159">b.</span></span> <span data-ttu-id="a2d1e-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="a2d1e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2d1e-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-161">These values are not real.</span></span> <span data-ttu-id="a2d1e-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a2d1e-163">Pour obtenir ces valeurs, contactez l’[l’équipe de support technique de Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="a2d1e-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="a2d1e-164">Votre application Kronos attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a2d1e-165">Collaborez avec [l’équipe de support de Kronos](https://www.kronos.in/contact/en-in/form) pour identifier tout d’abord l’identificateur utilisateur correct qui est mappé à l’application.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="a2d1e-166">Suivez également les instructions sur l’attribut à utiliser pour ce mappage.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="a2d1e-167">Microsoft recommande d’utiliser l’attribut **« NameIdentifier »** en tant qu’identificateur utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="a2d1e-168">Vous pouvez gérer les valeurs de ces attributs à partir de la section **« Attributs utilisateur »** sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="a2d1e-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="a2d1e-170">Ici, nous avons mappé **l’identificateur d’utilisateur (nameid)** avec la fonction **ExtractMailPrefix()** de **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="a2d1e-171">Cela donne la valeur de préfixe de l’adresse de messagerie de l’utilisateur qui est l’ID d’utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="a2d1e-172">Celle-ci est envoyée à l’application Kronos pour chaque réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="a2d1e-174">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique** :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="a2d1e-175">a.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-175">a.</span></span> <span data-ttu-id="a2d1e-176">Dans la liste déroulante Identificateur de l’utilisateur, sélectionnez **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="a2d1e-177">b.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-177">b.</span></span> <span data-ttu-id="a2d1e-178">Dans la liste déroulante **E-mail**, sélectionnez **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="a2d1e-179">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="a2d1e-181">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a2d1e-181">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a2d1e-183">Pour configurer l’authentification unique côté **Kronos**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique de Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="a2d1e-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="a2d1e-184">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a2d1e-185">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a2d1e-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2d1e-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2d1e-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2d1e-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a2d1e-190">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2d1e-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a2d1e-191">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2d1e-193">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2d1e-195">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2d1e-197">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2d1e-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2d1e-199">a.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-199">a.</span></span> <span data-ttu-id="a2d1e-200">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2d1e-201">b.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-201">b.</span></span> <span data-ttu-id="a2d1e-202">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2d1e-203">c.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-203">c.</span></span> <span data-ttu-id="a2d1e-204">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a2d1e-205">d.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-205">d.</span></span> <span data-ttu-id="a2d1e-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="a2d1e-207">Création d’un utilisateur de test Kronos</span><span class="sxs-lookup"><span data-stu-id="a2d1e-207">Creating a Kronos test user</span></span>

<span data-ttu-id="a2d1e-208">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Kronos.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="a2d1e-209">Tous les utilisateurs de Kronos doivent être configurés dans cette application avant de procéder à l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="a2d1e-210">Collaborez avec l’[équipe de support technique de Kronos](https://www.kronos.in/contact/en-in/form) pour approvisionner tous ces utilisateurs dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a2d1e-211">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d1e-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a2d1e-212">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Kronos.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a2d1e-214">**Pour affecter Britta Simon à Kronos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2d1e-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="a2d1e-215">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a2d1e-217">Dans la liste des applications, sélectionnez **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-217">In the applications list, select **Kronos**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="a2d1e-219">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a2d1e-221">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-221">Click **Add** button.</span></span> <span data-ttu-id="a2d1e-222">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a2d1e-224">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a2d1e-225">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2d1e-226">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2d1e-227">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a2d1e-227">Testing single sign-on</span></span>

<span data-ttu-id="a2d1e-228">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a2d1e-229">Lorsque vous cliquez sur la mosaïque Kronos dans le volet d’accès, vous devez être connecté automatiquement à votre application Kronos.</span><span class="sxs-lookup"><span data-stu-id="a2d1e-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2d1e-230">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a2d1e-230">Additional resources</span></span>

* [<span data-ttu-id="a2d1e-231">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d1e-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2d1e-232">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a2d1e-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

