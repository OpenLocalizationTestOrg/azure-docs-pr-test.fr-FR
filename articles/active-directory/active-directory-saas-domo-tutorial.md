---
title: "Didacticiel : Intégration d’Azure Active Directory avec Domo | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 919d2262cf9f14159a13370037301005b5b69da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="3da73-103">Didacticiel : intégration d’Azure Active Directory à Domo</span><span class="sxs-lookup"><span data-stu-id="3da73-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="3da73-104">Dans ce didacticiel, vous allez apprendre à intégrer Domo à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3da73-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3da73-105">L’intégration de Domo dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3da73-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3da73-106">Dans Azure AD, vous pouvez contrôler qui a accès à Domo</span><span class="sxs-lookup"><span data-stu-id="3da73-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="3da73-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Domo (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3da73-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3da73-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3da73-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3da73-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3da73-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3da73-110">Prerequisites</span></span>

<span data-ttu-id="3da73-111">Pour configurer l’intégration d’Azure AD avec Domo, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3da73-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="3da73-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3da73-113">Un abonnement Domo pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3da73-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3da73-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3da73-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3da73-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3da73-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3da73-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3da73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3da73-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3da73-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3da73-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3da73-118">Scenario description</span></span>
<span data-ttu-id="3da73-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3da73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3da73-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="3da73-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3da73-121">Ajout de Domo depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="3da73-121">Adding Domo from the gallery</span></span>
2. <span data-ttu-id="3da73-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="3da73-123">Ajout de Domo depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="3da73-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="3da73-124">Pour configurer l’intégration de Domo avec Azure AD, vous devez ajouter Domo, à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3da73-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3da73-125">**Pour ajouter Domo à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3da73-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3da73-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3da73-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3da73-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3da73-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3da73-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3da73-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3da73-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3da73-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3da73-133">Dans la zone de recherche, tapez **Domo**.</span><span class="sxs-lookup"><span data-stu-id="3da73-133">In the search box, type **Domo**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="3da73-135">Dans le volet de résultats, sélectionnez **Domo**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3da73-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3da73-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3da73-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Domo, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3da73-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3da73-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Domo correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3da73-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="3da73-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Domo associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="3da73-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="3da73-141">Dans Domo, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="3da73-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3da73-142">Pour configurer et tester l’authentification unique Azure AD avec Domo, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="3da73-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3da73-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3da73-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3da73-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3da73-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3da73-145">**[Création d’un utilisateur de test Domo](#creating-a-domo-test-user)** pour avoir un équivalent de Britta Simon dans Domo lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="3da73-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3da73-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3da73-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3da73-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3da73-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3da73-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3da73-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Domo.</span><span class="sxs-lookup"><span data-stu-id="3da73-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="3da73-150">**Pour configurer l’authentification unique Azure AD avec Domo, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3da73-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="3da73-151">Dans le portail Azure, sur la page d’intégration de l’application **Domo**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3da73-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3da73-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3da73-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="3da73-155">Dans la section **Domaine et URL Domo**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3da73-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="3da73-157">a.</span><span class="sxs-lookup"><span data-stu-id="3da73-157">a.</span></span> <span data-ttu-id="3da73-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="3da73-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="3da73-159">b.</span><span class="sxs-lookup"><span data-stu-id="3da73-159">b.</span></span> <span data-ttu-id="3da73-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3da73-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="3da73-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3da73-161">These values are not real.</span></span> <span data-ttu-id="3da73-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="3da73-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3da73-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="3da73-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

4. <span data-ttu-id="3da73-164">L’application Domo attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="3da73-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3da73-165">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="3da73-165">Configure the following claims for this application.</span></span> <span data-ttu-id="3da73-166">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="3da73-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3da73-167">La capture d’écran suivante montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="3da73-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="3da73-169">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3da73-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3da73-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="3da73-170">Attribute Name</span></span> | <span data-ttu-id="3da73-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="3da73-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="3da73-172">name</span><span class="sxs-lookup"><span data-stu-id="3da73-172">name</span></span> | <span data-ttu-id="3da73-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="3da73-173">user.displayname</span></span> |
    | <span data-ttu-id="3da73-174">email</span><span class="sxs-lookup"><span data-stu-id="3da73-174">email</span></span> | <span data-ttu-id="3da73-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="3da73-175">user.mail</span></span> |
    
    <span data-ttu-id="3da73-176">a.</span><span class="sxs-lookup"><span data-stu-id="3da73-176">a.</span></span> <span data-ttu-id="3da73-177">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="3da73-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3da73-180">b.</span><span class="sxs-lookup"><span data-stu-id="3da73-180">b.</span></span> <span data-ttu-id="3da73-181">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="3da73-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="3da73-182">c.</span><span class="sxs-lookup"><span data-stu-id="3da73-182">c.</span></span> <span data-ttu-id="3da73-183">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="3da73-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3da73-184">d.</span><span class="sxs-lookup"><span data-stu-id="3da73-184">d.</span></span> <span data-ttu-id="3da73-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3da73-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="3da73-186">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3da73-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="3da73-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3da73-188">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="3da73-190">Dans la section **Configuration de Domo**, cliquez sur **Configurer Domo** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="3da73-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3da73-191">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="3da73-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="3da73-193">Pour configurer l’authentification unique côté **Domo**, vous devez envoyer le **Certificat** téléchargé, **l’ID d’entité SAML**, **l’URL du service d’authentification unique SAML** et **l’URL de déconnexion** à [l’équipe de support de Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="3da73-193">To configure single sign-on on **Domo** side, you need to send the downloaded **Certificate**, **SAML Entity ID**, the **SAML Single Sign-On Service URL** and the **Sign-Out URL** to [Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="3da73-194">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="3da73-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3da73-195">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="3da73-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3da73-196">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="3da73-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3da73-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3da73-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3da73-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="3da73-199">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3da73-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3da73-201">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3da73-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3da73-202">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3da73-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3da73-204">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3da73-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3da73-206">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3da73-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3da73-208">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3da73-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3da73-210">a.</span><span class="sxs-lookup"><span data-stu-id="3da73-210">a.</span></span> <span data-ttu-id="3da73-211">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3da73-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3da73-212">b.</span><span class="sxs-lookup"><span data-stu-id="3da73-212">b.</span></span> <span data-ttu-id="3da73-213">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3da73-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3da73-214">c.</span><span class="sxs-lookup"><span data-stu-id="3da73-214">c.</span></span> <span data-ttu-id="3da73-215">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3da73-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3da73-216">d.</span><span class="sxs-lookup"><span data-stu-id="3da73-216">d.</span></span> <span data-ttu-id="3da73-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3da73-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="3da73-218">Création d’un utilisateur de test Domo</span><span class="sxs-lookup"><span data-stu-id="3da73-218">Creating a Domo test user</span></span>

<span data-ttu-id="3da73-219">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Domo.</span><span class="sxs-lookup"><span data-stu-id="3da73-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="3da73-220">Domo prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="3da73-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="3da73-221">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="3da73-221">There is no action item for you in this section.</span></span> <span data-ttu-id="3da73-222">Un utilisateur est créé lors d’une tentative d’accès à Domo s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="3da73-222">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3da73-223">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da73-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3da73-224">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Domo.</span><span class="sxs-lookup"><span data-stu-id="3da73-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3da73-226">**Pour affecter Britta Simon à Domo, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3da73-226">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="3da73-227">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3da73-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3da73-229">Dans la liste des applications, sélectionnez **Domo**.</span><span class="sxs-lookup"><span data-stu-id="3da73-229">In the applications list, select **Domo**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="3da73-231">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3da73-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3da73-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3da73-233">Click **Add** button.</span></span> <span data-ttu-id="3da73-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3da73-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3da73-236">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3da73-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3da73-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3da73-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3da73-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3da73-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3da73-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3da73-239">Testing single sign-on</span></span>

<span data-ttu-id="3da73-240">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3da73-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="3da73-241">Lorsque vous cliquez sur la mosaïque Domo dans le volet d’accès, vous devez être connecté automatiquement à votre application Domo.</span><span class="sxs-lookup"><span data-stu-id="3da73-241">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="3da73-242">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3da73-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3da73-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3da73-243">Additional resources</span></span>

* [<span data-ttu-id="3da73-244">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3da73-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3da73-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3da73-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

