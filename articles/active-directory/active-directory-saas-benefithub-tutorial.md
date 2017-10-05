---
title: "Didacticiel : Intégration d’Azure Active Directory à BenefitHub | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="d25fe-103">Didacticiel : Intégration d’Azure Active Directory à BenefitHub</span><span class="sxs-lookup"><span data-stu-id="d25fe-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="d25fe-104">Dans ce didacticiel, vous allez apprendre à intégrer BenefitHub à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d25fe-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d25fe-105">L’intégration de BenefitHub dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d25fe-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d25fe-106">Dans Azure AD, vous pouvez contrôler qui a accès à BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="d25fe-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="d25fe-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à BenefitHub (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d25fe-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d25fe-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d25fe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d25fe-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d25fe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d25fe-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d25fe-110">Prerequisites</span></span>

<span data-ttu-id="d25fe-111">Pour configurer l’intégration d’Azure AD à BenefitHub, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d25fe-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="d25fe-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d25fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d25fe-113">Un abonnement BenefitHub pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d25fe-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d25fe-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d25fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d25fe-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d25fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d25fe-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d25fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d25fe-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d25fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d25fe-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d25fe-118">Scenario description</span></span>
<span data-ttu-id="d25fe-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d25fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d25fe-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d25fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d25fe-121">Ajout de BenefitHub à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d25fe-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="d25fe-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d25fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="d25fe-123">Ajout de BenefitHub à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d25fe-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="d25fe-124">Pour configurer l’intégration de BenefitHub à Azure AD, vous devez ajouter BenefitHub à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d25fe-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d25fe-125">**Pour ajouter BenefitHub à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="d25fe-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d25fe-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d25fe-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d25fe-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d25fe-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d25fe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d25fe-133">Dans la zone de recherche, tapez **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-133">In the search box, type **BenefitHub**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="d25fe-135">Dans le volet de résultats, sélectionnez **BenefitHub**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d25fe-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d25fe-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d25fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d25fe-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BenefitHub avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d25fe-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d25fe-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur BenefitHub correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d25fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="d25fe-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur BenefitHub associé.</span><span class="sxs-lookup"><span data-stu-id="d25fe-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="d25fe-141">Dans BenefitHub, affectez la valeur du **nom d’utilisateur** d’Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d25fe-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d25fe-142">Pour configurer et tester l’authentification unique Azure AD avec BenefitHub, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d25fe-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d25fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d25fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d25fe-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d25fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d25fe-145">**[Création d’un utilisateur de test BenefitHub](#creating-a-benefithub-test-user)** pour avoir un équivalent de Britta Simon dans BenefitHub lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d25fe-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d25fe-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d25fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d25fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d25fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d25fe-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d25fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d25fe-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="d25fe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="d25fe-150">**Pour configurer l’authentification unique Azure AD avec BenefitHub, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="d25fe-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d25fe-151">Dans le portail Azure, dans la page d’intégration de l’application **BenefitHub**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d25fe-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d25fe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="d25fe-155">Dans la section **Domaine et URL BenefitHub**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d25fe-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="d25fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="d25fe-157">a.</span></span> <span data-ttu-id="d25fe-158">Dans la zone de texte **Identificateur**, tapez : `urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="d25fe-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="d25fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="d25fe-159">b.</span></span> <span data-ttu-id="d25fe-160">Dans la zone de texte **URL de réponse**, tapez : `https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="d25fe-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="d25fe-161">L’application BenefitHub s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="d25fe-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="d25fe-162">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="d25fe-162">Configure the following claims for this application.</span></span> <span data-ttu-id="d25fe-163">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="d25fe-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="d25fe-165">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut du jeton SAML comme sur l’image précédente, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d25fe-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="d25fe-166">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="d25fe-166">Attribute Name</span></span> | <span data-ttu-id="d25fe-167">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="d25fe-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="d25fe-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="d25fe-168">organizationid</span></span> | <span data-ttu-id="d25fe-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="d25fe-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="d25fe-170">Cette valeur d’attribut n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="d25fe-170">This attribute value is not real.</span></span> <span data-ttu-id="d25fe-171">Remplacez cette valeur par la valeur réelle d’organizationid.</span><span class="sxs-lookup"><span data-stu-id="d25fe-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="d25fe-172">Pour obtenir la valeur réelle d’organizationid, contactez [l’équipe du support BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="d25fe-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="d25fe-173">a.</span><span class="sxs-lookup"><span data-stu-id="d25fe-173">a.</span></span> <span data-ttu-id="d25fe-174">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d25fe-177">b.</span><span class="sxs-lookup"><span data-stu-id="d25fe-177">b.</span></span> <span data-ttu-id="d25fe-178">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d25fe-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d25fe-179">c.</span><span class="sxs-lookup"><span data-stu-id="d25fe-179">c.</span></span> <span data-ttu-id="d25fe-180">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d25fe-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d25fe-181">d.</span><span class="sxs-lookup"><span data-stu-id="d25fe-181">d.</span></span> <span data-ttu-id="d25fe-182">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d25fe-183">Avant de pouvoir configurer votre assertion SAML, vous devez contacter le [support BenefitHub](https://www.benefithub.com/Home/ContactUs) et lui demander d’affecter la valeur d’attribut d’identificateur unique à votre locataire.</span><span class="sxs-lookup"><span data-stu-id="d25fe-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="d25fe-184">Vous avez besoin de cette valeur pour configurer la revendication personnalisée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d25fe-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="d25fe-185">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d25fe-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="d25fe-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d25fe-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d25fe-189">Pour configurer l’authentification unique côté **BenefitHub**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à [l’équipe du support BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="d25fe-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="d25fe-190">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="d25fe-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d25fe-191">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d25fe-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d25fe-192">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d25fe-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d25fe-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d25fe-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d25fe-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d25fe-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="d25fe-195">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d25fe-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d25fe-197">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d25fe-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d25fe-198">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d25fe-200">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d25fe-202">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d25fe-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d25fe-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d25fe-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d25fe-206">a.</span><span class="sxs-lookup"><span data-stu-id="d25fe-206">a.</span></span> <span data-ttu-id="d25fe-207">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d25fe-208">b.</span><span class="sxs-lookup"><span data-stu-id="d25fe-208">b.</span></span> <span data-ttu-id="d25fe-209">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d25fe-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d25fe-210">c.</span><span class="sxs-lookup"><span data-stu-id="d25fe-210">c.</span></span> <span data-ttu-id="d25fe-211">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d25fe-212">d.</span><span class="sxs-lookup"><span data-stu-id="d25fe-212">d.</span></span> <span data-ttu-id="d25fe-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="d25fe-214">Création d’un utilisateur de test BenefitHub</span><span class="sxs-lookup"><span data-stu-id="d25fe-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="d25fe-215">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="d25fe-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="d25fe-216">Pour ajouter des utilisateurs dans la plateforme BenefitHub, contactez [l’équipe du support BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="d25fe-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="d25fe-217">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d25fe-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d25fe-218">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d25fe-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d25fe-219">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="d25fe-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d25fe-221">**Pour attribuer Britta Simon à BenefitHub, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="d25fe-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d25fe-222">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d25fe-224">Dans la liste des applications, sélectionnez **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-224">In the applications list, select **BenefitHub**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="d25fe-226">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d25fe-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-228">Click **Add** button.</span></span> <span data-ttu-id="d25fe-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d25fe-231">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d25fe-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d25fe-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d25fe-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d25fe-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d25fe-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d25fe-234">Testing single sign-on</span></span>

<span data-ttu-id="d25fe-235">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d25fe-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d25fe-236">Quand vous cliquez sur la vignette BenefitHub dans le volet d’accès, vous devez être connecté automatiquement à votre application BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="d25fe-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="d25fe-237">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d25fe-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d25fe-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d25fe-238">Additional resources</span></span>

* [<span data-ttu-id="d25fe-239">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d25fe-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d25fe-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d25fe-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

