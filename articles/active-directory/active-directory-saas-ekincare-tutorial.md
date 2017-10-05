---
title: "Didacticiel : Intégration d’Azure Active Directory avec eKincare | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="86136-103">Didacticiel : Intégration d’Azure Active Directory avec eKincare</span><span class="sxs-lookup"><span data-stu-id="86136-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="86136-104">Dans ce didacticiel, vous allez apprendre à intégrer eKincare à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86136-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86136-105">L’intégration d’eKincare dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="86136-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86136-106">Dans Azure AD, vous pouvez contrôler qui a accès à eKincare.</span><span class="sxs-lookup"><span data-stu-id="86136-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="86136-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à eKincare (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86136-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86136-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="86136-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="86136-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86136-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86136-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="86136-110">Prerequisites</span></span>

<span data-ttu-id="86136-111">Pour configurer l’intégration d’Azure AD à eKincare, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="86136-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="86136-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="86136-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86136-113">Un abonnement eKincare pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="86136-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86136-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="86136-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86136-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="86136-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86136-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="86136-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86136-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86136-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86136-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="86136-118">Scenario description</span></span>
<span data-ttu-id="86136-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="86136-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86136-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="86136-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86136-121">Ajout d’eKincare à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="86136-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="86136-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="86136-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="86136-123">Ajout d’eKincare à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="86136-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="86136-124">Pour configurer l’intégration d’eKincare à Azure AD, vous devez ajouter eKincare à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="86136-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86136-125">**Pour ajouter eKincare à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86136-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86136-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86136-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86136-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="86136-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86136-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="86136-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="86136-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86136-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="86136-133">Dans la zone de recherche, tapez **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="86136-133">In the search box, type **eKincare**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="86136-135">Dans le volet de résultats, sélectionnez **eKincare**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="86136-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86136-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="86136-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86136-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec eKincare, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="86136-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86136-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur eKincare correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86136-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="86136-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur eKincare associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="86136-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="86136-141">Dans eKincare, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="86136-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="86136-142">Pour configurer et tester l’authentification unique Azure AD avec eKincare, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="86136-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86136-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="86136-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86136-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86136-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86136-145">**[Création d’un utilisateur de test eKincare](#creating-a-ekincare-test-user)** pour avoir un équivalent de Britta Simon dans eKincare lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86136-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86136-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86136-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86136-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="86136-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86136-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="86136-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86136-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application eKincare.</span><span class="sxs-lookup"><span data-stu-id="86136-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="86136-150">**Pour configurer l’authentification unique Azure AD avec eKincare, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86136-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="86136-151">Dans le portail Azure, sur la page d’intégration de l’application **eKincare**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="86136-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="86136-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="86136-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="86136-155">Dans la section **Domaine et URL eKincare**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86136-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="86136-157">a.</span><span class="sxs-lookup"><span data-stu-id="86136-157">a.</span></span> <span data-ttu-id="86136-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="86136-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="86136-159">b.</span><span class="sxs-lookup"><span data-stu-id="86136-159">b.</span></span> <span data-ttu-id="86136-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="86136-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86136-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="86136-161">These values are not real.</span></span> <span data-ttu-id="86136-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="86136-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="86136-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="86136-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="86136-164">L’application eKincare attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="86136-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="86136-165">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="86136-165">Configure the following claims for this application.</span></span> <span data-ttu-id="86136-166">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="86136-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="86136-167">La capture d’écran suivante montre un exemple de configuration.</span><span class="sxs-lookup"><span data-stu-id="86136-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="86136-168">Le nom de la revendication sera toujours **« employeeid »** et sa valeur mappée à user.extensionattribute1 qui contient la valeur employeeid de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86136-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="86136-169">Les deux autres noms de revendication, à savoir</span><span class="sxs-lookup"><span data-stu-id="86136-169">The other two claims' name i.e</span></span> <span data-ttu-id="86136-170">**« organizationid »** et **« organizationname »**, seront toujours identiques et leur valeur correspond aux détails de l’organisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86136-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="86136-172">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86136-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="86136-173">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="86136-173">Attribute Name</span></span> | <span data-ttu-id="86136-174">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="86136-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="86136-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="86136-175">employeeid</span></span> | <span data-ttu-id="86136-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="86136-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="86136-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="86136-177">organizationid</span></span> | <span data-ttu-id="86136-178">*« uniquevalue »*</span><span class="sxs-lookup"><span data-stu-id="86136-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="86136-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="86136-179">organizationname</span></span> | <span data-ttu-id="86136-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="86136-180">*user.companyname*</span></span> |

    <span data-ttu-id="86136-181">a.</span><span class="sxs-lookup"><span data-stu-id="86136-181">a.</span></span> <span data-ttu-id="86136-182">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="86136-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="86136-185">b.</span><span class="sxs-lookup"><span data-stu-id="86136-185">b.</span></span> <span data-ttu-id="86136-186">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="86136-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="86136-187">c.</span><span class="sxs-lookup"><span data-stu-id="86136-187">c.</span></span> <span data-ttu-id="86136-188">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="86136-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="86136-189">d.</span><span class="sxs-lookup"><span data-stu-id="86136-189">d.</span></span> <span data-ttu-id="86136-190">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="86136-190">Click **Ok**</span></span>

6. <span data-ttu-id="86136-191">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="86136-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="86136-193">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="86136-193">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="86136-195">Pour configurer l’authentification unique du côté **eKincare**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique d’eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="86136-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="86136-196">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="86136-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="86136-197">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="86136-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86136-198">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="86136-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86136-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86136-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86136-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="86136-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="86136-201">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="86136-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="86136-203">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86136-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86136-204">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86136-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86136-206">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="86136-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86136-208">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="86136-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86136-210">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86136-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86136-212">a.</span><span class="sxs-lookup"><span data-stu-id="86136-212">a.</span></span> <span data-ttu-id="86136-213">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86136-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86136-214">b.</span><span class="sxs-lookup"><span data-stu-id="86136-214">b.</span></span> <span data-ttu-id="86136-215">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86136-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86136-216">c.</span><span class="sxs-lookup"><span data-stu-id="86136-216">c.</span></span> <span data-ttu-id="86136-217">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="86136-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="86136-218">d.</span><span class="sxs-lookup"><span data-stu-id="86136-218">d.</span></span> <span data-ttu-id="86136-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="86136-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="86136-220">Création d’un utilisateur de test eKincare</span><span class="sxs-lookup"><span data-stu-id="86136-220">Creating a eKincare test user</span></span>

<span data-ttu-id="86136-221">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="86136-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="86136-222">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="86136-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="86136-223">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à eKincare.</span><span class="sxs-lookup"><span data-stu-id="86136-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="86136-225">**Pour affecter Britta Simon à eKincare, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="86136-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="86136-226">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="86136-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="86136-228">Dans la liste des applications, sélectionnez **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="86136-228">In the applications list, select **eKincare**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="86136-230">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="86136-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="86136-232">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="86136-232">Click **Add** button.</span></span> <span data-ttu-id="86136-233">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="86136-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="86136-235">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="86136-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86136-236">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="86136-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86136-237">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="86136-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86136-238">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="86136-238">Testing single sign-on</span></span>

<span data-ttu-id="86136-239">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="86136-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86136-240">Si vous cliquez sur la mosaïque eKincare dans le volet d’accès, vous devez vous connecter automatiquement à votre application eKincare.</span><span class="sxs-lookup"><span data-stu-id="86136-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="86136-241">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86136-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86136-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="86136-242">Additional resources</span></span>

* [<span data-ttu-id="86136-243">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86136-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86136-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="86136-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

