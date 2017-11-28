---
title: "Didacticiel : Intégration d’Azure Active Directory à ServiceChannel | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="84d2c-103">Didacticiel : Intégration d’Azure Active Directory à ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="84d2c-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="84d2c-104">Dans ce didacticiel, vous découvrez comment intégrer ServiceChannel à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84d2c-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84d2c-105">L’intégration de ServiceChannel à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="84d2c-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="84d2c-106">Dans Azure AD, vous pouvez contrôler qui a accès à ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="84d2c-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="84d2c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à ServiceChannel (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d2c-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84d2c-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="84d2c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="84d2c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84d2c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84d2c-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="84d2c-110">Prerequisites</span></span>

<span data-ttu-id="84d2c-111">Pour configurer l’intégration d’Azure AD à ServiceChannel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="84d2c-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="84d2c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d2c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84d2c-113">Un abonnement ServiceChannel pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="84d2c-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84d2c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="84d2c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84d2c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="84d2c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84d2c-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="84d2c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="84d2c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84d2c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84d2c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="84d2c-118">Scenario description</span></span>
<span data-ttu-id="84d2c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="84d2c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84d2c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="84d2c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84d2c-121">Ajout de ServiceChannel à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="84d2c-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="84d2c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d2c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="84d2c-123">Ajout de ServiceChannel à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="84d2c-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="84d2c-124">Pour configurer l’intégration de ServiceChannel à Azure AD, vous devez ajouter ServiceChannel à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="84d2c-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="84d2c-125">**Pour ajouter ServiceChannel à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d2c-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="84d2c-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84d2c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="84d2c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="84d2c-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="84d2c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="84d2c-133">Dans la zone de recherche, entrez **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-133">In the search box, type **ServiceChannel**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="84d2c-135">Dans le volet des résultats, sélectionnez **ServiceChannel** puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="84d2c-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84d2c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d2c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84d2c-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec ServiceChannel avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="84d2c-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84d2c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ServiceChannel équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d2c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="84d2c-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur ServiceChannel associé.</span><span class="sxs-lookup"><span data-stu-id="84d2c-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="84d2c-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="84d2c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="84d2c-142">Pour configurer et tester l’authentification unique Azure AD avec ServiceChannel, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="84d2c-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="84d2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="84d2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="84d2c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84d2c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84d2c-145">**[Création d’un utilisateur de test ServiceChannel](#creating-a-servicechannel-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84d2c-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="84d2c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d2c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84d2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="84d2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84d2c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d2c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84d2c-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail de gestion Azure et vous configurez l’authentification unique dans votre application ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="84d2c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="84d2c-150">**Pour configurer l’authentification unique Azure AD avec ServiceChannel, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d2c-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="84d2c-151">Dans le portail de gestion Azure, dans la page d’intégration de l’application **ServiceChannel**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="84d2c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="84d2c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="84d2c-155">Dans la section **Domaine et URL ServiceChannel**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84d2c-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="84d2c-157">a.</span><span class="sxs-lookup"><span data-stu-id="84d2c-157">a.</span></span> <span data-ttu-id="84d2c-158">Dans la zone de texte **Identificateur**, entrez la valeur `http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="84d2c-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="84d2c-159">b.</span><span class="sxs-lookup"><span data-stu-id="84d2c-159">b.</span></span> <span data-ttu-id="84d2c-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="84d2c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84d2c-161">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="84d2c-161">Please note that these are not the real values.</span></span> <span data-ttu-id="84d2c-162">Vous devez mettre à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="84d2c-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="84d2c-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="84d2c-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="84d2c-164">Contactez l’[équipe de support technique de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="84d2c-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="84d2c-165">Votre application ServiceChannel attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration d’attributs de jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="84d2c-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="84d2c-166">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="84d2c-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="84d2c-167">**NameIdentifier (Identifiant utilisateur)** est la seule revendication obligatoire et la valeur par défaut est **user.userprincipalname**, mais ServiceChannel attend que ceci soit mappé à **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="84d2c-168">Si vous prévoyez d’activer l’approvisionnement des utilisateurs juste à temps, vous devez ajouter les revendications suivantes comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84d2c-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="84d2c-169">La revendication **Rôle** doit être mappée à **user.assignedroles**, qui contient le rôle de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="84d2c-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="84d2c-170">Vous pouvez consulter le guide de ServiceChannel [ici](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) pour obtenir des instructions sur les revendications.</span><span class="sxs-lookup"><span data-stu-id="84d2c-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="84d2c-172">Cliquez [ici](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) pour savoir comment configurer un **rôle** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d2c-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="84d2c-173">Dans **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** et définissez les attributs.</span><span class="sxs-lookup"><span data-stu-id="84d2c-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="84d2c-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="84d2c-174">Attribute Name</span></span> | <span data-ttu-id="84d2c-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="84d2c-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="84d2c-176">Rôle</span><span class="sxs-lookup"><span data-stu-id="84d2c-176">Role</span></span>| <span data-ttu-id="84d2c-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="84d2c-177">user.assignedroles</span></span> |

    <span data-ttu-id="84d2c-178">a.</span><span class="sxs-lookup"><span data-stu-id="84d2c-178">a.</span></span> <span data-ttu-id="84d2c-179">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="84d2c-182">b.</span><span class="sxs-lookup"><span data-stu-id="84d2c-182">b.</span></span> <span data-ttu-id="84d2c-183">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="84d2c-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="84d2c-184">c.</span><span class="sxs-lookup"><span data-stu-id="84d2c-184">c.</span></span> <span data-ttu-id="84d2c-185">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="84d2c-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="84d2c-186">d.</span><span class="sxs-lookup"><span data-stu-id="84d2c-186">d.</span></span> <span data-ttu-id="84d2c-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="84d2c-188">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="84d2c-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="84d2c-190">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-190">Click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="84d2c-192">Dans la section **Configuration de ServiceChannel**, cliquez sur **Configurer ServiceChannel** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="84d2c-193">Notez l’**ID d’entité SAML** dans la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="84d2c-194">Pour configurer l’authentification unique du côté **ServiceChannel**, vous devez envoyer le **certificat (Base64)** téléchargé et **ID d’entité SAML** à l’[équipe de support technique de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="84d2c-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="84d2c-195">Ils effectueront les réglages nécessaires pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="84d2c-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84d2c-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d2c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="84d2c-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="84d2c-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="84d2c-199">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d2c-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="84d2c-200">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84d2c-202">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="84d2c-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84d2c-204">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84d2c-206">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84d2c-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84d2c-208">a.</span><span class="sxs-lookup"><span data-stu-id="84d2c-208">a.</span></span> <span data-ttu-id="84d2c-209">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84d2c-210">b.</span><span class="sxs-lookup"><span data-stu-id="84d2c-210">b.</span></span> <span data-ttu-id="84d2c-211">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84d2c-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84d2c-212">c.</span><span class="sxs-lookup"><span data-stu-id="84d2c-212">c.</span></span> <span data-ttu-id="84d2c-213">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="84d2c-214">d.</span><span class="sxs-lookup"><span data-stu-id="84d2c-214">d.</span></span> <span data-ttu-id="84d2c-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="84d2c-216">Création d’un utilisateur de test ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="84d2c-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="84d2c-217">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="84d2c-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="84d2c-218">Pour l’approvisionnement de l’utilisateur complet, contactez l’[équipe de support technique de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="84d2c-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="84d2c-219">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d2c-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="84d2c-220">Dans cette section, vous permettez à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="84d2c-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="84d2c-222">**Pour affecter Britta Simon à ServiceChannel, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d2c-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="84d2c-223">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="84d2c-225">Dans la liste des applications, sélectionnez **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="84d2c-227">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="84d2c-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-229">Click **Add** button.</span></span> <span data-ttu-id="84d2c-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="84d2c-232">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="84d2c-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="84d2c-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84d2c-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="84d2c-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84d2c-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="84d2c-235">Testing single sign-on</span></span>

<span data-ttu-id="84d2c-236">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="84d2c-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="84d2c-237">Quand vous cliquez sur la vignette ServiceChannel dans le volet d’accès, vous êtes normalement connecté automatiquement à votre application ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="84d2c-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84d2c-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="84d2c-238">Additional resources</span></span>

* [<span data-ttu-id="84d2c-239">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84d2c-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84d2c-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="84d2c-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png