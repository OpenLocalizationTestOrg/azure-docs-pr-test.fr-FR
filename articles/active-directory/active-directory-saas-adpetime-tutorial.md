---
title: "Didacticiel : Intégration d’Azure Active Directory à ADP eTime | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="a3931-103">Didacticiel : Intégration d’Azure AD à ADP eTime</span><span class="sxs-lookup"><span data-stu-id="a3931-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="a3931-104">Dans ce didacticiel, vous allez apprendre à intégrer ADP eTime à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3931-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3931-105">L’intégration d’ADP eTime dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a3931-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a3931-106">Dans Azure AD, vous pouvez contrôler qui a accès à ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="a3931-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="a3931-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à ADP eTime (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3931-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3931-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a3931-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a3931-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3931-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3931-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a3931-110">Prerequisites</span></span>

<span data-ttu-id="a3931-111">Pour configurer l’intégration d’Azure AD à ADP eTime, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a3931-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="a3931-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3931-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3931-113">Un abonnement ADP eTime pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a3931-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3931-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a3931-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3931-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a3931-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3931-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a3931-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3931-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3931-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3931-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a3931-118">Scenario description</span></span>
<span data-ttu-id="a3931-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a3931-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3931-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3931-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3931-121">Ajout de ADP eTime à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a3931-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="a3931-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3931-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="a3931-123">Ajout de ADP eTime à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a3931-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="a3931-124">Pour configurer l’intégration d’ADP eTime à Azure AD, vous devez ajouter ADP eTime à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a3931-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a3931-125">**Pour ajouter ADP eTime à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a3931-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a3931-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3931-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a3931-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a3931-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a3931-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a3931-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a3931-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a3931-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a3931-133">Dans la zone de recherche, tapez **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="a3931-133">In the search box, type **ADP eTime**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="a3931-135">Dans le volet de résultats, sélectionnez **ADP eTime**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a3931-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3931-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3931-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3931-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ADP eTime, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a3931-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a3931-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur ADP eTime correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3931-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="a3931-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur ADP eTime associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a3931-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="a3931-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="a3931-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="a3931-142">Pour configurer et tester l’authentification unique Azure AD avec ADP eTime, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3931-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a3931-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a3931-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a3931-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3931-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3931-145">**[Création d’un utilisateur test ADP eTime](#creating-an-adp-etime-test-user)** pour avoir un équivalent de Britta Simon dans ADP eTime lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a3931-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3931-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3931-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3931-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a3931-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3931-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3931-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3931-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="a3931-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="a3931-150">**Pour configurer l’authentification unique Azure AD avec ADP eTime, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a3931-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="a3931-151">Dans le portail Azure, dans la page d’intégration de l’application **ADP eTime**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a3931-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a3931-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a3931-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="a3931-155">Dans la section **Domaine et URL ADP eTime**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3931-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="a3931-157">a.</span><span class="sxs-lookup"><span data-stu-id="a3931-157">a.</span></span> <span data-ttu-id="a3931-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="a3931-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="a3931-159">b.</span><span class="sxs-lookup"><span data-stu-id="a3931-159">b.</span></span> <span data-ttu-id="a3931-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="a3931-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="a3931-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a3931-161">These values are not the real.</span></span> <span data-ttu-id="a3931-162">Mettez à jour ces valeurs avec l’URL de réponse et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="a3931-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="a3931-163">Pour obtenir ces valeurs, contactez [l’équipe du support ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3931-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="a3931-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a3931-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="a3931-166">L’application ADP eTime s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="a3931-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="a3931-167">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="a3931-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="a3931-168">Le nom de la revendication sera toujours **« PersonImmutableID »** et sa valeur mappée à ExtensionAttribute2 qui contient la valeur EmployeeID de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a3931-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="a3931-169">Ici, le mappage utilisateur d’Azure AD à ADP eTime est effectué avec EmployeeID, mais vous pouvez le mapper à une valeur différente également basée sur les paramètres de votre application.</span><span class="sxs-lookup"><span data-stu-id="a3931-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="a3931-170">Par conséquent, contactez d’abord [l’équipe du support ADP eTime](https://www.adp.com/contact-us/overview.aspx) pour utiliser le bon identificateur d’utilisateur et mapper cette valeur à la revendication **« PersonImmutableID »**.</span><span class="sxs-lookup"><span data-stu-id="a3931-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="a3931-172">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a3931-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="a3931-173">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="a3931-173">Attribute Name</span></span> | <span data-ttu-id="a3931-174">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="a3931-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="a3931-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="a3931-175">PersonImmutableID</span></span> | <span data-ttu-id="a3931-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="a3931-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="a3931-177">a.</span><span class="sxs-lookup"><span data-stu-id="a3931-177">a.</span></span> <span data-ttu-id="a3931-178">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="a3931-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a3931-181">b.</span><span class="sxs-lookup"><span data-stu-id="a3931-181">b.</span></span> <span data-ttu-id="a3931-182">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="a3931-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="a3931-183">c.</span><span class="sxs-lookup"><span data-stu-id="a3931-183">c.</span></span> <span data-ttu-id="a3931-184">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="a3931-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a3931-185">d.</span><span class="sxs-lookup"><span data-stu-id="a3931-185">d.</span></span> <span data-ttu-id="a3931-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3931-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a3931-187">Avant de pouvoir configurer votre assertion SAML, vous devez contacter [l’équipe du support ADP eTime](https://www.adp.com/contact-us/overview.aspx) et lui demander d’affecter la valeur d’attribut d’identificateur unique à votre locataire.</span><span class="sxs-lookup"><span data-stu-id="a3931-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="a3931-188">Vous avez besoin de cette valeur pour configurer la revendication personnalisée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a3931-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="a3931-189">Dans la section **Configuration d’ADP eTime**, cliquez sur **Configurer ADP eTime** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a3931-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="a3931-191">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a3931-191">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="a3931-193">Pour configurer l’authentification unique du côté **ADP eTime**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe du support ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3931-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="a3931-194">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a3931-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a3931-195">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a3931-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a3931-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3931-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3931-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3931-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3931-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a3931-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a3931-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a3931-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a3931-201">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3931-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3931-203">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a3931-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3931-205">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a3931-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3931-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a3931-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3931-209">a.</span><span class="sxs-lookup"><span data-stu-id="a3931-209">a.</span></span> <span data-ttu-id="a3931-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3931-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3931-211">b.</span><span class="sxs-lookup"><span data-stu-id="a3931-211">b.</span></span> <span data-ttu-id="a3931-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3931-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3931-213">c.</span><span class="sxs-lookup"><span data-stu-id="a3931-213">c.</span></span> <span data-ttu-id="a3931-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a3931-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a3931-215">d.</span><span class="sxs-lookup"><span data-stu-id="a3931-215">d.</span></span> <span data-ttu-id="a3931-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3931-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="a3931-217">Création d’un utilisateur test ADP eTime</span><span class="sxs-lookup"><span data-stu-id="a3931-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="a3931-218">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="a3931-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="a3931-219">Pour ajouter les utilisateurs au compte ADP eTime, contactez [l’équipe du support ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3931-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a3931-220">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3931-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a3931-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="a3931-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a3931-223">**Pour affecter Britta Simon à ADP eTime, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a3931-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="a3931-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a3931-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a3931-226">Dans la liste des applications, sélectionnez **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="a3931-226">In the applications list, select **ADP eTime**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="a3931-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a3931-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a3931-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a3931-230">Click **Add** button.</span></span> <span data-ttu-id="a3931-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a3931-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a3931-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a3931-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a3931-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a3931-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3931-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a3931-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3931-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a3931-236">Testing single sign-on</span></span>

<span data-ttu-id="a3931-237">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a3931-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a3931-238">Quand vous cliquez sur la vignette ADP eTime dans le volet d’accès, vous devez être connecté automatiquement à votre application ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="a3931-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="a3931-239">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3931-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a3931-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a3931-240">Additional resources</span></span>

* [<span data-ttu-id="a3931-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3931-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3931-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a3931-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

