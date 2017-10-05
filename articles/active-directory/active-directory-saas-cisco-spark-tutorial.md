---
title: "Didacticiel : Intégration d’Azure Active Directory avec Cisco Spark | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="8c320-103">Didacticiel : Intégration d’Azure Active Directory avec Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="8c320-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="8c320-104">Ce didacticiel explique comment intégrer Cisco Spark avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c320-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c320-105">L’intégration de Cisco Spark avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8c320-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8c320-106">Dans Azure AD, vous pouvez contrôler qui a accès à Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="8c320-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Cisco Spark (authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c320-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c320-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8c320-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8c320-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c320-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c320-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8c320-110">Prerequisites</span></span>

<span data-ttu-id="8c320-111">Pour configurer l’intégration d’Azure AD avec Cisco Spark, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8c320-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="8c320-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c320-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c320-113">Un abonnement Cisco Spark pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8c320-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c320-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8c320-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c320-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8c320-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c320-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8c320-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c320-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c320-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c320-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8c320-118">Scenario description</span></span>
<span data-ttu-id="8c320-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8c320-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c320-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c320-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c320-121">Ajout de Cisco Spark à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8c320-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="8c320-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c320-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="8c320-123">Ajout de Cisco Spark à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8c320-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="8c320-124">Pour configurer l’intégration de Cisco Spark à Azure AD, vous devez ajouter Cisco Spark, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8c320-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8c320-125">**Pour ajouter Cisco Spark à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c320-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8c320-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c320-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c320-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8c320-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8c320-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8c320-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8c320-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8c320-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8c320-133">Dans la zone de recherche, tapez **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="8c320-133">In the search box, type **Cisco Spark**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="8c320-135">Dans le panneau de résultats, sélectionnez **Cisco Spark**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8c320-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c320-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c320-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c320-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cisco Spark sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8c320-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8c320-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir quel utilisateur dans Cisco Spark équivaut à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c320-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="8c320-140">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="8c320-141">Dans Cisco Spark, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8c320-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8c320-142">Pour configurer et tester l’authentification unique Azure AD avec Cisco Spark, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c320-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8c320-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8c320-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8c320-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c320-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c320-145">**[Création d’un utilisateur de test Cisco Spark](#creating-a-cisco-spark-test-user)** pour avoir un équivalent de Britta Simon dans Cisco Spark, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="8c320-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c320-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c320-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c320-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8c320-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c320-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c320-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c320-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="8c320-150">**Pour configurer l’authentification unique Azure AD avec Cisco Spark, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c320-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="8c320-151">Dans le portail Azure, sur la page d’intégration de l’application **Cisco Spark**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8c320-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8c320-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8c320-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="8c320-155">Dans la section **Domaine et URL Cisco Spark**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c320-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="8c320-157">a.</span><span class="sxs-lookup"><span data-stu-id="8c320-157">a.</span></span> <span data-ttu-id="8c320-158">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="8c320-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="8c320-159">b.</span><span class="sxs-lookup"><span data-stu-id="8c320-159">b.</span></span> <span data-ttu-id="8c320-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8c320-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8c320-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="8c320-161">This value is not real.</span></span> <span data-ttu-id="8c320-162">Mettez à jour cette valeur avec l’identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="8c320-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="8c320-163">Pour obtenir cette valeur, contactez [l’équipe de support de Cisco Spark](https://support.ciscospark.com/).</span><span class="sxs-lookup"><span data-stu-id="8c320-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="8c320-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8c320-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="8c320-166">L’application Cisco Spark s’attend à ce que les assertions SAML contiennent des attributs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8c320-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="8c320-167">Configurez les attributs suivants pour cette application.</span><span class="sxs-lookup"><span data-stu-id="8c320-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="8c320-168">Vous pouvez gérer les valeurs de ces attributs à partir de la section **Attributs utilisateur** sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="8c320-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8c320-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="8c320-169">The following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="8c320-171">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c320-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="8c320-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="8c320-172">Attribute Name</span></span>  | <span data-ttu-id="8c320-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="8c320-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="8c320-174">uid</span><span class="sxs-lookup"><span data-stu-id="8c320-174">uid</span></span>    | <span data-ttu-id="8c320-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8c320-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="8c320-176">a.</span><span class="sxs-lookup"><span data-stu-id="8c320-176">a.</span></span> <span data-ttu-id="8c320-177">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="8c320-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8c320-180">b.</span><span class="sxs-lookup"><span data-stu-id="8c320-180">b.</span></span> <span data-ttu-id="8c320-181">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8c320-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8c320-182">c.</span><span class="sxs-lookup"><span data-stu-id="8c320-182">c.</span></span> <span data-ttu-id="8c320-183">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8c320-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8c320-184">d.</span><span class="sxs-lookup"><span data-stu-id="8c320-184">d.</span></span> <span data-ttu-id="8c320-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c320-185">Click **Ok**.</span></span>

