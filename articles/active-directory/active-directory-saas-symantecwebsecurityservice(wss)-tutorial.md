---
title: "Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Symantec Web Security Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d0738bb750a82863b2f77540e8e7b94cca4b64e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="af27f-103">Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="af27f-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="af27f-104">Dans ce tutoriel, vous allez apprendre à intégrer Symantec Web Security Service (WSS) à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af27f-104">In this tutorial, you learn how to integrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af27f-105">L’intégration de Symantec Web Security Service (WSS) à Azure AD vous fait bénéficier des avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="af27f-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="af27f-106">Vous pouvez contrôler dans Azure AD qui a accès à Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="af27f-106">You can control in Azure AD who has access to Symantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="af27f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Symantec Web Security Service (WSS) (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af27f-107">You can enable your users to automatically get signed-on to Symantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af27f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="af27f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="af27f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af27f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af27f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="af27f-110">Prerequisites</span></span>

<span data-ttu-id="af27f-111">Pour configurer l’intégration d’Azure AD à Symantec Web Security Service (WSS), vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="af27f-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="af27f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="af27f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af27f-113">Un abonnement Symantec Web Security Service (WSS) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="af27f-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af27f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="af27f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af27f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="af27f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af27f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="af27f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af27f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af27f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af27f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="af27f-118">Scenario description</span></span>
<span data-ttu-id="af27f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="af27f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af27f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="af27f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af27f-121">Ajout de Symantec Web Security Service (WSS) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="af27f-121">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
2. <span data-ttu-id="af27f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="af27f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="af27f-123">Ajout de Symantec Web Security Service (WSS) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="af27f-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="af27f-124">Pour configurer l’intégration de Symantec Web Security Service (WSS) à Azure AD, vous devez ajouter Symantec Web Security Service (WSS) à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="af27f-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="af27f-125">**Pour ajouter Symantec Web Security Service (WSS) à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="af27f-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="af27f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af27f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="af27f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="af27f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="af27f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="af27f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="af27f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="af27f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="af27f-133">Dans la zone de recherche, tapez **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="af27f-133">In the search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="af27f-135">Dans le volet de résultats, sélectionnez **Symantec Web Security Service (WSS)**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="af27f-135">In the results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="af27f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="af27f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="af27f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="af27f-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af27f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Symantec Web Security Service (WSS) équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af27f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="af27f-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Symantec Web Security Service (WSS) associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="af27f-140">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="af27f-141">Dans Symantec Web Security Service (WSS), affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="af27f-141">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="af27f-142">Pour configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS), vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="af27f-142">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="af27f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="af27f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="af27f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af27f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af27f-145">**[Création d’un utilisateur de test Symantec Web Security Service (WSS)](#creating-a-symantec-web-security-service-wss-test-user)** pour avoir dans Symantec Web Security Service (WSS) un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="af27f-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="af27f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af27f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af27f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="af27f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="af27f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="af27f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="af27f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="af27f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="af27f-150">**Pour configurer l’authentification unique Azure AD avec Symantec Web Security Service (WSS), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="af27f-150">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="af27f-151">Dans le portail Azure, dans la page d’intégration de l’application **Symantec Web Security Service (WSS)**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="af27f-151">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="af27f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="af27f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="af27f-155">Dans la section **Domaine et URL Symantec Web Security Service (WSS)** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="af27f-155">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="af27f-157">a.</span><span class="sxs-lookup"><span data-stu-id="af27f-157">a.</span></span> <span data-ttu-id="af27f-158">Dans la zone de texte **URL de connexion**, indiquez l’URL à bloquer conformément à la stratégie de blocage de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="af27f-158">In the **Sign-on URL** textbox, mention the url, which you want to block according to the blocking policy of the Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="af27f-159">b.</span><span class="sxs-lookup"><span data-stu-id="af27f-159">b.</span></span> <span data-ttu-id="af27f-160">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="af27f-160">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="af27f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="af27f-161">These values are not real.</span></span> <span data-ttu-id="af27f-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="af27f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="af27f-163">Contactez l’[équipe de support client Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="af27f-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="af27f-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="af27f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="af27f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="af27f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af27f-168">Pour configurer l’authentification unique côté **Symantec Web Security Service (WSS)**, vous devez envoyer le **XML de métadonnées** téléchargé à l’[équipe de support technique Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="af27f-168">To configure single sign-on on **Symantec Web Security Service (WSS)** side, you need to send the downloaded **Metadata XML** to [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="af27f-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="af27f-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="af27f-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="af27f-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="af27f-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="af27f-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="af27f-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="af27f-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="af27f-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="af27f-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="af27f-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="af27f-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="af27f-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af27f-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af27f-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="af27f-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af27f-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="af27f-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af27f-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="af27f-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af27f-184">a.</span><span class="sxs-lookup"><span data-stu-id="af27f-184">a.</span></span> <span data-ttu-id="af27f-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af27f-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af27f-186">b.</span><span class="sxs-lookup"><span data-stu-id="af27f-186">b.</span></span> <span data-ttu-id="af27f-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af27f-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af27f-188">c.</span><span class="sxs-lookup"><span data-stu-id="af27f-188">c.</span></span> <span data-ttu-id="af27f-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="af27f-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="af27f-190">d.</span><span class="sxs-lookup"><span data-stu-id="af27f-190">d.</span></span> <span data-ttu-id="af27f-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="af27f-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="af27f-192">Création d’un utilisateur de test Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="af27f-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="af27f-193">Dans cette section, vous créez un utilisateur appelé Britta Simon dans Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="af27f-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="af27f-194">Consultez l’[équipe de support technique Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) pour ajouter les utilisateurs dans la plateforme Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="af27f-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add the users in the Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="af27f-195">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="af27f-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="af27f-196">En plus des détails de l’utilisateur, vous devez envoyer l’adresse IP publique de l’ordinateur à partir duquel vous tentez d’accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="af27f-196">Also along with the user details you need to send the public IPaddress of the machine from which you are trying to access the application.</span></span>

> [!NOTE]
> <span data-ttu-id="af27f-197">[Cliquez ici](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) pour obtenir l’adresse IP publique de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="af27f-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="af27f-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="af27f-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="af27f-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="af27f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="af27f-201">**Pour affecter Britta Simon à Symantec Web Security Service (WSS), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="af27f-201">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="af27f-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="af27f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="af27f-204">Dans la liste des applications, sélectionnez **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="af27f-204">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="af27f-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="af27f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="af27f-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="af27f-208">Click **Add** button.</span></span> <span data-ttu-id="af27f-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="af27f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="af27f-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="af27f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="af27f-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="af27f-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af27f-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="af27f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="af27f-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="af27f-214">Testing single sign-on</span></span>

<span data-ttu-id="af27f-215">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="af27f-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="af27f-216">Quand vous cliquez sur la vignette Symantec Web Security Service (WSS) dans le volet d’accès, vous êtes redirigé vers la page de blocage pour laquelle la stratégie de blocage a été configurée.</span><span class="sxs-lookup"><span data-stu-id="af27f-216">When you click the Symantec Web Security Service (WSS) tile in the Access Panel, you get redirected to the blocking page for which the blocking policy has been configured.</span></span>
<span data-ttu-id="af27f-217">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="af27f-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af27f-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="af27f-218">Additional resources</span></span>

* [<span data-ttu-id="af27f-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af27f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af27f-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="af27f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

