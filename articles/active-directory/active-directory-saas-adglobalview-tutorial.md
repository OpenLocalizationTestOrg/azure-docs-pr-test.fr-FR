---
title: "Didacticiel : Intégration d’ADP GlobalView à Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ADP GlobalView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="05d51-103">Didacticiel : Intégration d’ADP GlobalView à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05d51-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="05d51-104">Dans ce didacticiel, vous allez apprendre à intégrer ADP GlobalView à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05d51-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05d51-105">L’intégration d’ADP GlobalView dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="05d51-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05d51-106">Dans Azure AD, vous pouvez contrôler qui a accès à ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="05d51-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="05d51-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à ADP GlobalView (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d51-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05d51-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="05d51-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="05d51-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05d51-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05d51-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="05d51-110">Prerequisites</span></span>

<span data-ttu-id="05d51-111">Pour configurer l’intégration d’ADP GlobalView à Azure AD, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="05d51-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="05d51-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d51-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05d51-113">Un abonnement ADP GlobalView pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="05d51-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05d51-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="05d51-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05d51-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="05d51-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05d51-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="05d51-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05d51-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05d51-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05d51-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="05d51-118">Scenario description</span></span>
<span data-ttu-id="05d51-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="05d51-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05d51-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="05d51-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05d51-121">Ajout d’ADP GlobalView à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="05d51-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="05d51-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d51-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="05d51-123">Ajout d’ADP GlobalView à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="05d51-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="05d51-124">Pour configurer l’intégration d’ADP GlobalView à Azure AD, vous devez ajouter ADP GlobalView depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="05d51-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05d51-125">**Pour ajouter ADP GlobalView à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="05d51-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05d51-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05d51-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05d51-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="05d51-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="05d51-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="05d51-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="05d51-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="05d51-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="05d51-133">Dans la zone de recherche, tapez **ADP GlobalView**.</span><span class="sxs-lookup"><span data-stu-id="05d51-133">In the search box, type **ADP Globalview**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="05d51-135">Dans le panneau des résultats, sélectionnez **ADP GlobalView**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="05d51-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05d51-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d51-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05d51-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ADP GlobalView avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="05d51-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05d51-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur ADP GlobalView correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d51-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="05d51-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur ADP GlobalView associé.</span><span class="sxs-lookup"><span data-stu-id="05d51-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="05d51-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="05d51-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="05d51-142">Pour configurer et tester l’authentification unique Azure AD avec ADP GlobalView, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="05d51-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05d51-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="05d51-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05d51-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05d51-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05d51-145">**[Création d’un utilisateur de test ADP GlobalView](#creating-an-adp-globalview-test-user)** pour avoir un équivalent de Britta Simon dans ADP GlobalView lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="05d51-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="05d51-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d51-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05d51-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="05d51-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05d51-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d51-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05d51-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="05d51-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="05d51-150">**Pour configurer l’authentification unique Azure AD avec ADP GlobalView, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="05d51-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="05d51-151">Dans le portail Azure, dans la page d’intégration de l’application **ADP GlobalView**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="05d51-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="05d51-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="05d51-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="05d51-155">Dans la section **Domaine et URL ADP GlobalView**, effectuez le étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="05d51-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="05d51-157">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.globalview.adp.com/federate` ou `https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="05d51-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05d51-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="05d51-158">The value is not real.</span></span> <span data-ttu-id="05d51-159">Mettez à jour cette valeur avec l’identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="05d51-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="05d51-160">Pour obtenir la valeur, contactez le [support ADP GlobalView](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="05d51-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="05d51-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="05d51-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="05d51-163">L’application ADP GlobalView s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="05d51-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="05d51-164">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="05d51-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="05d51-165">Le nom de la revendication sera toujours **« PersonImmutableID »** et sa valeur mappée à ExtensionAttribute2 qui contient la valeur EmployeeID de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="05d51-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="05d51-166">Ici, le mappage utilisateur d’Azure AD à ADP GlobalView est effectué avec EmployeeID, mais vous pouvez le mapper à une valeur différente également basée sur les paramètres de votre application.</span><span class="sxs-lookup"><span data-stu-id="05d51-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="05d51-167">Vous pouvez collaborer avec l’équipe ADP GlobalView pour utiliser l’identificateur correct d’un utilisateur et mapper cette valeur à la revendication **"PersonImmutableID"**.</span><span class="sxs-lookup"><span data-stu-id="05d51-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="05d51-168">Vous pouvez également mapper les revendications Email et UserID, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05d51-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="05d51-170">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="05d51-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="05d51-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="05d51-171">Attribute Name</span></span> | <span data-ttu-id="05d51-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="05d51-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="05d51-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="05d51-173">personalimmutableid</span></span> | <span data-ttu-id="05d51-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="05d51-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="05d51-175">email</span><span class="sxs-lookup"><span data-stu-id="05d51-175">email</span></span>               | <span data-ttu-id="05d51-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="05d51-176">user.mail</span></span> |
    | <span data-ttu-id="05d51-177">userId</span><span class="sxs-lookup"><span data-stu-id="05d51-177">userid</span></span>              | <span data-ttu-id="05d51-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="05d51-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="05d51-179">a.</span><span class="sxs-lookup"><span data-stu-id="05d51-179">a.</span></span> <span data-ttu-id="05d51-180">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="05d51-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="05d51-183">b.</span><span class="sxs-lookup"><span data-stu-id="05d51-183">b.</span></span> <span data-ttu-id="05d51-184">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="05d51-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="05d51-185">c.</span><span class="sxs-lookup"><span data-stu-id="05d51-185">c.</span></span> <span data-ttu-id="05d51-186">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="05d51-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="05d51-187">d.</span><span class="sxs-lookup"><span data-stu-id="05d51-187">d.</span></span> <span data-ttu-id="05d51-188">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="05d51-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05d51-189">Avant de pouvoir configurer votre assertion SAML, vous devez contacter le [support ADP GlobalView](https://www.adp.com/contact-us/overview.aspx) et lui demander d’affecter la valeur d’attribut d’identificateur unique à votre locataire.</span><span class="sxs-lookup"><span data-stu-id="05d51-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="05d51-190">Vous avez besoin de cette valeur pour configurer la revendication personnalisée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="05d51-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="05d51-191">Dans la section **Configuration d’ADP GlobalView**, cliquez sur **Configurer ADP Globalview** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="05d51-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="05d51-192">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="05d51-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="05d51-194">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="05d51-194">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="05d51-196">Pour configurer l’authentification unique côté **ADP GlobalView**, vous devez envoyer le **Certificat (en base64)** téléchargé, **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** au [support ADP GlobalView](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="05d51-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="05d51-197">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="05d51-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05d51-198">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="05d51-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05d51-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05d51-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05d51-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d51-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="05d51-201">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="05d51-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="05d51-203">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="05d51-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05d51-204">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05d51-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="05d51-206">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="05d51-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05d51-208">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="05d51-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05d51-210">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="05d51-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05d51-212">a.</span><span class="sxs-lookup"><span data-stu-id="05d51-212">a.</span></span> <span data-ttu-id="05d51-213">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05d51-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05d51-214">b.</span><span class="sxs-lookup"><span data-stu-id="05d51-214">b.</span></span> <span data-ttu-id="05d51-215">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05d51-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05d51-216">c.</span><span class="sxs-lookup"><span data-stu-id="05d51-216">c.</span></span> <span data-ttu-id="05d51-217">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="05d51-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="05d51-218">d.</span><span class="sxs-lookup"><span data-stu-id="05d51-218">d.</span></span> <span data-ttu-id="05d51-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="05d51-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="05d51-220">Création d’un utilisateur de test ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="05d51-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="05d51-221">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="05d51-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="05d51-222">Pour ajouter les utilisateurs au compte ADP GlobalView, contactez le [support ADP GlobalView](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="05d51-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05d51-223">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d51-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="05d51-224">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="05d51-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="05d51-226">**Pour attribuer Britta Simon à ADP GlobalView, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="05d51-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="05d51-227">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="05d51-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="05d51-229">Dans la liste des applications, sélectionnez **ADP GlobalView**.</span><span class="sxs-lookup"><span data-stu-id="05d51-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="05d51-231">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="05d51-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="05d51-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="05d51-233">Click **Add** button.</span></span> <span data-ttu-id="05d51-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="05d51-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="05d51-236">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="05d51-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="05d51-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="05d51-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05d51-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="05d51-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05d51-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="05d51-239">Testing single sign-on</span></span>

<span data-ttu-id="05d51-240">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="05d51-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="05d51-241">Quand vous cliquez sur la vignette ADP GlobalView dans le volet d’accès, vous êtes connecté automatiquement à votre application ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="05d51-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05d51-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="05d51-242">Additional resources</span></span>

* [<span data-ttu-id="05d51-243">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05d51-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05d51-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="05d51-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

