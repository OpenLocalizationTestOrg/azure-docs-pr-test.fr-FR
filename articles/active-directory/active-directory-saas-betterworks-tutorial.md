---
title: "Didacticiel : Intégration d’Azure Active Directory à BetterWorks | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="2ae97-103">Didacticiel : Intégration d’Azure Active Directory à BetterWorks</span><span class="sxs-lookup"><span data-stu-id="2ae97-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="2ae97-104">Dans ce didacticiel, vous allez apprendre à intégrer BetterWorks à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ae97-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ae97-105">L’intégration de BetterWorks dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2ae97-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2ae97-106">Dans Azure AD, vous pouvez contrôler qui a accès à BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="2ae97-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="2ae97-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à BetterWorks (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ae97-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ae97-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2ae97-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2ae97-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ae97-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ae97-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2ae97-110">Prerequisites</span></span>

<span data-ttu-id="2ae97-111">Pour configurer l’intégration d’Azure AD avec BetterWorks, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ae97-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="2ae97-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ae97-113">Un abonnement BetterWorks pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2ae97-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ae97-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2ae97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ae97-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2ae97-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ae97-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2ae97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ae97-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ae97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ae97-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2ae97-118">Scenario description</span></span>
<span data-ttu-id="2ae97-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2ae97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ae97-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ae97-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ae97-121">Ajout de BetterWorks à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2ae97-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="2ae97-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="2ae97-123">Ajout de BetterWorks à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2ae97-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="2ae97-124">Pour configurer l’intégration de BetterWorks avec Azure AD, vous devez ajouter BetterWorks à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2ae97-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2ae97-125">**Pour ajouter BetterWorks à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ae97-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2ae97-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ae97-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2ae97-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2ae97-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2ae97-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2ae97-133">Dans la zone de recherche, tapez **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-133">In the search box, type **BetterWorks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="2ae97-135">Dans le panneau de résultats, sélectionnez **BetterWorks**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2ae97-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ae97-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ae97-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BetterWorks avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2ae97-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ae97-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur BetterWorks équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ae97-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="2ae97-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur BetterWorks associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2ae97-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="2ae97-141">Dans BetterWorks, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2ae97-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2ae97-142">Pour configurer et tester l’authentification unique Azure AD avec BetterWorks, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ae97-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2ae97-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2ae97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2ae97-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ae97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ae97-145">**[Création d’un utilisateur de test BetterWorks](#creating-a-betterworks-test-user)** pour avoir un équivalent de Britta Simon dans BetterWorks lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="2ae97-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ae97-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ae97-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ae97-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2ae97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ae97-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ae97-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="2ae97-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="2ae97-150">**Pour configurer l’authentification unique Azure AD avec BetterWorks, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ae97-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="2ae97-151">Dans le portail Azure, dans la page d’intégration de l’application **BetterWorks**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2ae97-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2ae97-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="2ae97-155">Dans la section **Domaines et URL BetterWorks**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2ae97-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="2ae97-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ae97-157">a.</span></span> <span data-ttu-id="2ae97-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="2ae97-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="2ae97-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ae97-159">b.</span></span> <span data-ttu-id="2ae97-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="2ae97-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="2ae97-161">Dans la section **Domaines et URL BetterWorks**, si vous souhaitez configurer l’application en mode initié par **SP**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ae97-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="2ae97-163">a.</span><span class="sxs-lookup"><span data-stu-id="2ae97-163">a.</span></span> <span data-ttu-id="2ae97-164">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="2ae97-165">b.</span><span class="sxs-lookup"><span data-stu-id="2ae97-165">b.</span></span> <span data-ttu-id="2ae97-166">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="2ae97-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ae97-167">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2ae97-167">These are not real values.</span></span> <span data-ttu-id="2ae97-168">Mettez à jour ces valeurs avec l’URL de réponse, l’identificateur et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="2ae97-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="2ae97-169">Pour obtenir ces valeurs, contactez [l’équipe de support technique BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="2ae97-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="2ae97-170">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2ae97-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="2ae97-172">L’application BetterWorks attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="2ae97-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2ae97-173">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="2ae97-173">Configure the following claims for this application.</span></span> <span data-ttu-id="2ae97-174">Vous pouvez gérer les valeurs de ces attributs à partir de l’onglet « **Attribut** » de l’application.</span><span class="sxs-lookup"><span data-stu-id="2ae97-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="2ae97-175">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="2ae97-175">The following screenshot shows an example for this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="2ae97-177">Dans la boîte de dialogue **Attributs du jeton SAML** , pour chaque ligne indiquée dans le tableau ci-dessous, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae97-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="2ae97-178">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="2ae97-178">Attribute Name</span></span> | <span data-ttu-id="2ae97-179">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="2ae97-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="2ae97-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="2ae97-180">saml_token</span></span>     | <span data-ttu-id="2ae97-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="2ae97-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="2ae97-182">a.</span><span class="sxs-lookup"><span data-stu-id="2ae97-182">a.</span></span> <span data-ttu-id="2ae97-183">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="2ae97-186">b.</span><span class="sxs-lookup"><span data-stu-id="2ae97-186">b.</span></span> <span data-ttu-id="2ae97-187">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="2ae97-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="2ae97-188">c.</span><span class="sxs-lookup"><span data-stu-id="2ae97-188">c.</span></span> <span data-ttu-id="2ae97-189">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="2ae97-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="2ae97-190">d.</span><span class="sxs-lookup"><span data-stu-id="2ae97-190">d.</span></span> <span data-ttu-id="2ae97-191">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-191">Click **Ok**.</span></span>

7. <span data-ttu-id="2ae97-192">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2ae97-192">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2ae97-194">Pour configurer l’authentification unique côté **BetterWorks**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à l’[équipe de support technique BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="2ae97-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="2ae97-195">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2ae97-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2ae97-196">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2ae97-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2ae97-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ae97-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ae97-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae97-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ae97-199">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae97-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2ae97-201">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ae97-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2ae97-202">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ae97-204">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ae97-206">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2ae97-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ae97-208">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae97-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ae97-210">a.</span><span class="sxs-lookup"><span data-stu-id="2ae97-210">a.</span></span> <span data-ttu-id="2ae97-211">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ae97-212">b.</span><span class="sxs-lookup"><span data-stu-id="2ae97-212">b.</span></span> <span data-ttu-id="2ae97-213">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ae97-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ae97-214">c.</span><span class="sxs-lookup"><span data-stu-id="2ae97-214">c.</span></span> <span data-ttu-id="2ae97-215">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2ae97-216">d.</span><span class="sxs-lookup"><span data-stu-id="2ae97-216">d.</span></span> <span data-ttu-id="2ae97-217">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="2ae97-218">Création d’un utilisateur de test BetterWorks</span><span class="sxs-lookup"><span data-stu-id="2ae97-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="2ae97-219">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="2ae97-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="2ae97-220">Veuillez contacter l’[équipe de support BetterWorks](mailto:support@betterworks.com) pour ajouter les utilisateurs sur la plateforme BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="2ae97-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2ae97-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae97-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2ae97-222">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="2ae97-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2ae97-224">**Pour affecter Britta Simon à BetterWorks, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ae97-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="2ae97-225">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2ae97-227">Dans la liste des applications, sélectionnez **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-227">In the applications list, select **BetterWorks**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="2ae97-229">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2ae97-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-231">Click **Add** button.</span></span> <span data-ttu-id="2ae97-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2ae97-234">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2ae97-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2ae97-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ae97-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2ae97-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ae97-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2ae97-237">Testing single sign-on</span></span>

<span data-ttu-id="2ae97-238">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2ae97-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2ae97-239">Lorsque vous cliquez sur la vignette BetterWorks dans le volet d’accès, vous devez être connecté automatiquement à votre application BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="2ae97-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ae97-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2ae97-240">Additional resources</span></span>

* [<span data-ttu-id="2ae97-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ae97-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ae97-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2ae97-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

