---
title: "Didacticiel : Intégration d’Azure Active Directory à DigiCert | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="7740b-103">Didacticiel : Intégration d’Azure Active Directory à DigiCert</span><span class="sxs-lookup"><span data-stu-id="7740b-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="7740b-104">Dans ce didacticiel, vous allez apprendre à intégrer DigiCert à Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7740b-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7740b-105">L’intégration de DigiCert à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7740b-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7740b-106">Dans Azure AD, vous pouvez contrôler qui a accès à DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7740b-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="7740b-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à DigiCert (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7740b-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7740b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7740b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7740b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7740b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7740b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7740b-110">Prerequisites</span></span>

<span data-ttu-id="7740b-111">Pour configurer l’intégration d’Azure AD à DigiCert, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7740b-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="7740b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7740b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7740b-113">Un abonnement DigiCert pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7740b-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7740b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7740b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7740b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7740b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7740b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7740b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7740b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7740b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7740b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7740b-118">Scenario description</span></span>
<span data-ttu-id="7740b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7740b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7740b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7740b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7740b-121">Ajout de DigiCert à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7740b-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="7740b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7740b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="7740b-123">Ajout de DigiCert à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7740b-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="7740b-124">Pour configurer l’intégration de DigiCert à Azure AD, vous devez ajouter DigiCert à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7740b-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7740b-125">**Pour ajouter DigiCert à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7740b-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7740b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7740b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7740b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7740b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7740b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7740b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7740b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7740b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7740b-133">Dans la zone de recherche, tapez **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="7740b-133">In the search box, type **DigiCert**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="7740b-135">Dans le panneau de résultats, sélectionnez **DigiCert**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7740b-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7740b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7740b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7740b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec DigiCert à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7740b-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7740b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur DigiCert correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7740b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="7740b-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur DigiCert associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="7740b-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="7740b-141">Dans DigiCert, attribuez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="7740b-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7740b-142">Pour configurer et tester l’authentification unique Azure AD avec DigiCert, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7740b-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7740b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7740b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7740b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7740b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7740b-145">**[Création d’un utilisateur de test DigiCert](#creating-a-digicert-test-user)** pour avoir un équivalent de Britta Simon dans DigiCert lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7740b-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7740b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7740b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7740b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7740b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7740b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7740b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7740b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7740b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="7740b-150">**Pour configurer l’authentification unique Azure AD avec DigiCert, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7740b-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="7740b-151">Dans le portail Azure, sur la page d’intégration de l’application **DigiCert**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7740b-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7740b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7740b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="7740b-155">Dans la section **DigiCert Domain and URLs** (Domaine et URL DigiCert), l’utilisateur n’aura pas à effectuer les étapes que l’application a déjà intégrées préalablement à Azure.</span><span class="sxs-lookup"><span data-stu-id="7740b-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="7740b-157">L’application DigiCert attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="7740b-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7740b-158">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="7740b-158">Configure the following claims for this application.</span></span> <span data-ttu-id="7740b-159">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="7740b-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7740b-160">La capture d’écran suivante montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="7740b-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="7740b-162">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7740b-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="7740b-163">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="7740b-163">Attribute Name</span></span> | <span data-ttu-id="7740b-164">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="7740b-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7740b-165">société</span><span class="sxs-lookup"><span data-stu-id="7740b-165">company</span></span> | <span data-ttu-id="7740b-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="7740b-166">< companycode ></span></span> |
    | <span data-ttu-id="7740b-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="7740b-167">digicertrole</span></span> | <span data-ttu-id="7740b-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="7740b-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="7740b-169">La valeur de l’attribut **société** n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="7740b-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="7740b-170">Mettez à jour cette valeur avec le code de la société réel.</span><span class="sxs-lookup"><span data-stu-id="7740b-170">Update this value with actual company code.</span></span> <span data-ttu-id="7740b-171">Pour obtenir la valeur de l’attribut **société**, contactez [l’équipe de support technique DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="7740b-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="7740b-172">a.</span><span class="sxs-lookup"><span data-stu-id="7740b-172">a.</span></span> <span data-ttu-id="7740b-173">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="7740b-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7740b-176">b.</span><span class="sxs-lookup"><span data-stu-id="7740b-176">b.</span></span> <span data-ttu-id="7740b-177">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7740b-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="7740b-178">c.</span><span class="sxs-lookup"><span data-stu-id="7740b-178">c.</span></span> <span data-ttu-id="7740b-179">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7740b-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7740b-180">d.</span><span class="sxs-lookup"><span data-stu-id="7740b-180">d.</span></span> <span data-ttu-id="7740b-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7740b-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="7740b-182">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7740b-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="7740b-184">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7740b-184">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7740b-186">Pour configurer l’authentification unique du côté **DigiCert**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="7740b-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="7740b-187">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="7740b-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7740b-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7740b-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7740b-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7740b-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7740b-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7740b-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7740b-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7740b-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="7740b-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7740b-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7740b-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7740b-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7740b-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7740b-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7740b-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7740b-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7740b-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7740b-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7740b-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7740b-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7740b-203">a.</span><span class="sxs-lookup"><span data-stu-id="7740b-203">a.</span></span> <span data-ttu-id="7740b-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7740b-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7740b-205">b.</span><span class="sxs-lookup"><span data-stu-id="7740b-205">b.</span></span> <span data-ttu-id="7740b-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7740b-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7740b-207">c.</span><span class="sxs-lookup"><span data-stu-id="7740b-207">c.</span></span> <span data-ttu-id="7740b-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7740b-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7740b-209">d.</span><span class="sxs-lookup"><span data-stu-id="7740b-209">d.</span></span> <span data-ttu-id="7740b-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7740b-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="7740b-211">Création d’un utilisateur de test DigiCert</span><span class="sxs-lookup"><span data-stu-id="7740b-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="7740b-212">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7740b-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="7740b-213">Travaillez avec [l’équipe du support technique DigiCert](mailto:support@digicert.com) pour ajouter les utilisateurs dans DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7740b-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7740b-214">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7740b-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7740b-215">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7740b-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7740b-217">**Pour affecter Britta Simon à DigiCert, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7740b-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="7740b-218">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7740b-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7740b-220">Dans la liste des applications, sélectionnez **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="7740b-220">In the applications list, select **DigiCert**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="7740b-222">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7740b-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7740b-224">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7740b-224">Click **Add** button.</span></span> <span data-ttu-id="7740b-225">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7740b-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7740b-227">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7740b-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7740b-228">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7740b-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7740b-229">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7740b-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7740b-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7740b-230">Testing single sign-on</span></span>

<span data-ttu-id="7740b-231">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7740b-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7740b-232">Lorsque vous cliquez sur la vignette DigiCert dans le panneau d’accès, vous devez être connecté automatiquement à votre application DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7740b-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="7740b-233">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7740b-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7740b-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7740b-234">Additional resources</span></span>

* [<span data-ttu-id="7740b-235">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7740b-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7740b-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7740b-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

