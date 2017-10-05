---
title: "Didacticiel : Intégration d’Azure Active Directory à FreshGrade | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="e94aa-103">Didacticiel : Intégration d’Azure Active Directory à FreshGrade</span><span class="sxs-lookup"><span data-stu-id="e94aa-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="e94aa-104">Dans ce didacticiel, vous allez apprendre à intégrer FreshGrade à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e94aa-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e94aa-105">L’intégration de FreshGrade dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e94aa-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e94aa-106">Dans Azure AD, vous pouvez contrôler qui a accès à FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e94aa-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="e94aa-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à FreshGrade (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e94aa-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e94aa-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e94aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e94aa-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e94aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e94aa-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e94aa-110">Prerequisites</span></span>

<span data-ttu-id="e94aa-111">Pour configurer l’intégration d’Azure AD dans FreshGrade, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e94aa-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="e94aa-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e94aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e94aa-113">Un abonnement FreshGrade pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e94aa-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e94aa-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e94aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e94aa-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e94aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e94aa-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e94aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e94aa-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e94aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e94aa-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e94aa-118">Scenario description</span></span>
<span data-ttu-id="e94aa-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e94aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e94aa-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="e94aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e94aa-121">Ajout de FreshGrade depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="e94aa-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="e94aa-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e94aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="e94aa-123">Ajout de FreshGrade depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="e94aa-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="e94aa-124">Pour configurer l’intégration de FreshGrade à Azure AD, vous devez ajouter FreshGrade depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e94aa-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e94aa-125">**Procédez comme suit pour ajouter FreshGrade à partir de la galerie :**</span><span class="sxs-lookup"><span data-stu-id="e94aa-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e94aa-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e94aa-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e94aa-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e94aa-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e94aa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e94aa-133">Dans la zone de recherche, entrez **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-133">In the search box, type **FreshGrade**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="e94aa-135">Dans le volet de résultats, sélectionnez **FreshGrade**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="e94aa-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e94aa-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e94aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e94aa-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec FreshGrade avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e94aa-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e94aa-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur test FreshGrade équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e94aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="e94aa-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur FreshGrade associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="e94aa-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="e94aa-141">Dans FreshGrade, assignez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="e94aa-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e94aa-142">Pour configurer et tester l’authentification unique Azure AD avec FreshGrade, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="e94aa-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e94aa-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e94aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e94aa-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e94aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e94aa-145">**[Création d’un utilisateur de test FreshGrade](#creating-a-freshgrade-test-user)** pour avoir un équivalent de Britta Simon dans FreshGrade lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e94aa-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e94aa-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e94aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e94aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="e94aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e94aa-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e94aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e94aa-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e94aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="e94aa-150">**Procédez comme suit pour configurer l’authentification unique Azure AD avec FreshGrade :**</span><span class="sxs-lookup"><span data-stu-id="e94aa-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="e94aa-151">Sur le portail Azure, à la page d’intégration de l’application **FreshGrade**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e94aa-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e94aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="e94aa-155">Dans la section **Domaine et URL FreshGrade**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e94aa-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="e94aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="e94aa-157">a.</span></span> <span data-ttu-id="e94aa-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="e94aa-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="e94aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="e94aa-159">b.</span></span> <span data-ttu-id="e94aa-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="e94aa-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="e94aa-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e94aa-161">These values are not real.</span></span> <span data-ttu-id="e94aa-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="e94aa-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e94aa-163">Pour obtenir ces valeurs, contactez [l’équipe de prise en charge des clients FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="e94aa-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="e94aa-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e94aa-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="e94aa-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e94aa-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e94aa-168">Dans la section **Configuration de FreshGrade**, cliquez sur **Configurer FreshGrade** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e94aa-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e94aa-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="e94aa-171">Pour générer l’URL des **métadonnées**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e94aa-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="e94aa-172">a.</span><span class="sxs-lookup"><span data-stu-id="e94aa-172">a.</span></span> <span data-ttu-id="e94aa-173">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-173">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="e94aa-175">b.</span><span class="sxs-lookup"><span data-stu-id="e94aa-175">b.</span></span> <span data-ttu-id="e94aa-176">Cliquez sur **Points de terminaison** pour ouvrir la boîte de dialogue **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="e94aa-178">c.</span><span class="sxs-lookup"><span data-stu-id="e94aa-178">c.</span></span> <span data-ttu-id="e94aa-179">Cliquez sur le bouton Copier pour copier l’URL du document de métadonnées de fédération (**FEDERATION METADATA DOCUMENT**), puis collez-la dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e94aa-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="e94aa-181">d.</span><span class="sxs-lookup"><span data-stu-id="e94aa-181">d.</span></span> <span data-ttu-id="e94aa-182">Accédez maintenant à la page de propriétés de **FreshGrade**, puis copiez l’**ID d’application** à l’aide du bouton **Copier** et collez-le dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e94aa-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="e94aa-184">e.</span><span class="sxs-lookup"><span data-stu-id="e94aa-184">e.</span></span> <span data-ttu-id="e94aa-185">Générez l’**URL des métadonnées** en utilisant le format suivant : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="e94aa-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="e94aa-186">Pour configurer l’authentification unique du côté de **FreshGrade**, vous devez envoyer l’**URLde métadonnées** et l’**URL du service d’authentification unique SAML** à l’[équipe de support technique de FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="e94aa-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="e94aa-187">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="e94aa-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e94aa-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="e94aa-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e94aa-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="e94aa-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e94aa-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e94aa-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e94aa-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e94aa-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="e94aa-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e94aa-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e94aa-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e94aa-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e94aa-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e94aa-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e94aa-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e94aa-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e94aa-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e94aa-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e94aa-203">a.</span><span class="sxs-lookup"><span data-stu-id="e94aa-203">a.</span></span> <span data-ttu-id="e94aa-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e94aa-205">b.</span><span class="sxs-lookup"><span data-stu-id="e94aa-205">b.</span></span> <span data-ttu-id="e94aa-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e94aa-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e94aa-207">c.</span><span class="sxs-lookup"><span data-stu-id="e94aa-207">c.</span></span> <span data-ttu-id="e94aa-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e94aa-209">d.</span><span class="sxs-lookup"><span data-stu-id="e94aa-209">d.</span></span> <span data-ttu-id="e94aa-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="e94aa-211">Création d’un utilisateur de test FreshGrade</span><span class="sxs-lookup"><span data-stu-id="e94aa-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="e94aa-212">Dans cette section, vous créez un utilisateur appelé Britta Simon dans FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e94aa-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="e94aa-213">Collaborez avec l’[équipe de support technique FreshGrade](mailTo:support@freshgrade.com) pour ajouter les utilisateurs dans la plateforme FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e94aa-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e94aa-214">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e94aa-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e94aa-215">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e94aa-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e94aa-217">**Pour affecter Britta Simon à FreshGrade, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e94aa-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="e94aa-218">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e94aa-220">Dans la liste des applications, sélectionnez **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-220">In the applications list, select **FreshGrade**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="e94aa-222">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e94aa-224">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-224">Click **Add** button.</span></span> <span data-ttu-id="e94aa-225">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e94aa-227">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e94aa-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e94aa-228">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e94aa-229">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e94aa-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e94aa-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e94aa-230">Testing single sign-on</span></span>

<span data-ttu-id="e94aa-231">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="e94aa-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e94aa-232">Quand vous cliquez sur la vignette FreshGrade dans le volet d’accès, vous devez être connecté automatiquement à votre application FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e94aa-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="e94aa-233">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e94aa-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e94aa-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e94aa-234">Additional resources</span></span>

* [<span data-ttu-id="e94aa-235">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e94aa-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e94aa-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e94aa-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

