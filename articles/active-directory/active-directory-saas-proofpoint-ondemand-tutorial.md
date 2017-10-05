---
title: "Didacticiel : Intégration d’Azure Active Directory à Proofpoint on Demand | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Proofpoint on Demand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="3a506-103">Didacticiel : Intégration d’Azure Active Directory avec Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="3a506-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="3a506-104">Dans ce didacticiel, vous allez apprendre à intégrer Proofpoint on Demand à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a506-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a506-105">L’intégration de Proofpoint on Demand dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3a506-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a506-106">Dans Azure AD, vous pouvez contrôler l’accès à Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="3a506-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="3a506-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Proofpoint on Demand (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a506-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3a506-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3a506-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a506-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a506-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3a506-110">Prerequisites</span></span>

<span data-ttu-id="3a506-111">Pour configurer l’intégration d’Azure AD avec Proofpoint on Demand, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3a506-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="3a506-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a506-113">Un abonnement Proofpoint on Demand pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3a506-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a506-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3a506-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a506-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3a506-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a506-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3a506-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a506-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a506-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a506-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3a506-118">Scenario description</span></span>
<span data-ttu-id="3a506-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3a506-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a506-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a506-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a506-121">Ajouter Proofpoint on Demand à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3a506-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="3a506-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="3a506-123">Ajouter Proofpoint on Demand à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3a506-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="3a506-124">Pour configurer l’intégration de Proofpoint on Demand à Azure AD, vous devez ajouter Proofpoint on Demand à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3a506-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a506-125">**Pour ajouter Proofpoint on Demand à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3a506-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a506-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a506-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a506-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3a506-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a506-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3a506-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3a506-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3a506-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3a506-133">Dans la zone de recherche, tapez **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="3a506-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="3a506-135">Dans le panneau des résultats, sélectionnez **Proofpoint on Demand**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3a506-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a506-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a506-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Proofpoint on Demand grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3a506-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a506-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Proofpoint on Demand équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a506-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="3a506-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Proofpoint on Demand associé.</span><span class="sxs-lookup"><span data-stu-id="3a506-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="3a506-141">Pour cela, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** dans Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="3a506-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="3a506-142">Pour configurer et tester l’authentification unique Azure AD avec Proofpoint on Demand, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="3a506-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a506-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3a506-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a506-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a506-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a506-145">**[Création d’un utilisateur de test Proofpoint on Demand](#creating-a-proofpoint-on-demand-test-user)** pour avoir un équivalent de Britta Simon dans Proofpoint on Demand qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a506-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a506-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a506-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a506-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3a506-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a506-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a506-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="3a506-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="3a506-150">**Pour configurer l’authentification unique Azure AD avec Proofpoint on Demand, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="3a506-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="3a506-151">Dans le portail Azure, sur la page d’intégration de l’application **Proofpoint on Demand**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3a506-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3a506-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3a506-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="3a506-155">Dans la section **Domaine et URL Proofpoint on Demand**, réalisez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a506-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="3a506-157">a. Dans la zone de texte **URL de connexion**, entrez une URL selon le modèle suivant : `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="3a506-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="3a506-158">b.</span><span class="sxs-lookup"><span data-stu-id="3a506-158">b.</span></span> <span data-ttu-id="3a506-159">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="3a506-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="3a506-160">c.</span><span class="sxs-lookup"><span data-stu-id="3a506-160">c.</span></span>  <span data-ttu-id="3a506-161">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="3a506-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3a506-162">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3a506-162">These values are not the real.</span></span> <span data-ttu-id="3a506-163">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="3a506-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="3a506-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="3a506-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="3a506-165">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3a506-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="3a506-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3a506-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3a506-169">Pour ouvrir la fenêtre **Configurer l’authentification**, sur la section **Configuration de Proofpoint on Demand**, cliquez sur **Configurer Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="3a506-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a506-170">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="3a506-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="3a506-172">Pour configurer l’authentification unique côté **Proofpoint on Demand**, vous devez envoyer le **Certificat (Base64)** téléchargé, l’**ID d’entité SAML** et l’**URL du service d’authentification unique SAML** à l’[équipe de support technique Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="3a506-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="3a506-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="3a506-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a506-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="3a506-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a506-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a506-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a506-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a506-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3a506-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3a506-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3a506-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a506-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a506-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a506-182">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3a506-182">These values are not the real.</span></span> <span data-ttu-id="3a506-183">Mettez à jour ces valeurs avec les valeurs réelles</span><span class="sxs-lookup"><span data-stu-id="3a506-183">Update these values with the actual</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a506-185">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3a506-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a506-187">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3a506-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a506-189">a.</span><span class="sxs-lookup"><span data-stu-id="3a506-189">a.</span></span> <span data-ttu-id="3a506-190">Dans la zone de texte **Name**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a506-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3a506-191">b.</span><span class="sxs-lookup"><span data-stu-id="3a506-191">b.</span></span> <span data-ttu-id="3a506-192">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a506-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3a506-193">c.</span><span class="sxs-lookup"><span data-stu-id="3a506-193">c.</span></span> <span data-ttu-id="3a506-194">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3a506-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a506-195">d.</span><span class="sxs-lookup"><span data-stu-id="3a506-195">d.</span></span> <span data-ttu-id="3a506-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3a506-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="3a506-197">Créer un utilisateur de test Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="3a506-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="3a506-198">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="3a506-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="3a506-199">Collaborez avec l’[équipe de support aux clients Proofpoint on Demand](https://www.proofpoint.com/us/support-services) pour ajouter des utilisateurs sur la plateforme Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="3a506-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3a506-200">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a506-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3a506-201">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="3a506-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3a506-203">**Pour assigner Britta Simon à Proofpoint on Demand, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="3a506-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="3a506-204">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3a506-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3a506-206">Dans la liste des applications, sélectionnez **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="3a506-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="3a506-208">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3a506-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3a506-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3a506-210">Click **Add** button.</span></span> <span data-ttu-id="3a506-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3a506-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3a506-213">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3a506-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a506-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3a506-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a506-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3a506-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a506-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3a506-216">Testing single sign-on</span></span>

<span data-ttu-id="3a506-217">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3a506-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a506-218">Lorsque vous cliquez sur la mosaïque **Proofpoint on Demand** dans le volet d’accès, vous devez être automatiquement connecté à votre application Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="3a506-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="3a506-219">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a506-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="3a506-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3a506-220">Additional resources</span></span>

* [<span data-ttu-id="3a506-221">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a506-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a506-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3a506-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

