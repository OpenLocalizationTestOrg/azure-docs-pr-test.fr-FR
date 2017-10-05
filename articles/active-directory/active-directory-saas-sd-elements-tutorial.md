---
title: "Didacticiel : Intégration d’Azure Active Directory à SD Elements | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SD Elements."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="11f67-103">Didacticiel : Intégration d’Azure Active Directory à SD Elements</span><span class="sxs-lookup"><span data-stu-id="11f67-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="11f67-104">Dans ce didacticiel, vous allez apprendre à intégrer SD Elements avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11f67-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11f67-105">L’intégration de SD Elements à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="11f67-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11f67-106">Dans Azure AD, vous pouvez contrôler qui a accès à SD Elements.</span><span class="sxs-lookup"><span data-stu-id="11f67-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="11f67-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à SD Elements (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11f67-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11f67-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="11f67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="11f67-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11f67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11f67-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="11f67-110">Prerequisites</span></span>

<span data-ttu-id="11f67-111">Pour configurer l’intégration d’Azure AD avec SD Elements, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="11f67-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="11f67-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="11f67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11f67-113">Un abonnement SD Elements pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="11f67-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11f67-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="11f67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11f67-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="11f67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11f67-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="11f67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11f67-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11f67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11f67-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="11f67-118">Scenario description</span></span>
<span data-ttu-id="11f67-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="11f67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11f67-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="11f67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11f67-121">Ajout de SD Elements à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="11f67-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="11f67-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="11f67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="11f67-123">Ajout de SD Elements à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="11f67-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="11f67-124">Pour configurer l’intégration de SD Elements avec Azure AD, vous devez ajouter SD Elements disponible dans la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="11f67-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11f67-125">**Pour ajouter SD Elements à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11f67-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11f67-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11f67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11f67-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="11f67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11f67-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="11f67-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="11f67-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="11f67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="11f67-133">Dans la zone de recherche, tapez **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="11f67-133">In the search box, type **SD Elements**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="11f67-135">Dans le panneau de résultats, sélectionnez **SD Elements**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="11f67-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11f67-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="11f67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11f67-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SD Elements sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="11f67-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11f67-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SD Elements équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11f67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="11f67-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur SD Elements associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="11f67-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="11f67-141">Dans SD Elements, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="11f67-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11f67-142">Pour configurer et tester l’authentification unique Azure AD avec SD Elements, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="11f67-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11f67-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="11f67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11f67-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11f67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11f67-145">**[Création d'un utilisateur de test SD Elements](#creating-a-sd-elements-test-user)** pour avoir un équivalent de Britta Simon dans SD Elements lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="11f67-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="11f67-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11f67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11f67-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="11f67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11f67-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="11f67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11f67-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SD Elements.</span><span class="sxs-lookup"><span data-stu-id="11f67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="11f67-150">**Pour configurer l’authentification unique Azure AD avec SD Elements, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11f67-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="11f67-151">Dans le portail Azure, sur la page d’intégration de l’application **SD Elements**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="11f67-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="11f67-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="11f67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="11f67-155">Dans la section **Domaine et URL SD Elements**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="11f67-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="11f67-157">a.</span><span class="sxs-lookup"><span data-stu-id="11f67-157">a.</span></span> <span data-ttu-id="11f67-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="11f67-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="11f67-159">b.</span><span class="sxs-lookup"><span data-stu-id="11f67-159">b.</span></span> <span data-ttu-id="11f67-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="11f67-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11f67-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="11f67-161">These values are not real.</span></span> <span data-ttu-id="11f67-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="11f67-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="11f67-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique SD Elements](mailto:support@sdelements.com).</span><span class="sxs-lookup"><span data-stu-id="11f67-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="11f67-164">L’application SD Elements attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="11f67-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="11f67-165">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="11f67-165">Configure the following claims for this application.</span></span> <span data-ttu-id="11f67-166">Vous pouvez gérer les valeurs de ces attributs à partir de l’onglet **Attributs utilisateur** de l’application.</span><span class="sxs-lookup"><span data-stu-id="11f67-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="11f67-167">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="11f67-167">The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="11f67-169">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="11f67-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="11f67-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="11f67-170">Attribute Name</span></span> | <span data-ttu-id="11f67-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="11f67-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="11f67-172">email</span><span class="sxs-lookup"><span data-stu-id="11f67-172">email</span></span> |<span data-ttu-id="11f67-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="11f67-173">user.mail</span></span> |
    | <span data-ttu-id="11f67-174">firstname</span><span class="sxs-lookup"><span data-stu-id="11f67-174">firstname</span></span> |<span data-ttu-id="11f67-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="11f67-175">user.givenname</span></span> |
    | <span data-ttu-id="11f67-176">lastname</span><span class="sxs-lookup"><span data-stu-id="11f67-176">lastname</span></span> |<span data-ttu-id="11f67-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="11f67-177">user.surname</span></span> |

    <span data-ttu-id="11f67-178">a.</span><span class="sxs-lookup"><span data-stu-id="11f67-178">a.</span></span> <span data-ttu-id="11f67-179">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="11f67-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="11f67-182">b.</span><span class="sxs-lookup"><span data-stu-id="11f67-182">b.</span></span> <span data-ttu-id="11f67-183">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="11f67-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="11f67-184">c.</span><span class="sxs-lookup"><span data-stu-id="11f67-184">c.</span></span> <span data-ttu-id="11f67-185">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="11f67-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="11f67-186">d.</span><span class="sxs-lookup"><span data-stu-id="11f67-186">d.</span></span> <span data-ttu-id="11f67-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="11f67-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="11f67-188">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="11f67-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="11f67-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="11f67-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="11f67-192">Dans la section **Configuration de SD Elements** , cliquez sur **Configurer SD Elements** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="11f67-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="11f67-193">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="11f67-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="11f67-195">Pour activer l'authentification unique, contactez votre [équipe de support technique SD Elements](mailto:support@sdelements.com) et fournissez-leur le fichier de certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="11f67-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="11f67-196">Dans une autre fenêtre de navigateur, authentifiez-vous auprès de votre client SD Elements en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="11f67-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="11f67-197">Dans le menu du haut, cliquez sur **Système**, puis sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="11f67-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="11f67-199">Dans la boîte de dialogue **Paramètres d’authentification unique** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="11f67-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="11f67-201">a.</span><span class="sxs-lookup"><span data-stu-id="11f67-201">a.</span></span> <span data-ttu-id="11f67-202">Pour **SSO Type**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="11f67-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="11f67-203">b.</span><span class="sxs-lookup"><span data-stu-id="11f67-203">b.</span></span> <span data-ttu-id="11f67-204">Dans la zone de texte **Identity Provider Entity ID** (ID d’entité du fournisseur d'identité), collez la valeur de l’**ID d’entité SAML** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="11f67-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="11f67-205">c.</span><span class="sxs-lookup"><span data-stu-id="11f67-205">c.</span></span> <span data-ttu-id="11f67-206">Dans la zone de texte **Identity Provider Single Sign-On Service** (Service d’authentification unique du fournisseur d’identité), collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="11f67-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="11f67-207">d.</span><span class="sxs-lookup"><span data-stu-id="11f67-207">d.</span></span> <span data-ttu-id="11f67-208">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="11f67-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="11f67-209">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="11f67-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11f67-210">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="11f67-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11f67-211">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11f67-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11f67-212">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="11f67-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="11f67-213">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="11f67-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="11f67-215">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11f67-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11f67-216">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11f67-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11f67-218">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="11f67-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11f67-220">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="11f67-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11f67-222">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="11f67-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11f67-224">a.</span><span class="sxs-lookup"><span data-stu-id="11f67-224">a.</span></span> <span data-ttu-id="11f67-225">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11f67-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11f67-226">b.</span><span class="sxs-lookup"><span data-stu-id="11f67-226">b.</span></span> <span data-ttu-id="11f67-227">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11f67-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11f67-228">c.</span><span class="sxs-lookup"><span data-stu-id="11f67-228">c.</span></span> <span data-ttu-id="11f67-229">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="11f67-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="11f67-230">d.</span><span class="sxs-lookup"><span data-stu-id="11f67-230">d.</span></span> <span data-ttu-id="11f67-231">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="11f67-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="11f67-232">Création d'un utilisateur de test SD Elements</span><span class="sxs-lookup"><span data-stu-id="11f67-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="11f67-233">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans SD Elements.</span><span class="sxs-lookup"><span data-stu-id="11f67-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="11f67-234">Dans le cas de SD Elements, la création d'utilisateurs SD Elements est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="11f67-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="11f67-235">**Pour créer un utilisateur appelé Britta Simon dans SD Elements, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11f67-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="11f67-236">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise SD Elements en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="11f67-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="11f67-237">Dans le menu situé en haut, cliquez sur **Gestion des utilisateurs**, puis sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="11f67-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Création d'un utilisateur de test SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="11f67-239">Cliquez sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="11f67-239">Click **Add New User**.</span></span>
   
    ![Création d'un utilisateur de test SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="11f67-241">Dans la boîte de dialogue **Ajouter un nouvel utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="11f67-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Création d'un utilisateur de test SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="11f67-243">a.</span><span class="sxs-lookup"><span data-stu-id="11f67-243">a.</span></span> <span data-ttu-id="11f67-244">Dans la zone de texte **E-mail**, entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="11f67-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="11f67-245">b.</span><span class="sxs-lookup"><span data-stu-id="11f67-245">b.</span></span> <span data-ttu-id="11f67-246">Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="11f67-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="11f67-247">c.</span><span class="sxs-lookup"><span data-stu-id="11f67-247">c.</span></span> <span data-ttu-id="11f67-248">Dans la zone de texte **Nom**, entrez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="11f67-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="11f67-249">d.</span><span class="sxs-lookup"><span data-stu-id="11f67-249">d.</span></span> <span data-ttu-id="11f67-250">Pour **Role**, sélectionnez **User**.</span><span class="sxs-lookup"><span data-stu-id="11f67-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="11f67-251">e.</span><span class="sxs-lookup"><span data-stu-id="11f67-251">e.</span></span> <span data-ttu-id="11f67-252">Cliquez sur **Créer l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="11f67-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="11f67-253">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="11f67-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="11f67-254">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SD Elements.</span><span class="sxs-lookup"><span data-stu-id="11f67-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="11f67-256">**Pour affecter Britta Simon à SD Elements, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11f67-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="11f67-257">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="11f67-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="11f67-259">Dans la liste des applications, sélectionnez **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="11f67-259">In the applications list, select **SD Elements**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="11f67-261">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="11f67-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="11f67-263">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="11f67-263">Click **Add** button.</span></span> <span data-ttu-id="11f67-264">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="11f67-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="11f67-266">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="11f67-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11f67-267">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="11f67-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11f67-268">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="11f67-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11f67-269">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="11f67-269">Testing single sign-on</span></span>

<span data-ttu-id="11f67-270">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="11f67-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="11f67-271">Lorsque vous cliquez sur la mosaïque SD Elements dans le volet d’accès, vous devez être connecté automatiquement à votre application SD Elements.</span><span class="sxs-lookup"><span data-stu-id="11f67-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11f67-272">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="11f67-272">Additional resources</span></span>

* [<span data-ttu-id="11f67-273">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11f67-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11f67-274">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="11f67-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

