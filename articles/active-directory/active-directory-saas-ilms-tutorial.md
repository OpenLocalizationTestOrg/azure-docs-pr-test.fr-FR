---
title: "Didacticiel : intégration d’Azure Active Directory à iLMS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="c8e9f-103">Didacticiel : Intégration d’Azure Active Directory à iLMS</span><span class="sxs-lookup"><span data-stu-id="c8e9f-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="c8e9f-104">Dans ce didacticiel, vous allez apprendre à intégrer iLMS dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8e9f-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8e9f-105">L’intégration d’iLMS dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c8e9f-106">Dans Azure AD, vous pouvez contrôler qui a accès à iLMS</span><span class="sxs-lookup"><span data-stu-id="c8e9f-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="c8e9f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à iLMS (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8e9f-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c8e9f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c8e9f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8e9f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e9f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c8e9f-110">Prerequisites</span></span>

<span data-ttu-id="c8e9f-111">Pour configurer l’intégration d’Azure AD avec iLMS, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="c8e9f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8e9f-113">Un abonnement iLMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c8e9f-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8e9f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8e9f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8e9f-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c8e9f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8e9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8e9f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c8e9f-118">Scenario description</span></span>
<span data-ttu-id="c8e9f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8e9f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8e9f-121">Ajout d’iLMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c8e9f-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="c8e9f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="c8e9f-123">Ajout d’iLMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c8e9f-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="c8e9f-124">Pour configurer l’intégration d’iLMS avec Azure AD, vous devez ajouter iLMS à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c8e9f-125">**Pour ajouter iLMS à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8e9f-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e9f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8e9f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c8e9f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c8e9f-131">Pour ajouter la nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c8e9f-133">Dans la zone de recherche, tapez **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-133">In the search box, type **iLMS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="c8e9f-135">Dans le volet de résultats, sélectionnez **iLMS**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8e9f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8e9f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec iLMS avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c8e9f-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c8e9f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur iLMS équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="c8e9f-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur iLMS associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="c8e9f-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="c8e9f-142">Pour configurer et tester l’authentification unique Azure AD avec iLMS, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c8e9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c8e9f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8e9f-145">**[Création d’un utilisateur de test iLMS](#creating-an-ilms-test-user)** pour avoir un équivalent de Britta Simon dans iLMS lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c8e9f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8e9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8e9f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8e9f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="c8e9f-150">**Pour configurer l’authentification unique Azure AD avec iLMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8e9f-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e9f-151">Dans le portail Azure, sur la page d’intégration de l’application **iLMS**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c8e9f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="c8e9f-155">Dans la section **Domaines et URL iLMS**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP**:</span><span class="sxs-lookup"><span data-stu-id="c8e9f-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="c8e9f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-157">a.</span></span> <span data-ttu-id="c8e9f-158">Dans la zone de texte **Identificateur**, collez la valeur **Identificateur** que vous copiez à partir de la section **Fournisseur de services** des paramètres SAML dans le portail d’administration iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="c8e9f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-159">b.</span></span> <span data-ttu-id="c8e9f-160">Dans la zone de texte **URL de réponse**, collez la valeur **Point de terminaison (URL)** que vous copiez à partir de la section **Fournisseur de services** des paramètres SAML dans le portail d’administration iLMS, avec le modèle suivant `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="c8e9f-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="c8e9f-161">« 123456 » est un exemple de valeur d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="c8e9f-162">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="c8e9f-164">Dans la zone de texte **URL de connexion**, collez la valeur **Point de terminaison (URL)** que vous copiez à partir de la section **Fournisseur de services** des paramètres SAML dans le portail d’administration en tant que `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="c8e9f-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="c8e9f-165">Pour activer l’approvisionnement JIT, l’application iLMS attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c8e9f-166">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-166">Configure the following claims for this application.</span></span> <span data-ttu-id="c8e9f-167">Vous pouvez gérer les valeurs de ces attributs à partir de la section **Attributs utilisateur** sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="c8e9f-168">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-168">The following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="c8e9f-170">Créez les attributs **Département, région** et **Division** et ajoutez le nom de ces attributs dans iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="c8e9f-171">Tous les attributs présentés ci-dessus sont requis.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="c8e9f-172">Vous devez activer **Créer un compte utilisateur non reconnu** dans iLMS pour mapper ces attributs.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="c8e9f-173">Suivez les instructions [ici](http://support.inspiredelearning.com/customer/portal/articles/2204526) pour avoir une idée sur la configuration des attributs.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="c8e9f-174">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="c8e9f-175">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="c8e9f-175">Attribute Name</span></span> | <span data-ttu-id="c8e9f-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="c8e9f-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="c8e9f-177">division</span><span class="sxs-lookup"><span data-stu-id="c8e9f-177">division</span></span> | <span data-ttu-id="c8e9f-178">user.department</span><span class="sxs-lookup"><span data-stu-id="c8e9f-178">user.department</span></span> |
    | <span data-ttu-id="c8e9f-179">region</span><span class="sxs-lookup"><span data-stu-id="c8e9f-179">region</span></span> | <span data-ttu-id="c8e9f-180">user.state</span><span class="sxs-lookup"><span data-stu-id="c8e9f-180">user.state</span></span> |
    | <span data-ttu-id="c8e9f-181">department</span><span class="sxs-lookup"><span data-stu-id="c8e9f-181">department</span></span> | <span data-ttu-id="c8e9f-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="c8e9f-182">user.jobtitle</span></span> |

    <span data-ttu-id="c8e9f-183">a.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-183">a.</span></span> <span data-ttu-id="c8e9f-184">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="c8e9f-187">b.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-187">b.</span></span> <span data-ttu-id="c8e9f-188">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c8e9f-189">c.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-189">c.</span></span> <span data-ttu-id="c8e9f-190">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c8e9f-191">d.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-191">d.</span></span> <span data-ttu-id="c8e9f-192">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-192">Click **Ok**</span></span>

7. <span data-ttu-id="c8e9f-193">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="c8e9f-195">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c8e9f-195">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="c8e9f-197">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration iLMS** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="c8e9f-198">Cliquez sur **SSO:SAML** sous l’onglet **Paramètres** pour ouvrir les paramètres SAML et effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="c8e9f-200">a.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-200">a.</span></span> <span data-ttu-id="c8e9f-201">Développez la section **Fournisseur de services** et copiez les valeurs **Identificateur** et **URL du point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="c8e9f-203">b.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-203">b.</span></span> <span data-ttu-id="c8e9f-204">Sous la section **Fournisseur d’identité**, cliquez sur **importer les métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="c8e9f-205">c.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-205">c.</span></span> <span data-ttu-id="c8e9f-206">Sélectionnez le fichier **Métadonnées** téléchargé à partir du portail Azure à partir de la section **Certificat de signature SAML**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="c8e9f-208">d.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-208">d.</span></span> <span data-ttu-id="c8e9f-209">Si vous souhaitez activer JIT pour approvisionner des comptes iLMS pour l’annulation de reconnaissance d’utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="c8e9f-210">Cochez **Créer un compte utilisateur non reconnu**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="c8e9f-212">Mappez les attributs dans Azure AD avec les attributs dans iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="c8e9f-213">Dans la colonne d’attribut, spécifiez le nom des attributs ou la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="c8e9f-214">e.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-214">e.</span></span> <span data-ttu-id="c8e9f-215">Accédez à l’onglet **Règles d’entreprise** et effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="c8e9f-217">Cochez **Créer des régions, divisions et départements non reconnus** pour créer des régions, divisions et départements qui n’existent pas encore au moment de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="c8e9f-218">Cochez **Mettre à jour le profil utilisateur lors de la connexion** pour spécifier si le profil utilisateur est mis à jour à chaque ouverture de session unique.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="c8e9f-219">Si l’option **Mettre à jour les valeurs vides pour les champs non obligatoires dans le profil utilisateur** est cochée, les champs facultatifs qui sont vides lors de la connexion provoqueront également la présence de valeurs vides pour ces champs dans le profil iLMS de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="c8e9f-220">Cochez **Envoyer un e-mail de notification d’erreur** et entrez l’adresse e-mail de l’utilisateur pour lequel vous souhaitez recevoir l’e-mail de notification d’erreur.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="c8e9f-221">Cliquez sur **Enregistrer** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-221">Click **Save** button to save the settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="c8e9f-223">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c8e9f-224">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c8e9f-225">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8e9f-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8e9f-226">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8e9f-227">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c8e9f-229">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8e9f-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e9f-230">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8e9f-232">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8e9f-234">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8e9f-236">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8e9f-238">a.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-238">a.</span></span> <span data-ttu-id="c8e9f-239">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8e9f-240">b.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-240">b.</span></span> <span data-ttu-id="c8e9f-241">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8e9f-242">c.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-242">c.</span></span> <span data-ttu-id="c8e9f-243">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c8e9f-244">d.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-244">d.</span></span> <span data-ttu-id="c8e9f-245">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="c8e9f-246">Création d’un utilisateur de test iLMS</span><span class="sxs-lookup"><span data-stu-id="c8e9f-246">Creating an iLMS test user</span></span>

<span data-ttu-id="c8e9f-247">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="c8e9f-248">JIT fonctionnera si vous avez coché la case **Créer un compte utilisateur non reconnu** lors de la configuration de SAML sur le portail d’administration iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="c8e9f-249">Si vous avez besoin de créer un utilisateur manuellement, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c8e9f-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="c8e9f-250">Connectez-vous à votre site d’entreprise iLMS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="c8e9f-251">Cliquez sur **Inscrire un utilisateur** sous l’onglet **Utilisateurs** pour ouvrir la page **Inscrire un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Ajouter un employé](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="c8e9f-253">Dans la page **Inscrire un utilisateur**, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="c8e9f-255">a.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-255">a.</span></span> <span data-ttu-id="c8e9f-256">Dans la zone de texte **First Name** (Prénom), tapez le prénom, par exemple Britta.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="c8e9f-257">b.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-257">b.</span></span> <span data-ttu-id="c8e9f-258">Dans la zone de texte **Last Name** (Nom), tapez le nom, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="c8e9f-259">c.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-259">c.</span></span> <span data-ttu-id="c8e9f-260">Dans la zone de texte **ID d’e-mail** , tapez l’adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="c8e9f-261">d.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-261">d.</span></span> <span data-ttu-id="c8e9f-262">Dans la liste déroulante **Région**, sélectionnez la valeur pour la région.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="c8e9f-263">e.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-263">e.</span></span> <span data-ttu-id="c8e9f-264">Dans la liste déroulante **Division**, sélectionnez la valeur pour la division.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="c8e9f-265">f.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-265">f.</span></span> <span data-ttu-id="c8e9f-266">Dans la liste déroulante **Département**, sélectionnez une valeur pour le département.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="c8e9f-267">g.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-267">g.</span></span> <span data-ttu-id="c8e9f-268">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8e9f-269">Vous pouvez envoyer un courrier d’inscription à l’utilisateur en cochant la case **Send Registration Mail** (Envoyer un e-mail d’inscription).</span><span class="sxs-lookup"><span data-stu-id="c8e9f-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c8e9f-270">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e9f-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c8e9f-271">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c8e9f-273">**Pour affecter Britta Simon à iLMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8e9f-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e9f-274">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c8e9f-276">Dans la liste des applications, sélectionnez **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-276">In the applications list, select **iLMS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="c8e9f-278">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c8e9f-280">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-280">Click **Add** button.</span></span> <span data-ttu-id="c8e9f-281">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c8e9f-283">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c8e9f-284">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8e9f-285">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8e9f-286">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c8e9f-286">Testing single sign-on</span></span>

<span data-ttu-id="c8e9f-287">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c8e9f-288">Lorsque vous cliquez sur la mosaïque iLMS dans le volet d’accès, vous devez être connecté automatiquement à votre application iLMS.</span><span class="sxs-lookup"><span data-stu-id="c8e9f-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8e9f-289">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c8e9f-289">Additional resources</span></span>

* [<span data-ttu-id="c8e9f-290">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8e9f-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8e9f-291">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c8e9f-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

