---
title: "Didacticiel : Intégration d’Azure Active Directory à SumoLogic | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="acb8f-103">Didacticiel : Intégration d’Azure Active Directory à SumoLogic</span><span class="sxs-lookup"><span data-stu-id="acb8f-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="acb8f-104">Dans ce didacticiel, vous allez apprendre à intégrer SumoLogic avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acb8f-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acb8f-105">L’intégration de SumoLogic dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="acb8f-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="acb8f-106">Dans Azure AD, vous pouvez contrôler qui a accès à SumoLogic</span><span class="sxs-lookup"><span data-stu-id="acb8f-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="acb8f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à SumoLogic (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="acb8f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="acb8f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="acb8f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="acb8f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acb8f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="acb8f-110">Prerequisites</span></span>

<span data-ttu-id="acb8f-111">Pour configurer l’intégration d’Azure AD à SumoLogic, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="acb8f-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="acb8f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acb8f-113">Un abonnement SumoLogic pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="acb8f-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acb8f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="acb8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acb8f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="acb8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acb8f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="acb8f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acb8f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acb8f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acb8f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="acb8f-118">Scenario description</span></span>
<span data-ttu-id="acb8f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="acb8f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acb8f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="acb8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acb8f-121">Ajout de SumoLogic à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="acb8f-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="acb8f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="acb8f-123">Ajout de SumoLogic à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="acb8f-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="acb8f-124">Pour configurer l’intégration de SumoLogic dans Azure AD, vous devez ajouter SumoLogic à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="acb8f-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="acb8f-125">**Pour ajouter SumoLogic à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="acb8f-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="acb8f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="acb8f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="acb8f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="acb8f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="acb8f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="acb8f-133">Dans la zone de recherche, entrez **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-133">In the search box, type **SumoLogic**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="acb8f-135">Dans le panneau des résultats, sélectionnez **SumoLogic**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="acb8f-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="acb8f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="acb8f-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec SumoLogic, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="acb8f-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="acb8f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SumoLogic équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acb8f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="acb8f-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur SumoLogic associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="acb8f-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="acb8f-141">Dans SumoLogic, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="acb8f-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="acb8f-142">Pour configurer et tester l’authentification unique Azure AD avec SumoLogic, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="acb8f-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="acb8f-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="acb8f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="acb8f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acb8f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acb8f-145">**[Création d’un utilisateur de test SumoLogic](#creating-a-sumologic-test-user)** pour obtenir un équivalent de Britta Simon dans SumoLogic lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="acb8f-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="acb8f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acb8f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acb8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="acb8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="acb8f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="acb8f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="acb8f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="acb8f-150">**Pour configurer l’authentification unique Azure AD avec SumoLogic, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="acb8f-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="acb8f-151">Dans le portail Azure, dans la page d’intégration de l’application **SumoLogic**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="acb8f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="acb8f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="acb8f-155">Dans la section **Domaine et URL SumoLogic**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="acb8f-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="acb8f-157">a.</span><span class="sxs-lookup"><span data-stu-id="acb8f-157">a.</span></span> <span data-ttu-id="acb8f-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="acb8f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="acb8f-159">b.</span><span class="sxs-lookup"><span data-stu-id="acb8f-159">b.</span></span> <span data-ttu-id="acb8f-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="acb8f-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="acb8f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="acb8f-161">These values are not real.</span></span> <span data-ttu-id="acb8f-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="acb8f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="acb8f-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique SumoLogic](https://www.sumologic.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="acb8f-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="acb8f-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="acb8f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="acb8f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="acb8f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="acb8f-168">Dans la section **Configuration de SumoLogic**, cliquez sur **Configurer SumoLogic** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="acb8f-169">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="acb8f-171">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise SumoLogic en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="acb8f-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="acb8f-172">Accédez à **Manage \> Security**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="acb8f-173">![Gestion](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gestion")</span><span class="sxs-lookup"><span data-stu-id="acb8f-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="acb8f-174">Cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="acb8f-175">![Paramètres de sécurité globaux](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Paramètres de sécurité globaux")</span><span class="sxs-lookup"><span data-stu-id="acb8f-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="acb8f-176">Dans la liste **Select a configuration or create a new one**, sélectionnez **Azure AD**, puis cliquez sur **Configure**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="acb8f-177">![Configurer SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurer SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="acb8f-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="acb8f-178">Dans la boîte de dialogue **Configure SAML 2.0** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="acb8f-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="acb8f-179">![Configurer SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurer SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="acb8f-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="acb8f-180">a.</span><span class="sxs-lookup"><span data-stu-id="acb8f-180">a.</span></span> <span data-ttu-id="acb8f-181">Dans la zone de texte **Configuration Name**, entrez **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="acb8f-182">b.</span><span class="sxs-lookup"><span data-stu-id="acb8f-182">b.</span></span> <span data-ttu-id="acb8f-183">Sélectionnez **Debug Mode**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="acb8f-184">c.</span><span class="sxs-lookup"><span data-stu-id="acb8f-184">c.</span></span> <span data-ttu-id="acb8f-185">Dans la zone de texte **Issuer**, collez la valeur de **ID d’entité SAML** que vous avez copiée depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="acb8f-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="acb8f-186">d.</span><span class="sxs-lookup"><span data-stu-id="acb8f-186">d.</span></span> <span data-ttu-id="acb8f-187">Dans la zone de texte **Authn Request URL**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="acb8f-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="acb8f-188">e.</span><span class="sxs-lookup"><span data-stu-id="acb8f-188">e.</span></span> <span data-ttu-id="acb8f-189">Ouvrez votre certificat codé en base 64 dans le bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="acb8f-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="acb8f-190">f.</span><span class="sxs-lookup"><span data-stu-id="acb8f-190">f.</span></span> <span data-ttu-id="acb8f-191">Dans **Email Attribute**, sélectionnez **Use SAML subject**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="acb8f-192">g.</span><span class="sxs-lookup"><span data-stu-id="acb8f-192">g.</span></span> <span data-ttu-id="acb8f-193">Sélectionnez **SP initiated Login Configuration**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="acb8f-194">h.</span><span class="sxs-lookup"><span data-stu-id="acb8f-194">h.</span></span> <span data-ttu-id="acb8f-195">Dans la zone de texte **Login Path** (Chemin d’accès de connexion), entrez **Azure**, puis cliquez sur **Save** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="acb8f-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="acb8f-196">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="acb8f-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="acb8f-197">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="acb8f-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="acb8f-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acb8f-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="acb8f-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="acb8f-200">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="acb8f-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="acb8f-202">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="acb8f-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="acb8f-203">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="acb8f-205">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="acb8f-207">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="acb8f-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="acb8f-209">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="acb8f-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="acb8f-211">a.</span><span class="sxs-lookup"><span data-stu-id="acb8f-211">a.</span></span> <span data-ttu-id="acb8f-212">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acb8f-213">b.</span><span class="sxs-lookup"><span data-stu-id="acb8f-213">b.</span></span> <span data-ttu-id="acb8f-214">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acb8f-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="acb8f-215">c.</span><span class="sxs-lookup"><span data-stu-id="acb8f-215">c.</span></span> <span data-ttu-id="acb8f-216">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="acb8f-217">d.</span><span class="sxs-lookup"><span data-stu-id="acb8f-217">d.</span></span> <span data-ttu-id="acb8f-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="acb8f-219">Création d’un utilisateur de test SumoLogic</span><span class="sxs-lookup"><span data-stu-id="acb8f-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="acb8f-220">Pour se connecter à SumoLogic, les utilisateurs d’Azure AD doivent être approvisionnés dans SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="acb8f-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="acb8f-221">Dans le cas de SumoLogic, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="acb8f-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="acb8f-222">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="acb8f-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="acb8f-223">Connectez-vous à votre locataire **SumoLogic** .</span><span class="sxs-lookup"><span data-stu-id="acb8f-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="acb8f-224">Accédez à **Gérer \> Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="acb8f-225">![Utilisateurs](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="acb8f-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="acb8f-226">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-226">Click **Add**.</span></span>
   
    <span data-ttu-id="acb8f-227">![Utilisateurs](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="acb8f-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="acb8f-228">Dans la boîte de dialogue **New User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="acb8f-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="acb8f-229">![Nouvel utilisateur](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="acb8f-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="acb8f-230">a.</span><span class="sxs-lookup"><span data-stu-id="acb8f-230">a.</span></span> <span data-ttu-id="acb8f-231">Indiquez dans les zones de texte **First Name**, **Last Name** et **Email** le prénom, le nom et l’adresse e-mail du compte Azure AD valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="acb8f-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="acb8f-232">b.</span><span class="sxs-lookup"><span data-stu-id="acb8f-232">b.</span></span> <span data-ttu-id="acb8f-233">Sélectionnez un rôle</span><span class="sxs-lookup"><span data-stu-id="acb8f-233">Select a role.</span></span>
  
    <span data-ttu-id="acb8f-234">c.</span><span class="sxs-lookup"><span data-stu-id="acb8f-234">c.</span></span> <span data-ttu-id="acb8f-235">Pour **Status (Statut)**, sélectionnez **Active (Actif)**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="acb8f-236">d.</span><span class="sxs-lookup"><span data-stu-id="acb8f-236">d.</span></span> <span data-ttu-id="acb8f-237">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="acb8f-238">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par SumoLogic, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="acb8f-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="acb8f-239">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="acb8f-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="acb8f-240">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="acb8f-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="acb8f-242">**Pour affecter Britta Simon à SumoLogic, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="acb8f-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="acb8f-243">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="acb8f-245">Dans la liste des applications, sélectionnez **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-245">In the applications list, select **SumoLogic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="acb8f-247">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="acb8f-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-249">Click **Add** button.</span></span> <span data-ttu-id="acb8f-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="acb8f-252">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="acb8f-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="acb8f-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acb8f-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="acb8f-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="acb8f-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="acb8f-255">Testing single sign-on</span></span>

<span data-ttu-id="acb8f-256">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="acb8f-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="acb8f-257">Quand vous cliquez sur la vignette SumoLogic dans le panneau d’accès, vous devez être connecté automatiquement à votre application SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="acb8f-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="acb8f-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="acb8f-258">Additional resources</span></span>

* [<span data-ttu-id="acb8f-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acb8f-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acb8f-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="acb8f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

