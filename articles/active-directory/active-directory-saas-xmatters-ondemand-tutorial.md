---
title: "Didacticiel : Intégration d’Azure Active Directory à XMatters OnDemand | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="1941c-103">Didacticiel : Intégration d’Azure Active Directory à xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="1941c-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="1941c-104">Dans ce didacticiel, vous allez découvrir comment intégrer xMatters OnDemand à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1941c-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1941c-105">L’intégration de xMatters OnDemand à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1941c-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1941c-106">Dans Azure AD, vous pouvez contrôler qui a accès à xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="1941c-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="1941c-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à xMatters OnDemand (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1941c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1941c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1941c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1941c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1941c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1941c-110">Prerequisites</span></span>

<span data-ttu-id="1941c-111">Pour configurer l’intégration d’Azure AD à xMatters OnDemand, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1941c-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="1941c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1941c-113">Un abonnement xMatters OnDemand pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1941c-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1941c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1941c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1941c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1941c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1941c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1941c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1941c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1941c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1941c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1941c-118">Scenario description</span></span>
<span data-ttu-id="1941c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1941c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1941c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1941c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1941c-121">Ajout de xMatters OnDemand à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1941c-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="1941c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="1941c-123">Ajout de xMatters OnDemand à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1941c-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="1941c-124">Pour configurer l’intégration de xMatters OnDemand à Azure AD, vous devez ajouter xMatters OnDemand disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1941c-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1941c-125">**Pour ajouter xMatters OnDemand à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="1941c-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1941c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1941c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1941c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1941c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1941c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1941c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1941c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1941c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1941c-133">Dans la zone de recherche, tapez **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="1941c-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="1941c-135">Dans le volet de résultats, sélectionnez **xMatters OnDemand**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1941c-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1941c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1941c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec xMatters OnDemand avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1941c-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1941c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur xMatters OnDemand équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1941c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="1941c-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur xMatters OnDemand associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1941c-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="1941c-141">Dans xMatters OnDemand, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1941c-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1941c-142">Pour configurer et tester l’authentification unique Azure AD avec xMatters OnDemand, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1941c-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1941c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1941c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1941c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1941c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1941c-145">**[Création d’un utilisateur de test xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)** pour avoir un équivalent de Britta Simon dans xMatters OnDemand lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1941c-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1941c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1941c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1941c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1941c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1941c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1941c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1941c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="1941c-150">**Pour configurer l’authentification unique Azure AD avec xMatters OnDemand, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="1941c-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="1941c-151">Dans le portail Azure, dans la page d’intégration de l’application **xMatters OnDemand**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1941c-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1941c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1941c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="1941c-155">Dans la section **Domaine et URL xMatters OnDemand**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1941c-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="1941c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1941c-157">a.</span></span> <span data-ttu-id="1941c-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="1941c-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="1941c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1941c-159">b.</span></span> <span data-ttu-id="1941c-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="1941c-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="1941c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1941c-161">These values are not real.</span></span> <span data-ttu-id="1941c-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="1941c-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1941c-163">Pour obtenir ces valeurs, contactez l’[l’équipe de support technique de xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="1941c-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="1941c-164">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (Base64)**, puis enregistrez le fichier du certificat localement en tant que **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="1941c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="1941c-166">Vous devez transférer le certificat à l’[équipe de support technique de xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="1941c-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="1941c-167">L’équipe du support technique xMatters doit charger le certificat avant que vous ne puissiez finaliser la configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1941c-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="1941c-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1941c-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1941c-170">Dans la section **Configuration de xMatters OnDemand**, cliquez sur **Configurer xMatters OnDemand** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1941c-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1941c-171">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1941c-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="1941c-173">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise XMatters OnDemand en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1941c-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="1941c-174">Dans la barre d’outils de la partie supérieure, cliquez sur **Admin**, puis sur **Company Details** dans la barre de navigation située à gauche.</span><span class="sxs-lookup"><span data-stu-id="1941c-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="1941c-175">![Administrateur](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="1941c-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="1941c-176">Dans la page **SAML Configuration** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1941c-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="1941c-177">![Configuration SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="1941c-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="1941c-178">a.</span><span class="sxs-lookup"><span data-stu-id="1941c-178">a.</span></span> <span data-ttu-id="1941c-179">Sélectionnez **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="1941c-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="1941c-180">b.</span><span class="sxs-lookup"><span data-stu-id="1941c-180">b.</span></span> <span data-ttu-id="1941c-181">Dans la zone de texte **Identity Provider ID**, collez l’**ID d’entité SAML** que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1941c-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="1941c-182">c.</span><span class="sxs-lookup"><span data-stu-id="1941c-182">c.</span></span> <span data-ttu-id="1941c-183">Dans la zone de texte **Single Sign On URL**, collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1941c-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="1941c-184">d.</span><span class="sxs-lookup"><span data-stu-id="1941c-184">d.</span></span> <span data-ttu-id="1941c-185">Dans la zone de texte **Single Logout URL**, collez l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1941c-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="1941c-186">e.</span><span class="sxs-lookup"><span data-stu-id="1941c-186">e.</span></span> <span data-ttu-id="1941c-187">Dans la partie supérieure de la page Company Details, cliquez sur **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="1941c-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="1941c-188">![Détails sur la société](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Détails sur la société")</span><span class="sxs-lookup"><span data-stu-id="1941c-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="1941c-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1941c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1941c-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1941c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1941c-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1941c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1941c-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1941c-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1941c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1941c-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1941c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1941c-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1941c-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1941c-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1941c-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1941c-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1941c-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1941c-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1941c-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1941c-204">a.</span><span class="sxs-lookup"><span data-stu-id="1941c-204">a.</span></span> <span data-ttu-id="1941c-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1941c-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1941c-206">b.</span><span class="sxs-lookup"><span data-stu-id="1941c-206">b.</span></span> <span data-ttu-id="1941c-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1941c-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1941c-208">c.</span><span class="sxs-lookup"><span data-stu-id="1941c-208">c.</span></span> <span data-ttu-id="1941c-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1941c-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1941c-210">d.</span><span class="sxs-lookup"><span data-stu-id="1941c-210">d.</span></span> <span data-ttu-id="1941c-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1941c-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="1941c-212">Création d’un utilisateur de test xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="1941c-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="1941c-213">Pour pouvoir se connecter à XMatters OnDemand, les utilisateurs d’Azure AD doivent être approvisionnés dans XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1941c-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="1941c-214">Dans le cas de XMatters OnDemand, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="1941c-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="1941c-215">Pour approvisionner un compte d’utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1941c-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="1941c-216">Connectez-vous à votre client **xMatters OnDemand** .</span><span class="sxs-lookup"><span data-stu-id="1941c-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="1941c-217">Cliquez sur l’onglet **Users**,</span><span class="sxs-lookup"><span data-stu-id="1941c-217">Click **Users** tab.</span></span> <span data-ttu-id="1941c-218">puis cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1941c-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="1941c-219">![Utilisateurs](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="1941c-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="1941c-220">Dans la section **Add a User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1941c-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1941c-221">![Ajouter un utilisateur](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="1941c-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="1941c-222">a.</span><span class="sxs-lookup"><span data-stu-id="1941c-222">a.</span></span> <span data-ttu-id="1941c-223">Sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="1941c-223">Select **Active**.</span></span>

    <span data-ttu-id="1941c-224">b.</span><span class="sxs-lookup"><span data-stu-id="1941c-224">b.</span></span> <span data-ttu-id="1941c-225">Dans la zone de texte **User ID**, entrez l’identifiant d’un utilisateur, par exemple Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1941c-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="1941c-226">c.</span><span class="sxs-lookup"><span data-stu-id="1941c-226">c.</span></span> <span data-ttu-id="1941c-227">Dans la zone de texte **First Name**, entrez le prénom de l’utilisateur, par exemple Britta.</span><span class="sxs-lookup"><span data-stu-id="1941c-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="1941c-228">d.</span><span class="sxs-lookup"><span data-stu-id="1941c-228">d.</span></span> <span data-ttu-id="1941c-229">Dans la zone de texte **Last Name**, entrez le nom de l’utilisateur, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="1941c-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="1941c-230">e.</span><span class="sxs-lookup"><span data-stu-id="1941c-230">e.</span></span> <span data-ttu-id="1941c-231">Dans la zone de texte **Site**, entrez le site valide d’un compte Azure AD valide que vous voulez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="1941c-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="1941c-232">f.</span><span class="sxs-lookup"><span data-stu-id="1941c-232">f.</span></span> <span data-ttu-id="1941c-233">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1941c-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1941c-234">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1941c-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1941c-235">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1941c-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1941c-237">**Pour affecter Britta Simon à xMatters OnDemand, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="1941c-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="1941c-238">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1941c-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1941c-240">Dans la liste des applications, sélectionnez **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="1941c-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="1941c-242">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1941c-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1941c-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1941c-244">Click **Add** button.</span></span> <span data-ttu-id="1941c-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1941c-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1941c-247">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1941c-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1941c-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1941c-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1941c-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1941c-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1941c-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1941c-250">Testing single sign-on</span></span>

<span data-ttu-id="1941c-251">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1941c-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1941c-252">Quand vous cliquez sur la vignette xMatters OnDemand dans le volet d’accès, vous devez être connecté automatiquement à votre application xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1941c-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="1941c-253">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1941c-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1941c-254">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1941c-254">Additional resources</span></span>

* [<span data-ttu-id="1941c-255">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1941c-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1941c-256">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1941c-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

