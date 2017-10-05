---
title: "Didacticiel : Intégration d’Azure Active Directory avec OfficeSpace Software | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="d1c92-103">Didacticiel : Intégration d’Azure Active Directory avec OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="d1c92-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="d1c92-104">Dans ce didacticiel, vous allez apprendre à intégrer OfficeSpace Software à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1c92-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1c92-105">L’intégration d’OfficeSpace Software à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d1c92-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d1c92-106">Dans Azure AD, vous pouvez contrôler qui a accès à OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="d1c92-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="d1c92-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à OfficeSpace Software (authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c92-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d1c92-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c92-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d1c92-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1c92-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1c92-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d1c92-110">Prerequisites</span></span>

<span data-ttu-id="d1c92-111">Pour configurer l’intégration d’Azure AD avec OfficeSpace Software, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d1c92-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="d1c92-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1c92-113">Un abonnement OfficeSpace Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d1c92-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1c92-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d1c92-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1c92-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d1c92-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1c92-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d1c92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1c92-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1c92-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1c92-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d1c92-118">Scenario description</span></span>
<span data-ttu-id="d1c92-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d1c92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1c92-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d1c92-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1c92-121">Ajout d’OfficeSpace Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d1c92-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="d1c92-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="d1c92-123">Ajout d’OfficeSpace Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d1c92-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="d1c92-124">Pour configurer l’intégration d’OfficeSpace Software à Azure AD, vous devez ajouter OfficeSpace Software, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d1c92-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1c92-125">**Pour ajouter OfficeSpace Software à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d1c92-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c92-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="d1c92-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d1c92-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="d1c92-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d1c92-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="d1c92-133">Dans la zone de recherche, tapez **OfficeSpace Software**, sélectionnez **OfficeSpace Software** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d1c92-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![OfficeSpace Software dans la liste des résultats](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d1c92-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c92-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d1c92-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec OfficeSpace Software avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d1c92-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1c92-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur OfficeSpace Software équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c92-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="d1c92-138">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur OfficeSpace Software associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="d1c92-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="d1c92-139">Dans OfficeSpace Software, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d1c92-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d1c92-140">Pour configurer et tester l’authentification unique Azure AD avec OfficeSpace Software, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d1c92-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1c92-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d1c92-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1c92-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1c92-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1c92-143">**[Créer un utilisateur de test OfficeSpace Software](#create-a-officespace-software-test-user)** pour avoir un équivalent de Britta Simon dans OfficeSpace Software qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="d1c92-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1c92-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c92-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1c92-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d1c92-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d1c92-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c92-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d1c92-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="d1c92-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="d1c92-148">**Pour configurer l’authentification unique Azure AD avec OfficeSpace Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d1c92-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c92-149">Dans le portail Azure, sur la page d’intégration de l’application **OfficeSpace Software**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="d1c92-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d1c92-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="d1c92-153">Dans la section **Domaine et URL OfficeSpace Software**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d1c92-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="d1c92-155">a.</span><span class="sxs-lookup"><span data-stu-id="d1c92-155">a.</span></span> <span data-ttu-id="d1c92-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="d1c92-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="d1c92-157">b.</span><span class="sxs-lookup"><span data-stu-id="d1c92-157">b.</span></span> <span data-ttu-id="d1c92-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="d1c92-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d1c92-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d1c92-159">These values are not real.</span></span> <span data-ttu-id="d1c92-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="d1c92-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d1c92-161">Contactez [l’équipe de support technique d’OfficeSpace Software](mailto:support@officespacesoftware.com) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d1c92-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="d1c92-162">Votre application OfficeSpace Software attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="d1c92-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d1c92-163">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="d1c92-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="d1c92-164">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="d1c92-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="d1c92-165">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="d1c92-165">The following screenshot shows an example for this.</span></span>
    
    ![Configurer l’attribut](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="d1c92-167">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, sélectionnez **user.mail** en tant **qu’identificateur d’utilisateur**, et pour chaque ligne indiquée dans le tableau ci-dessous, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d1c92-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="d1c92-168">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="d1c92-168">Attribute Name</span></span> | <span data-ttu-id="d1c92-169">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="d1c92-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="d1c92-170">email</span><span class="sxs-lookup"><span data-stu-id="d1c92-170">email</span></span> | <span data-ttu-id="d1c92-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="d1c92-171">user.mail</span></span> |
    | <span data-ttu-id="d1c92-172">name</span><span class="sxs-lookup"><span data-stu-id="d1c92-172">name</span></span> | <span data-ttu-id="d1c92-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="d1c92-173">user.displayname</span></span> |
    | <span data-ttu-id="d1c92-174">first_name</span><span class="sxs-lookup"><span data-stu-id="d1c92-174">first_name</span></span> | <span data-ttu-id="d1c92-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d1c92-175">user.givenname</span></span> |
    | <span data-ttu-id="d1c92-176">last_name</span><span class="sxs-lookup"><span data-stu-id="d1c92-176">last_name</span></span> | <span data-ttu-id="d1c92-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="d1c92-177">user.surname</span></span> |

    <span data-ttu-id="d1c92-178">a.</span><span class="sxs-lookup"><span data-stu-id="d1c92-178">a.</span></span> <span data-ttu-id="d1c92-179">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="d1c92-180">Configurer l’ajout</span><span class="sxs-lookup"><span data-stu-id="d1c92-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configurer l’attribut](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d1c92-182">b.</span><span class="sxs-lookup"><span data-stu-id="d1c92-182">b.</span></span> <span data-ttu-id="d1c92-183">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d1c92-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d1c92-184">c.</span><span class="sxs-lookup"><span data-stu-id="d1c92-184">c.</span></span> <span data-ttu-id="d1c92-185">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d1c92-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d1c92-186">d.</span><span class="sxs-lookup"><span data-stu-id="d1c92-186">d.</span></span> <span data-ttu-id="d1c92-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="d1c92-188">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="d1c92-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="d1c92-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d1c92-190">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d1c92-192">Dans **Configuration de OfficeSpace Software**, cliquez sur **Configurer OfficeSpace Software** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d1c92-193">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration d’OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="d1c92-195">Dans une autre fenêtre de navigateur web, connectez-vous à votre locataire OfficeSpace Software en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d1c92-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="d1c92-196">Accédez à **Paramètres** et cliquez sur **Connecteurs**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-196">Go to **Settings** and click **Connectors**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="d1c92-198">Cliquez sur **Authentication SAML**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-198">Click **SAML Authentication**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="d1c92-200">Dans la section **SAML Authentication** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d1c92-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="d1c92-202">a.</span><span class="sxs-lookup"><span data-stu-id="d1c92-202">a.</span></span> <span data-ttu-id="d1c92-203">Dans la zone de texte **URL du fournisseur de déconnexion**, collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c92-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d1c92-204">b.</span><span class="sxs-lookup"><span data-stu-id="d1c92-204">b.</span></span> <span data-ttu-id="d1c92-205">Dans la zone de texte **URL cible du fournisseur d’identité client**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c92-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d1c92-206">c.</span><span class="sxs-lookup"><span data-stu-id="d1c92-206">c.</span></span> <span data-ttu-id="d1c92-207">Collez la valeur **Empreinte** que vous avez copiée à partir du portail Azure dans la zone de texte **Empreinte du certificat du fournisseur d’identité client**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="d1c92-208">d.</span><span class="sxs-lookup"><span data-stu-id="d1c92-208">d.</span></span> <span data-ttu-id="d1c92-209">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="d1c92-210">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d1c92-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d1c92-211">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d1c92-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d1c92-212">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1c92-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d1c92-213">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c92-213">Create an Azure AD test user</span></span>

<span data-ttu-id="d1c92-214">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c92-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="d1c92-216">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d1c92-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c92-217">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d1c92-219">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d1c92-221">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d1c92-223">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d1c92-223">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d1c92-225">a.</span><span class="sxs-lookup"><span data-stu-id="d1c92-225">a.</span></span> <span data-ttu-id="d1c92-226">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1c92-227">b.</span><span class="sxs-lookup"><span data-stu-id="d1c92-227">b.</span></span> <span data-ttu-id="d1c92-228">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1c92-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d1c92-229">c.</span><span class="sxs-lookup"><span data-stu-id="d1c92-229">c.</span></span> <span data-ttu-id="d1c92-230">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d1c92-231">d.</span><span class="sxs-lookup"><span data-stu-id="d1c92-231">d.</span></span> <span data-ttu-id="d1c92-232">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="d1c92-233">Créer un utilisateur de test OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="d1c92-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="d1c92-234">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="d1c92-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="d1c92-235">OfficeSpace Software prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d1c92-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d1c92-236">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d1c92-236">There is no action item for you in this section.</span></span> <span data-ttu-id="d1c92-237">Un utilisateur est créé lors d’une tentative d’accès à OfficeSpace Software s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="d1c92-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="d1c92-238">Si vous devez créer un utilisateur manuellement, contactez [l’équipe de support d’OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="d1c92-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d1c92-239">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c92-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="d1c92-240">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="d1c92-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="d1c92-242">**Pour affecter Britta Simon à OfficeSpace Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d1c92-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c92-243">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d1c92-245">Dans la liste des applications, sélectionnez **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![Lien OfficeSpace Software dans la liste des applications](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="d1c92-247">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="d1c92-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-249">Click **Add** button.</span></span> <span data-ttu-id="d1c92-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="d1c92-252">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d1c92-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d1c92-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1c92-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d1c92-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d1c92-255">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d1c92-255">Test single sign-on</span></span>

<span data-ttu-id="d1c92-256">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d1c92-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d1c92-257">Lorsque vous cliquez sur la vignette OfficeSpace Software dans le volet d’accès, vous êtes automatiquement connecté à votre application OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="d1c92-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1c92-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d1c92-258">Additional resources</span></span>

* [<span data-ttu-id="d1c92-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1c92-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1c92-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d1c92-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

