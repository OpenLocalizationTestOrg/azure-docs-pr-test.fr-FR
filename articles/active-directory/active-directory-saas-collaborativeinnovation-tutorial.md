---
title: "Didacticiel : intégration d’Azure Active Directory à Collaborative Innovation | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Collaborative Innovation."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="12493-103">Didacticiel : intégration d’Azure Active Directory à Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="12493-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="12493-104">Dans ce didacticiel, vous allez découvrir comment intégrer Collaborative Innovation à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12493-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12493-105">L’intégration de Collaborative Innovation à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="12493-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="12493-106">Dans Azure AD, vous pouvez contrôler qui a accès à Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="12493-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="12493-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Collaborative Innovation (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12493-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12493-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="12493-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="12493-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12493-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12493-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="12493-110">Prerequisites</span></span>

<span data-ttu-id="12493-111">Pour configurer l’intégration d’Azure AD à Collaborative Innovation, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="12493-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="12493-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="12493-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12493-113">Un abonnement Collaborative Innovation pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="12493-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12493-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="12493-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12493-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="12493-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12493-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="12493-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12493-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12493-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12493-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="12493-118">Scenario description</span></span>
<span data-ttu-id="12493-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="12493-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12493-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="12493-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12493-121">Ajout de Collaborative Innovation à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="12493-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="12493-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="12493-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="12493-123">Ajout de Collaborative Innovation à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="12493-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="12493-124">Pour configurer l’intégration de Collaborative Innovation à Azure AD, vous devez ajouter Collaborative Innovation disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="12493-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="12493-125">**Pour ajouter Collaborative Innovation à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12493-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="12493-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12493-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="12493-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="12493-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="12493-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="12493-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="12493-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="12493-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="12493-133">Dans la zone de recherche, tapez **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="12493-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="12493-135">Dans le volet de résultats, sélectionnez **Collaborative Innovation**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="12493-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12493-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="12493-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12493-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Collaborative Innovation avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="12493-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="12493-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Collaborative Innovation équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12493-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="12493-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Collaborative Innovation associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="12493-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="12493-141">Dans Collaborative Innovation, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="12493-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="12493-142">Pour configurer et tester l’authentification unique Azure AD avec Collaborative Innovation, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="12493-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="12493-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="12493-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="12493-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12493-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12493-145">**[Création d’un utilisateur de test Collaborative Innovation](#creating-a-collaborative-innovation-test-user)** pour avoir un équivalent de Britta Simon dans Collaborative Innovation lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12493-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="12493-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12493-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12493-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="12493-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12493-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="12493-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12493-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="12493-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="12493-150">**Pour configurer l’authentification unique Azure AD avec Collaborative Innovation, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12493-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="12493-151">Dans le portail Azure, dans la page d’intégration de l’application **Collaborative Innovation**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="12493-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="12493-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="12493-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="12493-155">Dans la section **Domaine et URL Collaborative Innovation**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="12493-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="12493-157">a.</span><span class="sxs-lookup"><span data-stu-id="12493-157">a.</span></span> <span data-ttu-id="12493-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="12493-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="12493-159">b.</span><span class="sxs-lookup"><span data-stu-id="12493-159">b.</span></span> <span data-ttu-id="12493-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="12493-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="12493-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="12493-161">These values are not real.</span></span> <span data-ttu-id="12493-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="12493-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12493-163">Pour obtenir ces valeurs, contactez [l’équipe du support client Collaborative Innovation](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="12493-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="12493-164">L’application Collaborative Innovation attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="12493-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="12493-165">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="12493-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="12493-166">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="12493-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="12493-167">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="12493-167">The following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="12493-169">Dans la section **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** pour développer les attributs.</span><span class="sxs-lookup"><span data-stu-id="12493-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="12493-170">Dans chacun des attributs affichés, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="12493-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="12493-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="12493-171">Attribute Name</span></span> | <span data-ttu-id="12493-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="12493-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="12493-173">givenname</span><span class="sxs-lookup"><span data-stu-id="12493-173">givenname</span></span> | <span data-ttu-id="12493-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="12493-174">user.givenname</span></span> |
    | <span data-ttu-id="12493-175">surname</span><span class="sxs-lookup"><span data-stu-id="12493-175">surname</span></span> | <span data-ttu-id="12493-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="12493-176">user.surname</span></span> |
    | <span data-ttu-id="12493-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="12493-177">emailaddress</span></span> | <span data-ttu-id="12493-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="12493-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="12493-179">name</span><span class="sxs-lookup"><span data-stu-id="12493-179">name</span></span> | <span data-ttu-id="12493-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="12493-180">user.userprincipalname</span></span> |

    <span data-ttu-id="12493-181">a.</span><span class="sxs-lookup"><span data-stu-id="12493-181">a.</span></span> <span data-ttu-id="12493-182">Cliquez sur l’attribut pour ouvrir la fenêtre **Modifier l’attribut**.</span><span class="sxs-lookup"><span data-stu-id="12493-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="12493-184">b.</span><span class="sxs-lookup"><span data-stu-id="12493-184">b.</span></span> <span data-ttu-id="12493-185">Supprimez la valeur de l’URL dans **Espace de noms**.</span><span class="sxs-lookup"><span data-stu-id="12493-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="12493-186">c.</span><span class="sxs-lookup"><span data-stu-id="12493-186">c.</span></span> <span data-ttu-id="12493-187">Cliquez sur **OK** pour enregistrer le paramètre.</span><span class="sxs-lookup"><span data-stu-id="12493-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="12493-188">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="12493-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="12493-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="12493-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="12493-192">Pour configurer l’authentification unique côté **Collaborative Innovation**, vous devez envoyer les **métadonnées XML** téléchargées à [l’équipe du support technique Collaborative Innovation](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="12493-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="12493-193">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="12493-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="12493-194">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="12493-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="12493-195">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="12493-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="12493-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12493-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12493-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="12493-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="12493-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12493-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="12493-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12493-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="12493-201">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12493-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12493-203">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="12493-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12493-205">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="12493-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12493-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="12493-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12493-209">a.</span><span class="sxs-lookup"><span data-stu-id="12493-209">a.</span></span> <span data-ttu-id="12493-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12493-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12493-211">b.</span><span class="sxs-lookup"><span data-stu-id="12493-211">b.</span></span> <span data-ttu-id="12493-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12493-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12493-213">c.</span><span class="sxs-lookup"><span data-stu-id="12493-213">c.</span></span> <span data-ttu-id="12493-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="12493-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="12493-215">d.</span><span class="sxs-lookup"><span data-stu-id="12493-215">d.</span></span> <span data-ttu-id="12493-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="12493-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="12493-217">Création d’un utilisateur de test Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="12493-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="12493-218">Pour permettre aux utilisateurs d’Azure AD de se connecter à Collaborative Innovation, vous devez les approvisionner dans Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="12493-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="12493-219">Dans le cas de cette application, l’approvisionnement est automatique, car elle prend en charge l’attribution d’utilisateurs juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="12493-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="12493-220">Vous n’avez donc pas de procédure à effectuer.</span><span class="sxs-lookup"><span data-stu-id="12493-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="12493-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="12493-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="12493-222">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="12493-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="12493-224">**Pour affecter Britta Simon à Collaborative Innovation, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12493-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="12493-225">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="12493-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="12493-227">Dans la liste des applications, sélectionnez **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="12493-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="12493-229">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="12493-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="12493-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="12493-231">Click **Add** button.</span></span> <span data-ttu-id="12493-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="12493-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="12493-234">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="12493-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="12493-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="12493-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12493-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="12493-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12493-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="12493-237">Testing single sign-on</span></span>

<span data-ttu-id="12493-238">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="12493-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="12493-239">Lorsque vous cliquez sur la vignette Collaborative Innovation dans le volet d’accès, vous devez accéder à sa page de connexion.</span><span class="sxs-lookup"><span data-stu-id="12493-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="12493-240">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="12493-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="12493-241">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="12493-241">Additional resources</span></span>

* [<span data-ttu-id="12493-242">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12493-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12493-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="12493-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

