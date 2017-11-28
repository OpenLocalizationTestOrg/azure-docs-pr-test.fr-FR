---
title: "Didacticiel : Intégration d'Azure Active Directory à Workpath | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="bfc05-103">Didacticiel : Intégration d’Azure Active Directory à Workpath | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="bfc05-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="bfc05-104">Dans ce didacticiel, vous allez apprendre à intégrer Workpath à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfc05-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfc05-105">L’intégration de Workpath dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bfc05-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bfc05-106">Dans Azure AD, vous pouvez contrôler qui a accès à Workpath</span><span class="sxs-lookup"><span data-stu-id="bfc05-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="bfc05-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Workpath (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfc05-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="bfc05-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bfc05-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfc05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfc05-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bfc05-110">Prerequisites</span></span>

<span data-ttu-id="bfc05-111">Pour configurer l’intégration d’Azure AD avec Workpath, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bfc05-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="bfc05-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfc05-113">Un abonnement Workpath pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bfc05-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfc05-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bfc05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfc05-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bfc05-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfc05-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bfc05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfc05-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfc05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfc05-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bfc05-118">Scenario description</span></span>
<span data-ttu-id="bfc05-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bfc05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfc05-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="bfc05-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfc05-121">Ajout de Workpath à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="bfc05-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="bfc05-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="bfc05-123">Ajout de Workpath à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="bfc05-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="bfc05-124">Pour configurer l’intégration de Workpath à Azure AD, vous devez ajouter Workpath à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bfc05-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bfc05-125">**Pour ajouter Workpath à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bfc05-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc05-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfc05-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bfc05-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bfc05-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bfc05-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bfc05-133">Dans la zone de recherche, tapez **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-133">In the search box, type **Workpath**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="bfc05-135">Dans le panneau des résultats, sélectionnez **Workpath**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="bfc05-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfc05-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfc05-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workpath, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bfc05-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfc05-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Workpath correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfc05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="bfc05-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Workpath associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="bfc05-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="bfc05-141">Dans Workpath, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="bfc05-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bfc05-142">Pour configurer et tester l’authentification unique Azure AD avec Workpath, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="bfc05-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bfc05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bfc05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bfc05-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfc05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfc05-145">**[Création d’un utilisateur de test Workpath](#creating-a-workpath-test-user)** pour avoir un équivalent de Britta Simon dans Workpath lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bfc05-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfc05-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfc05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfc05-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="bfc05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfc05-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfc05-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Workpath.</span><span class="sxs-lookup"><span data-stu-id="bfc05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="bfc05-150">**Pour configurer l’authentification unique Azure AD avec Workpath, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bfc05-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc05-151">Dans le portail Azure, sur la page d’intégration de l’application **Workpath**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bfc05-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bfc05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="bfc05-155">Dans la section **Domaines et URL Workpath**, si vous souhaitez configurer l’application en Mode initié par **IDP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bfc05-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="bfc05-157">a.</span><span class="sxs-lookup"><span data-stu-id="bfc05-157">a.</span></span> <span data-ttu-id="bfc05-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="bfc05-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="bfc05-159">b.</span><span class="sxs-lookup"><span data-stu-id="bfc05-159">b.</span></span> <span data-ttu-id="bfc05-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="bfc05-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="bfc05-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="bfc05-162">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bfc05-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="bfc05-164">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="bfc05-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bfc05-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="bfc05-165">These values are not real.</span></span> <span data-ttu-id="bfc05-166">Mettez à jour ces valeurs avec l’URL de réponse, l’identificateur et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="bfc05-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="bfc05-167">Pour obtenir ces valeurs, contactez [l’équipe de support technique Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="bfc05-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="bfc05-168">L’application Workpath attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="bfc05-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bfc05-169">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="bfc05-169">Configure the following claims for this application.</span></span> <span data-ttu-id="bfc05-170">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="bfc05-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="bfc05-171">La capture d’écran suivante montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="bfc05-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="bfc05-173">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bfc05-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="bfc05-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="bfc05-174">Attribute Name</span></span> | <span data-ttu-id="bfc05-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="bfc05-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="bfc05-176">first_name</span><span class="sxs-lookup"><span data-stu-id="bfc05-176">first_name</span></span> | <span data-ttu-id="bfc05-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="bfc05-177">user.givenname</span></span> |
    | <span data-ttu-id="bfc05-178">last_name</span><span class="sxs-lookup"><span data-stu-id="bfc05-178">last_name</span></span> | <span data-ttu-id="bfc05-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="bfc05-179">user.surname</span></span> |
    
    <span data-ttu-id="bfc05-180">a.</span><span class="sxs-lookup"><span data-stu-id="bfc05-180">a.</span></span> <span data-ttu-id="bfc05-181">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="bfc05-183">b.</span><span class="sxs-lookup"><span data-stu-id="bfc05-183">b.</span></span> <span data-ttu-id="bfc05-184">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="bfc05-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bfc05-186">c.</span><span class="sxs-lookup"><span data-stu-id="bfc05-186">c.</span></span> <span data-ttu-id="bfc05-187">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="bfc05-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="bfc05-188">d.</span><span class="sxs-lookup"><span data-stu-id="bfc05-188">d.</span></span> <span data-ttu-id="bfc05-189">Laissez la zone de texte **Espace de noms** vide.</span><span class="sxs-lookup"><span data-stu-id="bfc05-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="bfc05-190">e.</span><span class="sxs-lookup"><span data-stu-id="bfc05-190">e.</span></span> <span data-ttu-id="bfc05-191">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="bfc05-192">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bfc05-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="bfc05-194">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bfc05-194">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="bfc05-196">Dans la section **Configuration de Workpath**, cliquez sur **Configurer Workpath** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bfc05-197">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bfc05-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="bfc05-199">Pour configurer l’authentification unique côté **Workpath**, vous devez envoyer le **XML de métadonnées**, **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** téléchargés à [l’équipe de support Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="bfc05-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="bfc05-200">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="bfc05-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bfc05-201">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="bfc05-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bfc05-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfc05-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfc05-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfc05-204">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bfc05-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bfc05-206">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bfc05-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc05-207">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfc05-209">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfc05-211">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bfc05-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfc05-213">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bfc05-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfc05-215">a.</span><span class="sxs-lookup"><span data-stu-id="bfc05-215">a.</span></span> <span data-ttu-id="bfc05-216">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfc05-217">b.</span><span class="sxs-lookup"><span data-stu-id="bfc05-217">b.</span></span> <span data-ttu-id="bfc05-218">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfc05-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfc05-219">c.</span><span class="sxs-lookup"><span data-stu-id="bfc05-219">c.</span></span> <span data-ttu-id="bfc05-220">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bfc05-221">d.</span><span class="sxs-lookup"><span data-stu-id="bfc05-221">d.</span></span> <span data-ttu-id="bfc05-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="bfc05-223">Création d’un utilisateur de test Workpath</span><span class="sxs-lookup"><span data-stu-id="bfc05-223">Creating a Workpath test user</span></span>

<span data-ttu-id="bfc05-224">Workpath prend en charge l’approvisionnement juste-à-temps des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bfc05-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="bfc05-225">Une fois identifiés, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="bfc05-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bfc05-226">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc05-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bfc05-227">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Workpath.</span><span class="sxs-lookup"><span data-stu-id="bfc05-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bfc05-229">**Pour assigner Britta Simon à Workpath, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bfc05-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc05-230">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bfc05-232">Dans la liste des applications, sélectionnez **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-232">In the applications list, select **Workpath**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="bfc05-234">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bfc05-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-236">Click **Add** button.</span></span> <span data-ttu-id="bfc05-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bfc05-239">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bfc05-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bfc05-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfc05-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfc05-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bfc05-242">Testing single sign-on</span></span>

<span data-ttu-id="bfc05-243">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="bfc05-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bfc05-244">Quand vous cliquez sur la vignette Workpath dans le volet d’accès, vous devez être connecté automatiquement à votre application Workpath.</span><span class="sxs-lookup"><span data-stu-id="bfc05-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="bfc05-245">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bfc05-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bfc05-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bfc05-246">Additional resources</span></span>

* [<span data-ttu-id="bfc05-247">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfc05-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfc05-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bfc05-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