7. <span data-ttu-id="8c320-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8c320-186">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8c320-188">Connectez-vous à [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) (Gestion de la collaboration dans le cloud Cisco) avec vos informations d’identification d’administrateur complètes.</span><span class="sxs-lookup"><span data-stu-id="8c320-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="8c320-189">Sélectionnez **Settings** (Paramètres), puis, dans la section **Authentication** (Authentification), cliquez sur **Modify** (Modifier).</span><span class="sxs-lookup"><span data-stu-id="8c320-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="8c320-191">Sélectionnez **intégrer un fournisseur d’identité tiers. (Avancé)** et accédez à l’écran suivant.</span><span class="sxs-lookup"><span data-stu-id="8c320-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="8c320-192">Dans la page **Import Idp Metadata** -(Importer les métadonnées Idp), glissez-déposez le fichier de métadonnées Azure AD sur la page, ou utilisez l’option d’explorateur de fichiers pour localiser et charger le fichier de métadonnées Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c320-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="8c320-193">Ensuite, sélectionnez **Require certificate signed by a certificate authority in Metadata (more secure)** (Exiger un certificat signé par une autorité de certification dans les métadonnées (plus sûr)), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="8c320-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="8c320-195">Sélectionnez **Test SSO Connection** (Tester la connexion SSO), puis, quand un nouvel onglet de navigateur s’ouvre, et authentifiez-vous auprès d’Azure AD en vous connectant.</span><span class="sxs-lookup"><span data-stu-id="8c320-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="8c320-196">Revenez à l’onglet du navigateur **Cisco Cloud Collaboration Management** (Gestion de la collaboration dans le cloud Cisco).</span><span class="sxs-lookup"><span data-stu-id="8c320-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="8c320-197">Si le test a réussi, sélectionnez **Ce test a réussi. option Activer l’authentification unique** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8c320-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="8c320-198">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8c320-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8c320-199">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8c320-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8c320-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c320-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c320-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c320-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c320-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8c320-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8c320-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c320-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8c320-205">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c320-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c320-207">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8c320-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c320-209">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8c320-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c320-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c320-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c320-213">a.</span><span class="sxs-lookup"><span data-stu-id="8c320-213">a.</span></span> <span data-ttu-id="8c320-214">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c320-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c320-215">b.</span><span class="sxs-lookup"><span data-stu-id="8c320-215">b.</span></span> <span data-ttu-id="8c320-216">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c320-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c320-217">c.</span><span class="sxs-lookup"><span data-stu-id="8c320-217">c.</span></span> <span data-ttu-id="8c320-218">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8c320-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8c320-219">d.</span><span class="sxs-lookup"><span data-stu-id="8c320-219">d.</span></span> <span data-ttu-id="8c320-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8c320-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="8c320-221">Création d’un utilisateur de test Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="8c320-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="8c320-222">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="8c320-223">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="8c320-224">Accédez à [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) (Gestion de la collaboration dans le cloud Cisco) avec vos informations d’identification d’administrateur complètes.</span><span class="sxs-lookup"><span data-stu-id="8c320-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="8c320-225">Cliquez sur **Utilisateurs**, puis sur **Gérer les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8c320-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="8c320-227">Dans la fenêtre **Manage User** (Gérer l’utilisateur), sélectionnez **Manually add or modify users** (Ajouter ou modifier manuellement des utilisateurs), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="8c320-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="8c320-228">Sélectionnez **Names and Email address** (Noms et adresse de messagerie).</span><span class="sxs-lookup"><span data-stu-id="8c320-228">Select **Names and Email address**.</span></span> <span data-ttu-id="8c320-229">Ensuite, complétez la zone de texte comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c320-229">Then, fill out the textbox as follows:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="8c320-231">a.</span><span class="sxs-lookup"><span data-stu-id="8c320-231">a.</span></span> <span data-ttu-id="8c320-232">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8c320-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="8c320-233">b.</span><span class="sxs-lookup"><span data-stu-id="8c320-233">b.</span></span> <span data-ttu-id="8c320-234">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8c320-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="8c320-235">c.</span><span class="sxs-lookup"><span data-stu-id="8c320-235">c.</span></span> <span data-ttu-id="8c320-236">Dans la zone de texte **Adresse électronique**, tapez **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8c320-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="8c320-237">Cliquez sur le signe plus pour ajouter Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c320-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="8c320-238">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8c320-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="8c320-239">Dans la fenêtre **Add Services for Users** (Ajouter des services pour les utilisateurs), cliquez sur **Save** (Enregistrer), puis sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="8c320-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8c320-240">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c320-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8c320-241">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8c320-243">**Pour affecter Britta Simon à Cisco Spark, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8c320-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="8c320-244">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8c320-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8c320-246">Dans la liste des applications, sélectionnez **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="8c320-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="8c320-248">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8c320-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8c320-250">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8c320-250">Click **Add** button.</span></span> <span data-ttu-id="8c320-251">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8c320-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8c320-253">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8c320-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8c320-254">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8c320-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c320-255">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8c320-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c320-256">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8c320-256">Testing single sign-on</span></span>

<span data-ttu-id="8c320-257">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8c320-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8c320-258">Lorsque vous cliquez sur la vignette Cisco Spark dans le volet d’accès, vous devez être authentifié automatiquement auprès de votre application Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8c320-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c320-259">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8c320-259">Additional resources</span></span>

* [<span data-ttu-id="8c320-260">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c320-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c320-261">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8c320-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

